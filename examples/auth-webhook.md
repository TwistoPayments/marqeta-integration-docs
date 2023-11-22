### Authorization transaction webhook body
```json
    {
        "transactions": [
            {
                "type": "authorization",
                "state": "PENDING",
                "identifier": "96",
                "token": "96",
                "user_token": "user_1",
                "acting_user_token": "user_1",
                "card_token": "95f9a54d-991c-4568-97e1-c2fb68c20387",
                "gpa": {
                    "currency_code": "EUR",
                    "ledger_balance": 40,
                    "available_balance": 0,
                    "credit_balance": 0,
                    "pending_credits": 0,
                    "impacted_amount": -10,
                    "balances": {
                        "EUR": {
                            "currency_code": "EUR",
                            "ledger_balance": 40,
                            "available_balance": 0,
                            "credit_balance": 0,
                            "pending_credits": 0,
                            "impacted_amount": -10
                        }
                    }
                },
                "gpa_order": {
                    "token": "e35c4186-7cad-4846-bb5f-01356c61a733",
                    "amount": 10,
                    "created_time": "2019-04-08T12:17:13Z",
                    "last_modified_time": "2019-04-08T12:17:13Z",
                    "transaction_token": "97",
                    "state": "PENDING",
                    "response": {
                        "code": "0000",
                        "memo": "Approved or completed successfully"
                    },
                    "funding": {
                        "amount": 10,
                        "source": {
                            "type": "programgateway",
                            "token": "**********ay_1",
                            "active": true,
                            "name": "test_gateway_1",
                            "is_default_account": false,
                            "created_time": "2019-03-26T11:27:19Z",
                            "last_modified_time": "2019-03-26T11:27:19Z"
                        },
                        "gateway_log": {
                            "order_number": "96",
                            "transaction_id": "7b71d4e7-d325-4249-81a6-73305857691b",
                            "message": "Approved or completed successfully",
                            "duration": 529,
                            "timed_out": false,
                            "response": {
                                "code": "200",
                                "data": {
                                    "jit_funding": {
                                        "token": "7b71d4e7-d325-4249-81a6-73305857691b",
                                        "method": "pgfs.authorization",
                                        "user_token": "user_1",
                                        "acting_user_token": "user_1",
                                        "amount": 10
                                    }
                                }
                            }
                        }
                    },
                    "funding_source_token": "**********ay_1",
                    "jit_funding": {
                        "token": "7b71d4e7-d325-4249-81a6-73305857691b",
                        "method": "pgfs.authorization",
                        "user_token": "user_1",
                        "acting_user_token": "user_1",
                        "amount": 10
                    },
                    "user_token": "user_1",
                    "currency_code": "EUR"
                },
                "duration": 743,
                "created_time": "2019-04-08T12:17:12Z",
                "user_transaction_time": "2019-04-08T12:17:12Z",
                "settlement_date": "2019-04-08T00:00:00Z",
                "request_amount": 10,
                "amount": 10,
                "currency_code": "EUR",
                "approval_code": "534165",
                "response": {
                    "code": "0000",
                    "memo": "Approved or completed successfully"
                },
                "network": "DISCOVER",
                "acquirer_fee_amount": 0,
                "acquirer": {
                    "system_trace_audit_number": "282052"
                },
                "user": {
                    "metadata": {
                        "key1": "value1",
                        "key2": "value2"
                    }
                },
                "card": {
                    "metadata": {}
                },
                "issuer_received_time": "2019-04-08T12:17:12.948Z",
                "issuer_payment_node": "f8205a67b12b90d695b15704a64c074b",
                "card_acceptor": {
                    "mid": "123456890",
                    "mcc": "6411",
                    "network_mid": "123456890",
                    "mcc_groups": [
                        "NONE"
                    ],
                    "name": "Marqeta Storefront",
                    "address": "330 Central Ave. St.",
                    "city": "St. Petersburg",
                    "state": "CA",
                    "postal_code": "33705",
                    "country": "USA",
                    "poi": {
                        "partial_approval_capable": "1"
                    }
                },
                "is_recurring": false
            }
        ]
    }
