# Marqeta

[Marqeta](https://www.marqeta.com) is a card issuer-processor which will issue cards
for our customers. It's biggest advantage is
[Just-in-Time (JIT) funding](https://www.marqeta.com/platform/jit-funding) feature giving us
real-time control over the approval of customers transactions.

## Guides

- [Sandbox testing setup](./guides/sandbox.md)
- [Local testing setup](guides/testing.md)
- [Set PIN doc](https://swimlanes.io/u/03-xjk4ek)
- [Replacement](./guides/replacement.md)

## Marqeta Core API

This RESTful API is the main API of the Marqeta platform. It consist of objects of which
the most important are User, Card and Transaction.

### Docs

- [Integration documentation](api_integration.md)
- [Developer Guides](https://www.marqeta.com/api/guides/WIlA2isAAMkAsk6F/quick-start--marqeta-api)
- [Core API Reference](https://www.marqeta.com/api/docs/WYDH6igAAL8FnF21/api-introduction)
- [Core API Explorer](https://www.marqeta.com/api-explorer) (requires sign up)
- [Card Proxy](cardproxy.md)
- [3DS Authentication](3ds_authentication.md)
- [Flow charts](https://miro.com/app/board/uXjVPZuYRDM=/)

### Examples

- [transactions](./examples/transactions.md)
- [webhooks](./examples/auth-webhook.md)

### Users

User object represents an end customer and can be associated with multiple payment cards.
Every user has a general purpose account (**GPA**) used to fund their payments. When the JIT funding is used
GPA doesn't hold any funds, only the ledger balance which stores funds that are
currently on hold, but not yet cleared, is used.

##### Example

```
POST /users HTTP/1.1
Host: localhost:4002
Content-Type: application/json

{
    "token": "user_token_1",
    "email": "user_token_1@example.cz",
    "first_name": "Blue",
    "last_name": "Bird"
}
```

### Cards

Cards are objects representing physic or virtual payment cards. To create a card an user and a **Card Product** objects are needed.
Card Product is object defined in cooperation Marqeta and defines attributes of associated cards like card type (physical, virtual),
allowed usage methods (ATM, ecommerce...) etc.

##### Example

```
POST /cards HTTP/1.1
Host: localhost:4002
Content-Type: application/json

{
    "user_token": "user_token_1",
    "card_product_token": "twisto_card_product"
}
```

### Transactions

Transaction are immutable (excepting the state attribute) objects. They usually originate when
a transaction message from the card network is received by Marqeta. For every message received it creates a new transaction.
Marqeta also creates transactions based on internal actions like funding user's GPA in response to approved
JIT funding gateway message.

A typical payment can consist of these transactions:

1. **authorisation**

   Confirming whether a card is valid, business rules are met, and
   funds are sufficient, and then placing a temporary hold on those funds.
   When JIT funding is used Marqeta will move funds from the cad program funding source (**PFS**)
   into the user's GPA ledger balance.

2. **authorisation.advice** or **authorization.reversal**

   Increasing or decreasing the funds on hold after the authorization.
   In case of JIT funding funds moves between the cards PFS and the user's GPA.

3. **authorization.clearing**

   Finalizing the hold on funds and posting the transaction on the card holder's account.
   Moves funds out of the user's GPA ledger balance and letter settle the transaction between Marqeta and a merchants acquiring bank.
   Cleared amount can be higher or lower then the original amount on hold. In case of
   a partial clearing the rest of the authorized funds will stay on hold and addition advices
   or clearings can be invoked.

PIN debit payments consist of only one transaction:

- **pindebit**

  Card holder attempts to make a payment using their PIN. Such a transaction typically
  contains all information required for authorization and clearing in a single electronic message.
  In case of JIT funding funds are moved from the card's PFS into the user's GPA and immediately spent.

Other transaction types exist like chargeback, token.activation-request etc.
For more see [Transaction events](https://www.marqeta.com/api/docs/VjFJjCYAAM4A3YfI/event-types#transaction_events) in the docs.
