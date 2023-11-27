# Marqeta API Integration overview
## Requests from Twisto To Marqeta
- Production URL: `https://twisto-api.marqeta.com/v3/`
- Marqeta sandbox URL: `https://twisto-dev.marqeta.com/v3/`
- Twisto testserver mock URL: `https://marqeta.<ts_name>.ts.twisto.wtf`
- Authorization - Basic (username:password encoded in base64)
  - e.g. `Authorization: Basic dHdzdF9zYW5kYm94=`
### Users
#### Create user
- Used in: register_customer
- Doc: https://www.marqeta.com/docs/core-api/users#postUsers
- Action: POST
- Endpoint: `/users`
- Example:
```json
{
  "first_name": "Jane",
  "last_name": "Doe",
  "address1": "1234 Grove Street",
  "city": "Prague",
  "state": "CZE",
  "country": "CZE",
  "postal_code": "94702",
  "phone": "+420777345452",
  "uses_parent_account": false,
  "metadata": {
    "customer_id": "1235446364",
    "email": "john.doe@gmail.com",
    "site": 1
  },
  "notes": "Invoice ID: {customer.invoice_id} | Email: {customer.email} | Country: {customer.site.country_code}"
}
```
#### Update user
- Used in: edit_customer, edit_related_customer
- Doc: https://www.marqeta.com/docs/core-api/users#putUsersToken
- Action: PUT
- Endpoint: `/users/{token}`
- Example:
```json
{
  "first_name": "Jane",
  "last_name": "Doe",
  "token": "my_user_01",
  "address1": "1234 Grove Street",
  "city": "Prague",
  "state": "CZE",
  "country": "CZE",
  "postal_code": "94702",
  "phone": "+420777345452",
  "uses_parent_account": false,
  "metadata": {
    "customer_id": "1235446364",
    "email": "john.doe@gmail.com",
    "site": 1
  },
  "notes": "Invoice ID: {customer.invoice_id} | Email: {customer.email} | Country: {customer.site.country_code}"
}
```
#### Retrieve user
- Used in: get_customer, full_close_profile
- Doc: https://www.marqeta.com/docs/core-api/users#getUsersToken
- Action: GET
- Endpoint: `/users/{token}`

