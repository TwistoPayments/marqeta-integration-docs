# Dynamic decline Rules - Managed card risk engine

To be able to set and change card risk rules for non-technical users, we created a new section in [Django admin](https://www.twisto.cz/site-admin/card/declinerule/) - `Decline rules`

This section should provide full ability to create complex rules for declining card transactions and it should be able to almost completely replace rules defined in the code in the future. Right now it is not possible to compare two dynamic values, like users limit.

Ability to create rules via Admin will also allow us to promptly stop any potential frauds.

### Safety notice

Improperly configured rule could potentially decline all or most of card transactions, which is very dangerous. Because of this there is an emphasis on testing and peer review. Only highly capable and trained users should have access to this section.

## High level description

Each record (rule) in the admin stands for a standalone decline rule. When the rule is triggered the transaction is declined with decline reason set in the rule.

The rule is triggered when all conditions are met - the conditions are in logical AND.

There can also be exceptions to the rule - when any exception on the rule is triggered, the rule itself is not triggered.

For rule to become active there has to be real authorizations linked to the rule - both which are declined and which are not - for users to be able to test, if the rule applies correctly.

After all is set and successfully tested, the rule has to be submitted by one user and approved by a different one before it can be enabled.

Once the rule is approved, it can never be changed, only replaced. (By Update button, see below).

## Main Decline rule record

Main decline rule record contains some information about the rule and settings how the rule will behave.

- `Name` - should provide a brief description of the rule and main conditions
- `Decription` - should provide a full description of all conditions and exceptions and a reason of the rule
- `Decline reason` - defines what will be shown to the customer as a decline reason
- `Priority` - Decline reason of the triggered rule with highest priority will be shown to the customer in his app.
- `Site` - This field is optional - when no site is selected, the rule applies for all sites. When the site is set the rule is only visible in admin for that site and applies only to transactions for that site.
- `Previous rule link` - Link to rule which was replaced (or is about to be replaced) by this rule
- `Updated by rule link` - Link to rule which replaced (or is about to replace) this rule

## Decline conditions

Conditions are the hearth of the rule - they define individual conditions which have to be met for the rule to trigger.

All values are compared as case-insensitive strings unless `Numeric cast` is set to True.

- `Field` - which **field** of the transaction (or related to the transaction) should be used.
- `Operator` - how the values should be compared.
- `Value` - value which will be used for the comparison with the value from the transaction.
- `Numeric cast` - necessary to set, when we want to compare numeric values. e.g. without numeric cast set 1000 > 9 would be false, because 1 is alphabetically before 9

### Fields

Fields are written as text as they can be found in Card transaction or Marqeta Transaction Log records. Field names are usually the same as they appear in admin, only lowercase and spaces are written with underscores `_`.
You can also access related objects using `.` between the field names.
Be careful with accesing related objects, it can potentially slow down whole transaction processing.

Commonly used fields:

- `amount`, `merchant_category_code`, `merchant_name`, `merchant_id`, `terminal_id`
- `merchant_country`: country code with three letters `CZE`, `USA`, `DEU` - [ISO 3166-1 Alpha-3](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes)
- `card.product_token`: cz_card_yellow | pl_card_yellow | cz_card_black | pl_card_black | cz_card_virtual | pl_card_virtual
- `source`: ECOMMERCE:`1`, ATM: `2`, POS: `3`, CASH: `4`, MOTO: `5`, IMPRINT: `6`, UNKNOWN: `7`
- `customer_plan`: Online: `1`, Standard: `2`, Premium/Space: `3`
- `wallet_token.platform`: Apple pay: `1`, Google pay: `2`, Samsung pay: `3`, Unknown/Other: `100`
- `data.<field>.<field>`: to access field directly as seen in tha data in a log.

### Operators

When a field is missing from the transaction all operators return False (except `Is False`), causing the condition not to trigger.

Some operators are self explanatory - here are the more complex ones

- `Is in` - Is true when a value in transaction matches matches any value in the list
  - the list is defined by comma separated values - e.g. 'RUS,UKR, CHN'
- `Is True` - Checks whether the value is True or exists
- `Is False` - Checks whether the value is False or does not exist
  - for `Is True` and `Is False` operators if you want `False` or `0` values to behave as logical False, you need to select Numeric cast.
  - These fields could come very handy when checking for presence of a field.
  - value in `Value` field is ignored.

## Exceptions

Exceptions are special Decline rule records which will be checked when parent rule triggers. They can be linked to parent on the parent detail.

The operators and exceptions definitions are the same as on the main Decline rule described above. Other fields do not have any impact on the rule execution.

The exceptions can be chained - even exception can have exceptions giving us the ability to create more complex rules.

To assign decline conditions to the exceptions you need to create it first (add name and description and click `Save` on the main record) and than click `Change` above the exception name

**If any of the exceptions for the parent rule triggers, the parent rule is not triggered**

## Approving and Enabling a Decline Rule

To be able to enable a decline rule, the rule has to be successfully tested, then submitted and than approved by a different user than the one who submitted it.

The rule can be immediately disabled and then enabled without any additional steps.

Once the rule is approved (or force enabled), it can never be changed.

Submitting, Approving, Enabling and disabling can be done with the buttons in the header of the Decline rule record.

Once the rule is Enabled it will start to decline transactions **immediately**.

## Testing

To test a Decline rule a user has to select an already existing authorization and then select whether he expects it to be declined or authorized. To run the test the user has to click a `Test` button.

To consider a Decline rule as successfully tested there has to be 3 authorized and 3 declined authorizations attached to the rule with a matching expected result and the real result.
Without this the rule cannot be submitted for approval.

Also each transaction has to contain all the fields which are defined in the conditions, otherwise the test isn't successful. (The field does not have to be present for Is False operator)

When the rule is **Submitted** you can see real transactions which would be declined by this rule in `Declined transactions - if enabled` inline.
Once the rule is **Enabled** the really declined transactions will appear in `Declined transactions` inline.

## Updating a rule

To avoid the rule to be temporarily malfunctional or without review when we try to change it - e.g. when we want to add new condition or exception - update system was implemented.
Once the rule was enabled, it can never be changed, so for a better convenience there is an **Update** button.

When you click the update button, new exact copy of the record will be created and prepared for update. Once the copy is updated, tested, approved and enabled. The old record is disabled and hidden.

## Force Approve

To be able to really quickly stop some fraud, there is a Force Approve button, which does not require different user and multiple tests for the rule to becom approved.
Only condition for \*_Force approve_ is to select one transaction which will be authorized and one which will be declined and test it.

Only users with `card.risk_master` role can see and use this button.

## Examples

Decline ecommerce transaction for online plan:

```
customer_plan - Equals - 1
source - Equals - 1
```

Blacklist by MCC with name Whitelist

```
merchant_category - Is in - 6010,6011,6012,4829,6211,6051,7995,7801,5967,9406
Exception1
    merchant_category - Equals - 4829
    merchant_name - Starts with - DEPO
Exception2
    merchant_category - Equals - 4829
    merchant_name - Starts with - DHL
Exception3
    merchant_category - Equals - 4829
    merchant_name - Starts with - IN TIME
```

Custom field usage - quickly decline mobile payments payments with newly created virtual cards

```
card.date_created - Greater than - 2020-11-01
wallet_token.platform - Is True
card.product_token - Is in - cz_card_virtual,pl_card_virtual
```
