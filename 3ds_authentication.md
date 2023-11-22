# Marqeta 3DS authentication

Before cardholder makes an online payment he should receive push notification to authenticate the payment in Twisto app for improved security and fraud protection.

To do this complete flow with marqeta these steps have to be done

1. Decide, whether the authentication is necessary - **decision**
2. Send push notification - **challenge**
3. Receive cardholders action - **challenge-result**

Marqeta does everything on its side (except sending push notifications) and basically only informs us about the state of the authentication.

# Marqeta Integration

- the documentation to marqeta 3ds api can be found in this document - https://drive.google.com/drive/u/1/folders/12F2QYMKaiONpn26UX28mpiaWlN6K2tRy
- This document is also helpful - https://drive.google.com/drive/u/1/folders/12F2QYMKaiONpn26UX28mpiaWlN6K2tRy
- Miro board with flows https://miro.com/app/board/uXjVPZuYRDM=/?share_link_id=424817368235

### Marqeta sends requests to our 3 endpoints

- `/jit/three-ds/authentication-decision` - `JITAuthenticationDecisionView` (through cardproxy - see below)
  - Decides whether to send push notification (or sms) using `AuthenticationDecisionEngine` and sends the result in response back to marqeta.
- `/three-ds/authentication` - `AuthenticationChallengeView`
  - By sending request to this endpoint, marqeta tells us to send push notification to the cardholder - so it does so. The response is only `200 OK`.
- `/three-ds/authentication-result` - `AuthenticationFinalResultView`
  - Marqeta sends request to this endpoint to send result of the authentication, which may differ from the result we send to marqeta

### We send challenge result requests to one Marqeta's endpoint `/three-ds/challenge-result`

- this endpoint is used to submit the challenge result (what cardholder did with the push notification)
- We call this endpoint from `ResolveAuthentication`, when cardholder confirms or cancels the authentication or from `CustomerAccount.three_ds_card_lock` when cardholder fails to login to the app.

### Cardproxy

- To assure high availability and quick response time, the decision endpoint was also implemented in cardproxy - `AuthenticationDecisionView`. Marqeta sends decision requests here and when our main servers fail to response, the cardproxy will decide on its own, what to do. This brings more complexity to the implementation, since the engine and data parsing is shared between the apps to make it unified - `AuthenticationDecisionData` and `AuthenticationDecisionEngine`
- There have to be new data present in the cardproxy, so `base_currency` and `three_ds` fields were added to CustomerData and have to be synced.
- We also need to send conversion rates to cardproxy, because there is not any conversion rate information in the decision request, only amount and currency
  - `ConversionRatesView` - `/conversion-rates/`.
  - The rates are updated from `RatesScrapingTask` using `UpdateConversionRatesTask` when new rates are updated from mastercard in our main app

## Flow description

Possible states of authentication:

- `APP_CONFIRMATION_PENDING` - authentication need the confirmation from user to be processed further
- `STATUS_FINAL_RESULT_PENDING` - authentication need the verification from marqeta to be finally resolved
- `RESOLVED` - authentication is resolved (result is set)

Possible results of authentication:

- `SUCCEEDED` - authentication is positively resolved
- `FAILED` - authentication has failed
- `CANCELLED` - authentication is cancelled by the user

### Basic flow

1. Decision
   - Marqeta sends decision request to cardproxy
   - Cardproxy resends the request to `JITAuthenticationDecisionView`
   - `AuthenticationDecisionEngine` decides that the transaction should be authenticated via push notification, because the cardholder has compatible mobile app
   - Main app sends response about it to back to cardproxy, which resends it to marqeta
2. Challenge
   - Marqeta sends us challenge request to `AuthenticationChallengeView`
   - We send push notification using `Marqeta3dsPushTask` to cardholder and respond OK.
   - Push notification arrives to cardholder's device.
3. Confirmation
   - Authentication - state: `APP_CONFIRMATION_PENDING`, result: `None`
   - Cardholder confirms authentication in the app.
   - App calls `ResolveAuthentication` with result,
     `waitingTime` in seconds and `finalUrl` (url to redirect cardholder back to the merchant app) is returned.
   - Mutation sends result to marqeta using `APIProvider.submit-challeng-result`
   - Authentication - state: `FINAL_RESULT_PENDING`, result: `None`
