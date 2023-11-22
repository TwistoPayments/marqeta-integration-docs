# Marqeta objects

We try to map Marqeta's entities to models in our own database,
usually there's a 1 to 1 mapping.

For card management, see these models and their docstrings:

```
MarqetaProduct
MarqetaProfile
MarqetaCard
WalletToken
```

For card transaction processing,
these models are the most important:

```
CardTransaction
MarqetaTransactionLog
```

And for 3DS authentication, see

```
Marqeta3dsAuthentication
Marqeta3dsAuthenticationLog
```

## `MarqetaProfile`

Represents a customer entity created in Marqeta's systems.

### "Special" fields that require further explanation

#### `related_tokens`

Due to a bug in the past,
we created duplicate profiles for some customers.
These duplicate records exist only in Marqeta,
and they don't have matching `MarqetaProfile` records.
So, their tokens are kept in the `related_tokens` field of the original Marqeta profile.

Some cards, which seemingly belong to a certain profile,
might actually be created under one of the duplicates in `related_tokens`.
We have workarounds covering this situation in several places in the codebase,
like in `CustomerAccount.get_card_auth_proxy_update_payload` for example.
