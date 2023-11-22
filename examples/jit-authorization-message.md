### JIT Funding Message

```json
    {
        "type": "authorization",  # Used
        "state": "PENDING",  # Used
        "token": "96212fb6-4375-4698-979c-0a732cabf9fb",  # Used
        "user_token": "b70a9d1c-b5b5-4afd-b3ca-306be8d810d2",  # Used
        "acting_user_token": "b70a9d1c-b5b5-4afd-b3ca-306be8d810d2",
        "card_token": "c4d59f5d-1327-4893-88a1-9dec770de02c",  # Used
        "cardholder_authentication_data": {
            "acquirer_exemption": ["LOW_VALUE_PAYMENT"],  # Used
            "authentication_status": "THREEDS_REQUESTER_SCA_EXEMPTION",  # Used
            "electronic_commerce_indicator": "no_authentication",
            "verification_result": "verified",
            "verification_value_created_by": "issuer_acs"
        },
        "gpa": {
            "currency_code": "EUR",
            "ledger_balance": 0,
            "available_balance": 0,
            "credit_balance": 0,
            "pending_credits": 0,
            "balances": {
                "EUR": {
                    "currency_code": "EUR",
                    "ledger_balance": 0,
                    "available_balance": 0,
                    "credit_balance": 0,
                    "pending_credits": 0
                }
            }
        },
        "gpa_order": {
          "token": "a174a390-d1ec-46d4-bf9b-ecc931971673",
          "amount": 1.91,
          "transaction_token": "c9788ba1-5eda-45c3-a621-fecce9d4285b",
          "state": "PENDING",
          "funding": {
            "amount": 1.91,
            "source": {
              "type": "programgateway",
              "token": "**********pgfs",
              "active": true,
              "name": "twisto_testing_pgfs",
              "is_default_account": false,
              "created_time": "2019-09-17T13:37:04Z",
              "last_modified_time": "2019-09-17T13:37:04Z"
            }
          },
          "funding_source_token": "**********pgfs",
          "jit_funding": {
            "token": "c872a781-a063-4c00-a096-3e5ba0421544",
            "method": "pgfs.authorization",
            "user_token": "b70a9d1c-b5b5-4afd-b3ca-306be8d810d2",
            "acting_user_token": "b70a9d1c-b5b5-4afd-b3ca-306be8d810d2",
            "amount": 1.91,
            "address_verification": {
              "request": {
                "street_address": "27   ",
                "postal_code": "111      "
              },
              "issuer": {
                "on_file": {
                  "street_address": "Sokolovská 47/73",
                  "postal_code": ""
                },
                "response": {
                  "code": "0101",
                  "memo": "Address and zip code does not match"
                }
              }
            }
          },
          "user_token": "b70a9d1c-b5b5-4afd-b3ca-306be8d810d2",
          "currency_code": "PLN"
        },
        "created_time": "2019-09-18T15:14:04Z",  # Used
        "user_transaction_time": "2019-09-18T15:14:04Z",  # Used
        "settlement_date": "2019-09-18T00:00:00Z",
        "request_amount": 1.91,
        "amount": 1.91,  # Used
        "currency_conversion": {  # Used
            "network": {  # Used
              "original_amount": 0.39,  # Used
              "conversion_rate": 4.894582,  # Used
              "original_currency_code": "826"  # Used
            }
        },
        "fraud": {
            "network": {"account_risk_score": 7, "transaction_risk_score": 97},
            "issuer_processor": {
                "score": "8",
                "risk_level": "LOW",
                "rule_violations": [],
                "recommended_action": "APPROVE"
            }
        },
        "currency_code": "PLN",
        "network": "MASTERCARD",
        "subnetwork": "MASTERCARDDEBIT",
        "acquirer_fee_amount": 0,
        "acquirer": {
            "institution_id_code": "011319",  # Used
            "retrieval_reference_number": "091800003795",
            "system_trace_audit_number": "444039"
        },
        "user": {"metadata": {}},
        "card": {"last_four": "6491", "metadata": {}},
        "issuer_received_time": "2019-09-18T15:14:04.897Z",
        "issuer_payment_node": "fe6490cce8e8c7737a47db423bfb9831",
        "card_acceptor": {
            "mid": "009772089",
            "mcc": "7994",
            "name": "STEAMGAMES.COM",
            "city": "425-952-2985",
            "state": "GBR",
            "postal_code": "SW19 2RR",
            "country_code": "GBR"
        },
        "pos": {  # Used
            "pan_entry_mode": "OTHER",  # Used
            "pin_entry_mode": "FALSE",  # Used
            "terminal_id": "80222786",  # Used
            "terminal_attendance": "UNATTENDED",  # Used
            "terminal_location": "OFF_PREMISE_CARDHOLDER",
            "card_holder_presence": false,  # Used
            "card_presence": false,  # Used
            "card_data_input_capability": "KEY_ENTRY",  # Used
            "country_code": "826",
            "zip": "SW19 2RR  ",
            "partial_approval_capable": false,
            "purchase_amount_only": false,
            "is_recurring": false  # Used
        },
        "transaction_metadata": {  # Used
            "is_recurring": false,  # Used
            "payment_channel": "ECOMMERCE",  # Used
            "moto_indicator": null  # Used
        }
    }