4. Result
   - Frontend checks/requests state and result of the authentication every second.
   - Within `waitingTime` time marqeta basically just confirms the result by sending request to `AuthenticationFinalResultView`
   - Authentication - state: `RESOLVED`, result: `SUCCEEDED`
   - Frontend shows a message that everything went well.

### Exempted flow

1. Decision
   - Marqeta sends decision request to cardproxy
   - Cardproxy resends the request to `JITAuthenticationDecisionView`
   - `AuthenticationDecisionEngine` decides that the transaction should not be authenticated = **exempted**
   - Main app sends response about it to back to cardproxy, which resends it to marqeta
2. Result
   - Marqeta sends us the result by sending request to `AuthenticationFinalResultView`

### Push not available flow A

1. Decision
   - Marqeta sends decision request to cardproxy
   - Cardproxy resends the request to `JITAuthenticationDecisionView`
   - `AuthenticationDecisionEngine` decides that the transaction should be authenticated via OTP (SMS) - because cardholder does not have compatible app.
   - Main app sends response about it to back to cardproxy, which resends it to marqeta
2. Marqeta performs challenge via SMS
   - completely without any action on our side
3. Result
   - Marqeta sends us the result by sending request to `AuthenticationFinalResultView`

### Push not available flow B

1. Decision
   - Marqeta sends decision request to cardproxy
   - cardproxy resends the request to `JITAuthenticationDecisionView` but fails
   - `AuthenticationDecisionEngine` in cardproxy decides that the transaction should be authenticated via OTP (SMS) - because cardholder does not have compatible app.
   - cardproxy sends result back to marqeta
2. Marqeta performs challenge via SMS
   - completely without any action on our side
3. Result
   - Marqeta sends us the result by sending request to `AuthenticationFinalResultView`

### No final/definitive result of the authentication

1. Decision
   - Marqeta sends decision request to cardproxy
   - Cardproxy resends the request to `JITAuthenticationDecisionView`
   - `AuthenticationDecisionEngine` decides that the transaction should be authenticated via push notification, because the cardholder has compatible mobile app
   - Main app sends response about it to back to cardproxy, which resends it to marqeta
2. Challenge
   - Marqeta sends us challenge request to `AuthenticationChallengeView`
   - We send push notification using `Marqeta3dsPushTask` to cardholder and respond OK.
   - Push notification arrives to cardholder's device.
3. Confirmation
   - Authentication - state: `APP_CONFIRMATION_PENDING`, result: `None`
   - Cardholder confirms authentication in the app.
   - App calls `ResolveAuthentication` with result,
     `waitingTime` in seconds and `finalUrl` (url to redirect cardholder back to the merchant app) is returned.
   - Mutation sends result to marqeta using `APIProvider.submit-challeng-result`
   - Authentication - state: `FINAL_RESULT_PENDING`, result: `None`
4. Result
   - Frontend checks/requests state and result of the authentication every second.
   - After `waitingTime` time, we are showing a waiting screen with a timer on it with max value of 10 min.

# Authentication Models

The idea was to create an abstract model - `Authentication`, to allow us to create only one `ResolveAuthentication` which should work for any model, which will inherit from the general model.
To make this work we had to create `AuthenticationNode` interface in GQL

## Marqeta3dsAuthentication

`Marqeta3dsAuthentication` model has some extra fields - reflecting that it is a card transaction authentication.

What is also added here is `Marqeta3dsAuthenticationLog` which should come really handy in debugging. Every relevant request and response regarding the authentication is saved here throughout any flow (except these not involving the main app, obviously.). The basic flow should create 5 logs.
Other than that, this model does not serve any purpose and could be deleted if everything worked perfectly.
There is an admin to see what's really going on. (But probably needs some work to be really nice.)

# Authentication Decision Engine

The `AuthenticationDecisionEngine` decides two thing - whether to Challenge or Exempt the transaction and whether to send push notification or fallback to Marqeta's OTP (SMS)

The rules are as follows:

- Card acceptors challenge preference is set to CHALLENGE
- every recurring transaction should be exempted.
- Transaction with larger amount than cardholders limit (600CZK or 100PLN) should be challenged
- When previous 5 transactions were exempted this one should be challenged
- When cumulative amount of previous transactions exceeds cardholders cumulative limit (2500CZK 450PLN) this one should be challenged

If cardholder has sufficient app version, we send the push notification.

- First supported android version is `2.1.1.5`
- First supported iOS version is `1.27`
