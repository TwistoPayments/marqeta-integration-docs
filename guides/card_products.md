# Marqeta Card Products

Card products serve as a setting for a card in Marqeta. We can now view and update them in our [admin](https://twisto.cz/site-admin/card/marqetaproduct/).

You can find a detailed documentation of each field in [Marqeta API documentation](https://www.marqeta.com/docs/core-api/card-products).

## Marqeta Card Product [admin](https://twisto.cz/site-admin/card/marqetaproduct/)

### Field description

- Token - unique identifier in Marqeta. Based on this field the products are fetched and created/updated.
- Other fields
  - Other fields in the admin are fields which are most commonly used in card products setting and are here for us to be able to edit them in user friendly manner.
  - We can see which of these fields differ from the ones saved in Marqeta in Finale update data field. (In a less user friendly manner)
- Finale update data - Contains a raw JSON payload which will be sent to Marqeta.
- Custom update data
  - this field can be used to edit custom Marqeta fields, which are not defined above.
  - Data from this field will always be sent to Marqeta
  - This field has to be in a valid JSON format.
- Marqeta data json - contains currently fetched data of card product from Marqeta

### Actions

- Fetch - Updates all the fields in our database with data from Marqeta.
- Submit - Locks the record and prepares it for Update in marqeta
- Unsubmit - Unlocks the record from previous submission
- Send to marqeta
  - Sends payload from `Final update data` field to Marqeta
  - This button has to be clicked by a different user who submitted the record (4 eyes)
  - Marqeta is really thorough with the field validation, so basically if you try to sent something wrong, nothing will be updated an Marqeta will return an explanatory Error.
- Save as new (bottom right)
  - Copies the record

### Creating an existing record

To create a card product, which already exists in Marqeta, all you have to do is to create a new record and fill the token field with the same token which the card product has in Marqeta. Then fill mandatory fields with random values and save the record.

- You can see all card products created in Marqeta (and their tokens) in `Marqeta data json` field in the create from.

Then click on the `Fetch` button and all the fields will update with data from Marqeta.

### Copying card product

To easily copy a product, open the product you want to copy, change token to what you want and click on `Save as new` button on bottom right (next to `Save` button)
