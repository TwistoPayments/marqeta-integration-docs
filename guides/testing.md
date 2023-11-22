# Testing setup

### 1) User creation

- run celery
- run twisto app `./manage.py runserver`
- run marqeta mock server `cd ../client/marqeta.py && python3 app.py`
- run card proxy auth server as described [here](https://github.com/TwistoPayments/tripping-avenger/tree/master/cardproxy#local-development-setup)

##### a) Managed by mock server

- create user `./manage.py test_user_pl --marqeta`

##### b) Not synced to mock server

- create user `./manage.py test_user_pl --marqeta-offline`

##### c) Without card profile

- create user `./manage.py test_user_pl --no-card-transactions`

### 2) Tools

Marqeta mock server

- user interface for managing transactions

        http://localhost:4002

### 3) Wallet token handling

##### Create wallet token for card

- `./manage.py add_wallet_token --card-id=1 --public-id=m-12345678 --platform=2 --state=3`
- When no `--card-id` or `--public-id` is provided, the latest used card is selected
- When `-card-id` is defined, `--public-id` is ignored
- `--state` values:
  - REQUESTED = 1
  - REQUEST_DECLINED = 2
  - ACTIVE = 3
  - USPENDED = 4
  - TERMINATED = 5
- `platform` values
  - APPLE_PAY = 1
  - GOOGLE_PAY = 2
  - SAMSUNG_PAY = 3
  - UNKNOWN = 100

##### Change wallet token state

- `./manage.py change_wallet_token_state --token-id --state='TERMINATED' --no-notification`
- by default, marqeta server sends notification to django about the update - use `--no-notification` option to disable this