#### Create user transition
- Used in: change_customer_status, lock_customer, unlock_customer, close_customer, full_close_profile
- Doc: https://www.marqeta.com/docs/core-api/user-transitions#postUsertransitions
- Action: POST
- Endpoint: `/usertransitions`
- Example:
```json
{
    "user_token": "1234363",
    "status": "CLOSED",
    "reason_code": "01",
    "reason": "Account closed by customer",
    "channel": "SYSTEM"
}
```
#### Create client access token
- Used in: get_client_token
- Doc: https://www.marqeta.com/docs/core-api/users#postUsersAuthClientaccesstoken
- Action: POST
- Endpoint: `/users/auth/clientaccesstoken`
#### Create single-use token
- Used in: get_one_time_token
- Doc: https://www.marqeta.com/docs/core-api/users#postUsersAuthOnetime
- Action: POST
- Endpoint: `/users/auth/onetime`
### Cards
#### Create card
- Used in: create_card
- Doc: https://www.marqeta.com/docs/core-api/cards#postCards
- Action: POST
- Endpoint: `/cards`
- Example:
```json
{
    "token": "52329nbu53fn3092f3f",
    "user_token": "234634634l6",
    "card_product_token": "twisto_black_plastic_cz",
    "fulfillment": {
        "card_personalization": {
            "text": {
                "name_line_1": {"value": "John Doe"},
                "name_line_2": {"value": "Johnyyy"},
                "name_line_3": {"value": ""}
            }
        },
        "shipping": {
          "recipient_address": {
            "city" : "Prague",
            "postal_code" : "12000",
            "state" : "Czechia",
            "country" : "CZE",
            "address1" : "Sokolovska 731/24"
          }
        }
    }
}
```
#### Retrieve card
- Used in: get_card
- Doc: https://www.marqeta.com/docs/core-api/cards#getCardsToken
- Action: GET
- Endpoint: `/cards/{token}`
- Used fields:
```json
{
  "token": "mytestcard01",
  "user_token": "my_user_01",
  "last_four": "8949",
  "expiration_time": "2027-02-28T23:59:59Z",
  "state": "UNACTIVATED",
  "card_product_token": "my_cardproduct_01"
}
```
#### List cards for user
- Used in: get_customer_cards, terminate_cards, full_close_profile
- Doc: https://www.marqeta.com/docs/core-api/cards#getCardsUserToken
- Action: GET
- Endpoint: `/cards/user/{token}`
#### Create card transition
- Used in: activate_card, change_card_state, lock card, unlock card, terminate card, terminate_cards, full_close_profile
- Doc: https://www.marqeta.com/docs/core-api/card-transitions#postCardtransitions
- Action: POST
- Endpoint: `/cardtransitions`
- Example:
```json
{
    "card_token": "4235235098nfsa",
    "state": "ACTIVE",
    "channel": "API",
    "reason_code": "00"
}
```
#### Retrieve card product
- Used in: get_card_product
- Doc: https://www.marqeta.com/docs/core-api/card-products#getCardproductsToken
- Action: GET
- Endpoint: `/cardproducts/{token}`
#### Create card product
- Used in: create_card_product
- Doc: https://www.marqeta.com/docs/core-api/card-products#postCardproducts
- Action: POST
- Endpoint: `/cardproducts`
#### Update card product
- Used in: update_card_product
- Doc: https://www.marqeta.com/docs/core-api/card-products#putCardproductsToken
- Action: PUT
- Endpoint: `/cardproducts/{token}`
#### Create PIN control token
- Used in: action_setpin
- Doc: https://www.marqeta.com/docs/core-api/pins#postPinsControltoken
- Action: POST
- Endpoint: `/pins/controltoken`
### Digital Wallets
#### Retrieve digital wallet token
- Used in: get_digital_wallet_token
- Doc: https://www.marqeta.com/docs/core-api/digital-wallets-management#getDigitalwallettokensToken
- Action: GET
- Endpoint: `/digitalwallettokens/{token}`
- Used Fields:
```json
{
  "token": "my_token_0000",
  "card_token": "my_card_01",
  "expiration_time": "2027-02-28T23:59:59Z",
  "state": "ACTIVE",
  "fulfillment_status": "PROVISIONED",
  "token_service_provider": {
    "token_pan": "533485259258529855",
    "token_reference_id": "my_token_reference_id_1600",
    "pan_reference_id": "my_pan_reference_id_0073",
    "token_requestor_id": "my_token_requestor_id_0373"
  },
  "device": {
    "type": "MOBILE_PHONE",
    "device_id": "my_device_id_9575",
    "name": "Phone Name"
  }
}
```
#### List digital wallet tokens for card
- Used in: get_card_wallet_tokens
- Doc: https://www.marqeta.com/docs/core-api/digital-wallets-management#getDigitalwallettokensCardCardtoken
- Action: GET
- Endpoint: `/digitalwallettokens/card/{card_token}`
#### Create digital wallet token transition
- Used in: change_digital_wallet_token_state, terminate_wallet_tokens, terminate_cards, full_close_profile
- Doc: https://www.marqeta.com/docs/core-api/digital-wallets-management#postDigitalwallettokentransitions
- Action: POST
- Endpoint: `/digitalwallettokentransitions`
#### Create digital wallet token provisioning request for Google Wallet:
- Used in: get_google_pay_tokenization_data
- Doc: https://www.marqeta.com/docs/core-api/digital-wallets-management#postDigitalwalletprovisionrequestsAndroidpay
- Action: POST
- Endpoint: `/digitalwalletprovisionrequests/androidpay`
#### Create digital wallet token provisioning request for Apple Wallet:
- Used in: get_apple_pay_tokenization_data
- Doc: https://www.marqeta.com/docs/core-api/digital-wallets-management#postDigitalwalletprovisionrequestsApplepay
- Action: POST
- Endpoint: `/digitalwalletprovisionrequests/applepay`
#### Create request for Apple Wallet web push provisioning (Not in use)
- Used in: apple_pay_push_provisioning
- Doc: https://www.marqeta.com/docs/core-api/digital-wallets-management#generateApplePayWPPJWT
- Action: POST
- Endpoint: `/digitalwallets/wpp/applePayJWT`
#### Create request for Google Wallet web push provisioning (Not in use)
- Used in: google_pay_push_provisioning
- Doc: https://www.marqeta.com/docs/core-api/digital-wallets-management#sendOPCDataToGooglePay
- Action: POST
- Endpoint: `/digitalwallets/wpp/googlePayPushProvisioningNotification`
### Transactions
#### Retrieve transaction
- Used in: get_transaction
- Doc: https://www.marqeta.com/docs/core-api/transactions#getTransactionsToken
- Action: GET
- Endpoint: `/transactions/{token}`
#### List transactions
- Used in: get_transactions
- Doc: https://www.marqeta.com/docs/core-api/transactions#getTransactions
- Action: GET
- Endpoint: `/transactions`
#### Supported transaction types:
  - [authorization](./examples/auth+clearing.md)
  - [authorization.advice](./examples/authorization.advice.md)
  - [authorization.clearing](./examples/auth+clearing.md)
  - [authorization.incremental](./examples/authorization.incremental.md)
  - [authorization.reversal](./examples/auth+full-reversal+clearing.md)
  - [authorization.reversal.issuerexpiration](./examples/authorization.reversal.issuerexpiration.md)
  - authorization.standin - no transactions of this type
  - [authorization.clearing.chargeback.completed](./examples/authorization.clearing.chargeback.completed.md)
  - authorization.chargeback.completed.reversal - no transactions of this type
  - [refund.authorization](./examples/refund.authorization.md)
  - refund.authorization.advice - no transactions of this type
  - refund.authorization.reversal - no transactions of this type
  - [refund.authorization.clearing](./examples/refund.authorization.clearing.md)
  - [original.credit.authorization](./examples/original.credit.authorization.md)
  - [original.credit.authorization.clearing](./examples/original.credit.authorization.clearing.md)
  - original.credit.authorization.reversal - no transactions of this type

