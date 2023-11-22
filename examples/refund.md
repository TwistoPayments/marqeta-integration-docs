### Refund
```json
    {
        "transaction": {
            "type": "refund",
            "state": "COMPLETION",
            "identifier": "122",
            "token": "122",
            "user_token": "e67a0dc4-0931-48f3-a05b-c21e34251290",
            "acting_user_token": "e67a0dc4-0931-48f3-a05b-c21e34251290",
            "card_token": "d839d66e-8334-4afb-9842-b052edcb6527",
            "gpa": {
                "currency_code": "EUR",
                "ledger_balance": 1.00,
                "available_balance": 0.00,
                "credit_balance": 0.00,
                "pending_credits": 0.00,
                "impacted_amount": 1.00,
                "balances": {
                    "EUR": {
                        "currency_code": "EUR",
                        "ledger_balance": 1.00,
                        "available_balance": 0.00,
                        "credit_balance": 0.00,
                        "pending_credits": 0.00,
                        "impacted_amount": 1.00
                    }
                }
            },
            "duration": 140,
            "created_time": "2019-05-07T13:05:25Z",
            "user_transaction_time": "2019-05-07T13:05:25Z",
            "settlement_date": "2019-05-07T00:00:00Z",
            "request_amount": 1.00,
            "amount": 1.00,
            "currency_code": "EUR",
            "approval_code": "528119",
            "response": {
                "code": "0000",
                "memo": "Approved or completed successfully"
            },
            "gpa_order_unload": {
                "token": "caa5979f-65b9-4256-8c18-67ec36647ecd",
                "amount": 1.00,
                "created_time": "2019-05-07T13:05:25Z",
                "last_modified_time": "2019-05-07T13:05:25Z",
                "transaction_token": "123",
                "state": "COMPLETION",
                "response": {
                    "code": "0000",
                    "memo": "Approved or completed successfully"
                },
                "funding": {
                    "amount": 1.00,
                    "source": {
                        "type": "programgateway",
                        "token": "**********ay_1",
                        "active": true,
                        "name": "test_gateway_1",
                        "is_default_account": false,
                        "created_time": "2019-03-26T11:27:19Z",
                        "last_modified_time": "2019-03-26T11:27:19Z"
                    }
                },
                "funding_source_token": "**********ay_1",
                "jit_funding": {
                    "token": "0c473a2c-fa6b-42e0-b94d-d4fc26ff5aca",
                    "method": "pgfs.refund",
                    "user_token": "e67a0dc4-0931-48f3-a05b-c21e34251290",
                    "acting_user_token": "e67a0dc4-0931-48f3-a05b-c21e34251290",
                    "amount": 1.00
                }
            },
            "network": "DISCOVER",
            "acquirer_fee_amount": 0,
            "acquirer": {
                "institution_id_code": "000000",
                "system_trace_audit_number": "000609"
            },
            "user": {
                "metadata": {}
            },
            "card": {
                "metadata": {}
            },
            "issuer_received_time": "2019-05-07T13:05:25.142Z",
            "issuer_payment_node": "f8205a67b12b90d695b15704a64c074b",
            "card_acceptor": {
                "mid": "1",
                "mcc": "6411",
                "network_mid": "1",
                "name": "Marqeta Storefront",
                "address": "330 Central Ave. St.",
                "city": "St. Petersburg",
                "state": "CA",
                "postal_code": "33705",
                "country": "USA",
                "poi": {
                    "partial_approval_capable": "0"
                }
            },
            "is_recurring": false
        },
        "raw_iso8583": {
            "0": "2210",
            "2": "1111110868701716",
            "3": "900000",
            "4": 1.00,
            "7": "0507130525",
            "11": "000000000609",
            "12": "20190507130525",
            "13": "190507",
            "14": "2305",
            "15": "20190507",
            "17": "0507",
            "21": "300923871791",
            "25": "9000",
            "26": "6411",
            "32": "000000",
            "37": "1443",
            "38": "528119",
            "39": "0000",
            "42": "1",
            "43": {
                "2": "Marqeta Storefront",
                "3": "330 Central Ave. St.",
                "4": "St. Petersburg",
                "5": "CA",
                "6": "33705",
                "7": "840"
            },
            "44": {
                "1": "Approved or completed successfully",
                "3": "00",
                "4": "Approved or completed successfully"
            },
            "54": "00029782C00000000000000019782C000000000100",
            "56": {
                "7": "120"
            },
            "63": "DISCOVER",
            "112": {
                "101": "0.00",
                "102": "1.00",
                "103": "978"
            },
            "113": {
                "2": "106",
                "29": "Y",
                "35": "API"
            },
            "180": "twst"
        }
    }
