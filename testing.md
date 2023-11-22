# Working with testservers

Use [Twisto toolbelt](https://github.com/TwistoPayments/twisto-toolbelt) to set up a new test server.

When deploying a branch different than `master`,
keep in mind that only tripping-avenger/twisto gets deployed in `{your_branch}`.
Rest of the services are there in latest builds of `master`.

Use kubectl directly on the test server to switch to a different build:

```
kubectl edit statefulset marqeta-mock

kubectl edit pod {your-cardproxy-pod-name}
```

# Testing CZ user

command `./manage.py test_user`

By default, user is created with wirecard plastic card and wristband and transactions along with other two users with splits

## Options

- `--standard`: standard account
- `--output-url`: Output only login url
- `--get-casper-params`: Output json with invoice details fot casper tests
- `--overdue-period`: One period not deferred but overdue
- `--full-email-payment`: Full email payment data set
- `--upgrade-request`: Add upgrade request data
- `--no-card-transactions`: Don`t Create Twisto card transactions and wirecard card
- `--card-prod`: Sets production environment for API calls. Default is testing env
- `--inactive-cards`: No activate cards if enabled
- `--debug`: Enables debugging API communication
- `--split`: Generate splits
- `--marqeta-profile`: Creates Marqeta profile
- `--enable-google-pay`: "Sets google pay enabled
- `--virtual-card`: Creates mq virtual card for user

## Examples

- to create user with virtual card and without WD card, use

       ./manage.py test_user --virtual-card --no-card-transactions

# Testing PL user

See `twisto/apps/card/docs/marqeta/guides/testing.md`
