### Authorization (real world example from Marqeta)

    {
        "acquirer": {
            "institution_id_code": "011610",
            "retrieval_reference_number": "006296981268",
            "system_trace_audit_number": "926527"
        },
        "acquirer_fee_amount": 0,
        "acquirer_reference_data": "MDSJJT0FG",
        "acting_user_token": "e4fdcf46-1ff6-4127-84cb-212e5b22e068",
        "amount": 15.3,
        "card": {
            "last_four": "9554",
            "metadata": {}
        },
        "card_acceptor": {
            "city": "LEGNICA",
            "country_code": "POL",
            "mcc": "5499",
            "mid": "009279000000001",
            "name": "SKLEP ZAGLOBA",
            "postal_code": "59220",
            "state": "POL"
        },
        "card_security_code_verification": {
            "response": {
                "code": "0000",
                "memo": "Card security code match"
            },
            "type": "ICVV"
        },
        "card_token": "ee1f0b7b-0ad4-48ef-8ec2-a938bd75ff96",
        "cardholder_authentication_data": {
            "acquirer_exemption": [
                "TRANSACTION_RISK_ANALYSIS"
            ]
        },
        "created_time": "2022-01-25T21:07:05Z",
        "currency_code": "PLN",
        "currency_conversion": {
            "network": {
                "conversion_rate": 1.0,
                "original_amount": 15.3,
                "original_currency_code": "985"
            }
        },
        "duration": 719,
        "gpa": {
            "available_balance": 0.0,
            "balances": {
                "CZK": {
                    "available_balance": 0.0,
                    "credit_balance": 0.0,
                    "currency_code": "CZK",
                    "ledger_balance": 0.0,
                    "pending_credits": 0.0
                },
                "EUR": {
                    "available_balance": 0.0,
                    "credit_balance": 0.0,
                    "currency_code": "EUR",
                    "ledger_balance": 0.0,
                    "pending_credits": 0.0
                },
                "PLN": {
                    "available_balance": 0.0,
                    "credit_balance": 0.0,
                    "currency_code": "PLN",
                    "ledger_balance": 0.0,
                    "pending_credits": 0.0
                },
                "RON": {
                    "available_balance": 0.0,
                    "credit_balance": 0.0,
                    "currency_code": "RON",
                    "ledger_balance": 0.0,
                    "pending_credits": 0.0
                }
            },
            "credit_balance": 0.0,
            "currency_code": "CZK",
            "ledger_balance": 0.0,
            "pending_credits": 0.0
        },
        "gpa_order": {
            "amount": 15.3,
            "created_time": "2022-01-25T21:07:05Z",
            "currency_code": "PLN",
            "funding": {
                "amount": 15.3,
                "gateway_log": {
                    "duration": 574,
                    "message": "Declined by gateway.",
                    "order_number": "2cf27ca4-7bc9-4abc-bc7f-3bb9e71df079",
                    "response": {
                        "code": "402",
                        "data": {
                            "jit_funding": {
                                "acting_user_token": "e4fdcf46-1ff6-4127-84cb-212e5b22e068",
                                "amount": 15.3,
                                "method": "pgfs.authorization",
                                "tags": "auth_method=2&declined_reason=8",
                                "token": "27a944c9-3c73-4c10-ad1e-4bfbf919749f",
                                "user_token": "e4fdcf46-1ff6-4127-84cb-212e5b22e068"
                            }
                        }
                    },
                    "timed_out": false,
                    "transaction_id": "27a944c9-3c73-4c10-ad1e-4bfbf919749f"
                },
                "source": {
                    "active": true,
                    "created_time": "2019-09-17T13:37:04Z",
                    "is_default_account": false,
                    "last_modified_time": "2019-09-17T13:37:04Z",
                    "name": "twisto_testing_pgfs",
                    "token": "**********pgfs",
                    "type": "programgateway"
                }
            },
            "funding_source_token": "**********pgfs",
            "jit_funding": {
                "acting_user_token": "e4fdcf46-1ff6-4127-84cb-212e5b22e068",
                "amount": 15.3,
                "method": "pgfs.authorization",
                "token": "27a944c9-3c73-4c10-ad1e-4bfbf919749f",
                "user_token": "e4fdcf46-1ff6-4127-84cb-212e5b22e068"
            },
            "last_modified_time": "2022-01-25T21:07:05Z",
            "response": {
                "code": "1842",
                "memo": "Account load failed"
            },
            "state": "DECLINED",
            "tags": "auth_method=2&declined_reason=8",
            "token": "92b7dd44-8e06-44bc-8ed2-068f058920a2",
            "transaction_token": "2e39ba23-dfec-46bd-8494-7297e5b7706d",
            "user_token": "e4fdcf46-1ff6-4127-84cb-212e5b22e068"
        },
        "identifier": "45648488",
        "issuer_interchange_amount": 0,
        "issuer_payment_node": "6ea4cb2554d7a34bf2d2c6e512d74045",
        "issuer_received_time": "2022-01-25T21:07:05.265Z",
        "network": "MASTERCARD",
        "network_metadata": {
            "product_id": "DEBIT_MASTERCARD"
        },
        "network_reference_id": "MDSJJT0FG0125",
        "pos": {
            "card_data_input_capability": "CHIP_CONTACTLESS",
            "card_holder_presence": true,
            "card_presence": true,
            "country_code": "616",
            "is_installment": false,
            "is_recurring": false,
            "pan_entry_mode": "CHIP_CONTACTLESS",
            "partial_approval_capable": false,
            "pin_entry_mode": "TRUE",
            "pin_present": false,
            "purchase_amount_only": false,
            "terminal_attendance": "ATTENDED",
            "terminal_id": "02122125",
            "terminal_location": "ON_PREMISE",
            "zip": "59220     "
        },
        "request_amount": 15.3,
        "response": {
            "code": "1016",
            "memo": "Not sufficient funds"
        },
        "settlement_date": "2022-01-25T00:00:00Z",
        "state": "DECLINED",
        "subnetwork": "MASTERCARDDEBIT",
        "token": "2cf27ca4-7bc9-4abc-bc7f-3bb9e71df079",
        "transaction_metadata": {
            "payment_channel": "OTHER"
        },
        "type": "authorization",
        "user": {
            "metadata": {
                "customer_id": "342714",
                "email": "krystianw819@gmail.com",
                "site": "2"
            }
        },
        "user_token": "e4fdcf46-1ff6-4127-84cb-212e5b22e068",
        "user_transaction_time": "2022-01-25T21:07:05Z"
    }
