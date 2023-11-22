```json
{
   "gpa":{
      "balances":{
         "CZK":{
            "currency_code":"CZK",
            "credit_balance":0.0,
            "ledger_balance":351.0,
            "pending_credits":0.0,
            "available_balance":0.0
         },
         "EUR":{
            "currency_code":"EUR",
            "credit_balance":0.0,
            "ledger_balance":0.0,
            "pending_credits":0.0,
            "available_balance":0.0
         }
      },
      "currency_code":"EUR",
      "credit_balance":0.0,
      "ledger_balance":0.0,
      "pending_credits":0.0,
      "available_balance":0.0
   },
   "pos":{
      "zip":"XBX 1120",
      "pin_present":false,
      "terminal_id":"00000001",
      "country_code":"470",
      "is_recurring":false,
      "card_presence":false,
      "is_installment":false,
      "pan_entry_mode":"OTHER",
      "pin_entry_mode":"FALSE",
      "terminal_location":"OFF_PREMISE_CARDHOLDER",
      "terminal_attendance":"UNATTENDED",
      "card_holder_presence":false,
      "purchase_amount_only":false,
      "partial_approval_capable":false,
      "card_data_input_capability":"KEY_ENTRY"
   },
   "card":{
      "metadata":{
         
      },
      "last_four":"1815"
   },
   "type":"original.credit.authorization",
   "fraud":{
      "network":{
         "transaction_risk_score":3,
         "transaction_risk_score_reason_code":"99",
         "transaction_risk_score_reason_description":"OTHERS"
      }
   },
   "state":"PENDING",
   "token":"08ce6fc8-5885-425d-8fd2-5b577ed2475f",
   "amount":2120.0,
   "network":"MASTERCARD",
   "acquirer":{
      "institution_id_code":"015554",
      "system_trace_audit_number":"125059",
      "retrieval_reference_number":"112285063423"
   },
   "card_token":"bf46fd94-c5af-4ce0-afd4-93c980a8926e",
   "subnetwork":"MASTERCARDDEBIT",
   "user_token":"238570",
   "created_time":"2023-11-20T20:23:20Z",
   "card_acceptor":{
      "mcc":"7995",
      "mid":"251001245000001",
      "url":"N/A",
      "city":"TA XBIEX",
      "name":"BETANO CZ",
      "phone":"Betano",
      "state":"MLT",
      "postal_code":"XBX 1120",
      "country_code":"MLT"
   },
   "currency_code":"CZK",
   "request_amount":2120.0,
   "original_credit":{
      "sender_name":"BETANO CZ",
      "funding_source":"DEPOSIT_ACCOUNT",
      "transaction_type":"online_gambling_payout",
      "fast_funds_enabled":false,
      "sender_account_type":"other"
   },
   "settlement_date":"2023-11-20T00:00:00Z",
   "gpa_order_unload":{
      "state":"PENDING",
      "token":"ee7ab3b9-6d39-4e31-b6d0-74f8a081c58f",
      "amount":2120.0,
      "funding":{
         "amount":2120.0,
         "source":{
            "name":"twisto_testing_pgfs",
            "type":"programgateway",
            "token":"**********pgfs",
            "active":true,
            "created_time":"2019-09-17T13:37:04Z",
            "is_default_account":false,
            "last_modified_time":"2019-09-17T13:37:04Z"
         }
      },
      "jit_funding":{
         "tags":"auth_method=1&declined_reason=3",
         "token":"6cbfaeb7-a287-484c-9374-2e7a490e23b9",
         "amount":2120.0,
         "method":"pgfs.original.credit.authorization",
         "user_token":"238570",
         "decline_reason":"TRANSACTION_NOT_PERMITTED",
         "acting_user_token":"238570"
      },
      "transaction_token":"6c111d58-4d5e-43de-bd7a-fddedd491078",
      "funding_source_token":"**********pgfs"
   },
   "acting_user_token":"238570",
   "card_product_token":"cz_card_black",
   "currency_conversion":{
      "network":{
         "conversion_rate":1.0,
         "original_amount":2120.0,
         "original_currency_code":"203"
      }
   },
   "issuer_payment_node":"fe6490cce8e8c7737a47db423bfb9831",
   "digital_wallet_token":{
      "state":"ACTIVE",
      "token":"88bff93e-fd45-4955-b673-151aa2d04f38",
      "device":{
         "name":"Lukas-IPhone",
         "type":"MOBILE_PHONE",
         "location":"+50.07/+14.35",
         "device_id":"04222883DD6780021133083866310410B695D7B3C53E787F",
         "ip_address":"89.177.134.202"
      },
      "card_token":"bf46fd94-c5af-4ce0-afd4-93c980a8926e",
      "created_time":"2021-12-08T17:37:10Z",
      "state_reason":"Token Update",
      "fulfillment_status":"PROVISIONED",
      "last_modified_time":"2023-10-09T05:53:01Z",
      "address_verification":{
         
      },
      "token_service_provider":{
         "token_pan":"516788______6421",
         "token_type":"DEVICE_SECURE_ELEMENT",
         "correlation_id":"D0002412633265",
         "pan_reference_id":"FAPLMC0000257305add4cdf430b54717b5fda8b30cdc1093",
         "token_expiration":"1026",
         "token_reference_id":"DAPLMC0000257305615a9e77d49d4f129398494a44381088",
         "token_requestor_id":"50110030273",
         "token_requestor_name":"APPLE_PAY"
      },
      "wallet_provider_profile":{
         "account":{
            "id":"0e57291ea351e903f851a392290c77b88fa9146fe11d7fc5a469fa10906e2b96",
            "score":"5"
         },
         "pan_source":"ON_FILE",
         "device_score":"3",
         "risk_assessment":{
            "score":"DECISION_GREEN",
            "version":"0001.00"
         }
      },
      "issuer_eligibility_decision":"0000"
   },
   "issuer_received_time":"2023-11-20T20:23:20.974Z",
   "network_reference_id":"MDSRX1Y421120",
   "transaction_metadata":{
      "payment_channel":"ECOMMERCE"
   },
   "user_transaction_time":"2023-11-20T20:23:20Z",
   "local_transaction_date":"2023-11-20T22:23:20Z",
   "acquirer_reference_data":"MDSRX1Y42"
}