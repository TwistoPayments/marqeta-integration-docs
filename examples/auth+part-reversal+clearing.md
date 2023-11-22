### Authorization + reversal + clearing

Clearing and reverse transactions are related to authorization via `transaction.preceding_related_transaction_token = transaction.token` .

##### 1)authorization

    {
        "transaction": {
            "type": "authorization",
            "state": "PENDING",
            "token": "11",
            "user_token": "bluebird_token",
            "acting_user_token": "bluebird_token",
            "card_token": "db389239-1ba4-4ffd-a1bd-5e0fd3ad46a9",
            "gpa": {
                "currency_code": "USD",
                "ledger_balance": 450.00,
                "available_balance": 0.00,
                "credit_balance": 0.00,
                "pending_credits": 0.00,
                "impacted_amount": -250.00,
                "balances": {
                    "USD": {
                        "currency_code": "USD",
                        "ledger_balance": 450.00,
                        "available_balance": 0.00,
                        "credit_balance": 0.00,
                        "pending_credits": 0.00,
                        "impacted_amount": -250.00
                    }
                }
            },
            "gpa_order": {
                "token": "3927a3b4-833e-4dcd-b6df-dd019c9ef0aa",
                "amount": 250.00,
                "created_time": "2019-03-25T14:03:27Z",
                "last_modified_time": "2019-03-25T14:03:27Z",
                "transaction_token": "12",
                "state": "PENDING",
                "response": {
                    "code": "0000",
                    "memo": "Approved or completed successfully"
                },
                "funding": {
                    "amount": 250.00,
                    "source": {
                        "type": "program",
                        "token": "**********4624",
                        "active": true,
                        "name": "Twisto Program Funding Source",
                        "is_default_account": false,
                        "created_time": "2019-03-20T21:02:07Z",
                        "last_modified_time": "2019-03-20T21:02:07Z"
                    }
                },
                "funding_source_token": "**********4624",
                "user_token": "bluebird_token",
                "currency_code": "USD"
            },
            "duration": 196,
            "created_time": "2019-03-25T14:03:26Z",
            "user_transaction_time": "2019-03-25T14:03:26Z",
            "settlement_date": "2019-03-25T00:00:00Z",
            "request_amount": 250.00,
            "amount": 250.00,
            "currency_code": "USD",
            "approval_code": "070704",
            "response": {
                "code": "0000",
                "memo": "Approved or completed successfully"
            },
            "network": "DISCOVER",
            "acquirer_fee_amount": 0,
            "acquirer": {
                "system_trace_audit_number": "933944"
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
            "card_acceptor": {
                "mid": "1",
                "mcc": "6411",
                "network_mid": "1",
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
        },
        "raw_iso8583": {
            "0": "2110",
            "2": "1111118333398836",
            "3": "000000",
            "4": 250.00,
            "7": "0325140326",
            "11": "000003933944",
            "12": "20190325140326",
            "13": "190325",
            "14": "2303",
            "15": "20190325",
            "17": "0325",
            "21": "181988675328",
            "22": "10000000020000000100000001000000",
            "24": "181",
            "26": "6411",
            "37": "1367",
            "38": "070704",
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
            "54": "00028402C00000000000000018402C000000045000",
            "63": "DISCOVER",
            "112": {
                "22": "0200010000700",
                "101": "0.00",
                "102": "450.00",
                "103": "840"
            },
            "113": {
                "2": "106",
                "29": "Y",
                "34": "Y",
                "35": "API"
            },
            "180": "twst"
        }
    }

##### 2) reversal

    {
        "transaction": {
            "type": "authorization.reversal",
            "state": "PENDING",
            "token": "13",
            "user_token": "bluebird_token",
            "acting_user_token": "bluebird_token",
            "card_token": "db389239-1ba4-4ffd-a1bd-5e0fd3ad46a9",
            "preceding_related_transaction_token": "11",
            "gpa": {
                "currency_code": "USD",
                "ledger_balance": 350.00,
                "available_balance": 0.00,
                "credit_balance": 0.00,
                "pending_credits": 0.00,
                "impacted_amount": 100.00,
                "balances": {
                    "USD": {
                        "currency_code": "USD",
                        "ledger_balance": 350.00,
                        "available_balance": 0.00,
                        "credit_balance": 0.00,
                        "pending_credits": 0.00,
                        "impacted_amount": 100.00
                    }
                }
            },
            "gpa_order": {
                "token": "3927a3b4-833e-4dcd-b6df-dd019c9ef0aa",
                "amount": 100.00,
                "created_time": "2019-03-25T14:03:27Z",
                "last_modified_time": "2019-03-25T14:06:12Z",
                "transaction_token": "14",
                "state": "PENDING",
                "response": {
                    "code": "0000",
                    "memo": "Approved or completed successfully"
                },
                "funding": {
                    "amount": 100.00,
                    "source": {
                        "type": "program",
                        "token": "**********4624",
                        "active": true,
                        "name": "Twisto Program Funding Source",
                        "is_default_account": false,
                        "created_time": "2019-03-20T21:02:07Z",
                        "last_modified_time": "2019-03-20T21:02:07Z"
                    }
                },
                "funding_source_token": "**********4624",
                "user_token": "bluebird_token",
                "currency_code": "USD"
            },
            "duration": 117,
            "created_time": "2019-03-25T14:06:12Z",
            "user_transaction_time": "2019-03-25T14:03:26Z",
            "request_amount": 250.00,
            "amount": 100.00,
            "currency_code": "USD",
            "approval_code": "070704",
            "response": {
                "code": "0000",
                "memo": "Approved or completed successfully"
            },
            "network": "DISCOVER",
            "acquirer_fee_amount": 0,
            "acquirer": {
                "system_trace_audit_number": "933944"
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
            "0": "2430",
            "2": "1111118333398836",
            "3": "000000",
            "4": 250.00,
            "7": "0325140612",
            "11": "000003933944",
            "12": "20190325140612",
            "13": "0325",
            "21": "181988675328",
            "25": "0000",
            "26": "6411",
            "37": "1417",
            "38": "070704",
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
            "54": "00028402C00000000000000018402C000000035000",
            "56": {
                "1": "2100",
                "2": "000003933944",
                "3": "20190325140612",
                "7": "11"
            },
            "63": "DISCOVER",
            "95": {
                "1": 150.00
            },
            "112": {
                "101": "0.00",
                "102": "350.00",
                "103": "840"
            },
            "113": {
                "2": "106",
                "35": "API"
            },
            "180": "twst"
        }
    }

##### 3) clearing

    {
        "transaction": {
            "type": "authorization.clearing",
            "state": "COMPLETION",
            "token": "15",
            "user_token": "bluebird_token",
            "acting_user_token": "bluebird_token",
            "card_token": "db389239-1ba4-4ffd-a1bd-5e0fd3ad46a9",
            "preceding_related_transaction_token": "11",
            "gpa": {
                "currency_code": "USD",
                "ledger_balance": 200.00,
                "available_balance": 0.00,
                "credit_balance": 0.00,
                "pending_credits": 0.00,
                "impacted_amount": -150.00,
                "balances": {
                    "USD": {
                        "currency_code": "USD",
                        "ledger_balance": 200.00,
                        "available_balance": 0.00,
                        "credit_balance": 0.00,
                        "pending_credits": 0.00,
                        "impacted_amount": -150.00
                    }
                }
            },
            "gpa_order": {
                "token": "3927a3b4-833e-4dcd-b6df-dd019c9ef0aa",
                "amount": 150.00,
                "created_time": "2019-03-25T14:03:27Z",
                "last_modified_time": "2019-03-25T14:07:50Z",
                "transaction_token": "16",
                "state": "COMPLETION",
                "response": {
                    "code": "0000",
                    "memo": "Approved or completed successfully"
                },
                "funding": {
                    "amount": 150.00,
                    "source": {
                        "type": "program",
                        "token": "**********4624",
                        "active": true,
                        "name": "Twisto Program Funding Source",
                        "is_default_account": false,
                        "created_time": "2019-03-20T21:02:07Z",
                        "last_modified_time": "2019-03-20T21:02:07Z"
                    }
                },
                "funding_source_token": "**********4624",
                "user_token": "bluebird_token",
                "currency_code": "USD"
            },
            "duration": 117,
            "created_time": "2019-03-25T14:07:50Z",
            "user_transaction_time": "2019-03-25T14:03:26Z",
            "settlement_date": "2019-03-25T00:00:00Z",
            "request_amount": 150.00,
            "amount": 150.00,
            "currency_code": "USD",
            "approval_code": "070704",
            "response": {
                "code": "0000",
                "memo": "Approved or completed successfully"
            },
            "network": "DISCOVER",
            "acquirer_fee_amount": 0,
            "acquirer": {
                "institution_id_code": "000000",
                "system_trace_audit_number": "000347"
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
            "2": "1111118333398836",
            "3": "900000",
            "4": 150.00,
            "7": "0325140750",
            "11": "000000000347",
            "12": "20190325140750",
            "13": "190325",
            "14": "2303",
            "15": "20190325",
            "17": "0325",
            "21": "181988675328",
            "25": "9000",
            "26": "6411",
            "32": "000000",
            "37": "1419",
            "38": "070704",
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
            "54": "00028402C00000000000000018402C000000020000",
            "56": {
                "7": "11"
            },
            "63": "DISCOVER",
            "112": {
                "101": "0.00",
                "102": "200.00",
                "103": "840"
            },
            "113": {
                "2": "106",
                "29": "Y",
                "35": "API"
            },
            "180": "twst"
        }
    }