### Disputes
#### Retrieve dispute case
- Used in: get_dispute
- Doc: https://www.marqeta.com/docs/core-api/dispute-cases-mastercard#_retrieve_dispute_case
- Action: GET
- Endpoint: `/cases/{token}`

## Requests from Marqeta to Twisto

### Webhooks
For security reasons we fetch the resource from marqeta using respective GET endpoint
to process the changed resource. The resource is fetched using the token from the webhook event.
- Doc: https://www.marqeta.com/docs/core-api/webhooks
- Event-types: https://www.marqeta.com/docs/core-api/event-types
- Endpoint: `<twisto_main>/marqeta/<secret>/webhook/transactions`

#### User transitions
- Doc: https://www.marqeta.com/docs/core-api/event-types#_account_holder_transition_events
- Related data - Retrieve User
#### Cards transitions events
- Doc: https://www.marqeta.com/docs/core-api/event-types#_card_transition_events
- Related data - Retrieve Card
#### Digital wallet transactions event
- Doc: https://www.marqeta.com/docs/core-api/event-types#_digital_wallet_token_transition_events
- Related data - Retrieve Digital wallet token

#### Transactions events
- Doc: https://www.marqeta.com/docs/core-api/event-types#_transaction_events
- Related data - Retrieve transaction

### Just in time authorization
- Doc: https://www.marqeta.com/docs/core-api/gateway-jit-funding-messages#_jit_funding_requests
- Action: POST
- Endpoint: `<twisto_proxy>/jit/` -> `<twisto_main>/marqeta/<secret>/jit/`
- [Example](./examples/jit-authorization-message.md)

## Strong Customer Authentication (SCA/3DS)

### Just In Time Decision
- Doc: https://www.marqeta.com/docs/core-api/3ds#_delegate_decisioning_determine_whether_to_send_an_sca
- Endpoint: `<twisto_cardproxy>/jit/three-ds/decision` -> `<twisto_main>/marqeta/<secret>/jit/three-ds/authentication-decision/`

### Challenge request
- Doc: https://www.marqeta.com/docs/core-api/3ds#_receive_an_advanced_authentication_challenge
- Endpoint: `<twisto_main>//three-ds/authentication/`
- The endpoint name is misleading but it is according to MQ doc - should be called challenge-request


### Challenge result
Send a authentication challenge result to Marqeta (misleading endpoint name)
- Used in: submit_authentication_result
- Doc: https://www.marqeta.com/docs/core-api/3ds#_update_an_authentication_result_to_marqeta
- Action: POST
- Endpoint: `<marqeta_acs_server>/v3/three-ds/authentication-result`
  - The endpoint should be called `/challenge-result` to make more sense…

### Final authentication result
- Doc: https://www.marqeta.com/docs/core-api/3ds#_notify_a_3ds_completion_status
- Endpoint: <twisto_main>/three-ds/authentication-result/
