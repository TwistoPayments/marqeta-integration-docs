# Credit transactions

In credit transactions, the impact on users limit is positive.
It means the money is transferred from the merchant to the user.

Credit transactions can have a similar life cycle to debit transactions.

## General processing info

Currently, the full life cycle of credit transactions is implemented, incl. authorization, reversals, clearing etc.,
but **everything is hidden from the user until the transaction gets cleared.**
This is due to "legacy reasons" and we'll probably work on improving the UX in the future.

### Risk review

`MarqetaTransactionLogRiskReview`

Credit authorizations above certain amount need to be reviewed by someone form the risk team.
Amount limits are currently set to `Site.auto_credit_limit`.
After review is approved, the transaction can be processed
(because everything is hidden until clearing, this does not matter too much right now).
If review gets declined because of some fraud suspicion,
we block all future transactions for the customer.
Clearing gets processed even if the authorization is still waiting for review.

All new risk reviews get reported in [#card-credit-transactions](https://app.slack.com/client/T024SRNM2/C01HZUV9JG6).

## Credit transaction types

### Refund Transactions

```
refund
refund.authorization
refund.authorization.advice
refund.authorization.clearing
refund.authorization.reversal
```

These are used when a merchant is refunding the user for the return of goods they previously purchased.

Refund transactions can be paired to a previous debit transaction (the original payment for the thing).
Marqeta does not handle this pairing on their side,
so we can only attempt to pair using data like network reference ID or merchant info.

### Original Credit Transactions (OCT)

```
original.credit.authorization
original.credit.authorization.clearing
original.credit.authorization.reversal
```

These are typically used for a simple transfer of funds to the user,
in situations like payout from a lottery win.

They are not referencing any previous debit transactions.

#### MoneySend

MoneySend is a special sub-category of OCT.
These transactions are marked as OCT
and the only way to identify MoneySend is through MCC.

Biggest difference in processing is that funds have to be made available to the customer within 30 minutes after authorization.
We currently don't support that and credits are created after clearing,
just like with other credit transactions.

Internally, we treat MoneySend the same way as other OCT,
except that risk review is retroactive - does not block further processing.

As of February 2021, MoneySend transactions are very rare.
Marqeta reported they haven't seen any in Europe.

All MoneySend transactions get reported in [#money_send-transactions](https://app.slack.com/client/T024SRNM2/C01J0LH749K) Slack channel.
