### Authorization + partial reversal + clearing

##### 1) authorization

    {
        "transaction": {
            "type": "authorization",
            "state": "PENDING",
            "token": "17",
            "user_token": "bluebird_token",
            "acting_user_token": "bluebird_token",
            "card_token": "db389239-1ba4-4ffd-a1bd-5e0fd3ad46a9",
            "gpa": {
                "currency_code": "USD",
                "ledger_balance": 700.00,
                "available_balance": 0.00,
                "credit_balance": 0.00,
                "pending_credits": 0.00,
                "impacted_amount": -500.00,
                "balances": {
                    "USD": {
                        "currency_code": "USD",
                        "ledger_balance": 700.00,
                        "available_balance": 0.00,
                        "credit_balance": 0.00,
                        "pending_credits": 0.00,
                        "impacted_amount": -500.00
                    }
                }
            },
            "gpa_order": {
                "token": "f1df9218-933d-4d0a-8068-eb4f1c90ff07",
                "amount": 500.00,
                "created_time": "2019-03-25T15:30:52Z",
                "last_modified_time": "2019-03-25T15:30:52Z",
                "transaction_token": "18",
                "state": "PENDING",
                "response": {
                    "code": "0000",
                    "memo": "Approved or completed successfully"
                },
                "funding": {
                    "amount": 500.00,
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
            "duration": 108,
            "created_time": "2019-03-25T15:30:52Z",
            "user_transaction_time": "2019-03-25T15:30:52Z",
            "settlement_date": "2019-03-25T00:00:00Z",
            "request_amount": 500.00,
            "amount": 500.00,
            "currency_code": "USD",
            "approval_code": "326991",
            "response": {
                "code": "0000",
                "memo": "Approved or completed successfully"
            },
            "network": "DISCOVER",
            "acquirer_fee_amount": 0,
            "acquirer": {
                "system_trace_audit_number": "463163"
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
            "4": 500.00,
            "7": "0325153052",
            "11": "000004463163",
            "12": "20190325153052",
            "13": "190325",
            "14": "2303",
            "15": "20190325",
            "17": "0325",
            "21": "057182846687",
            "22": "10000000020000000100000001000000",
            "24": "181",
            "26": "6411",
            "37": "1427",
            "38": "326991",
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
            "54": "00028402C00000000000000018402C000000070000",
            "63": "DISCOVER",
            "112": {
                "22": "0200010000700",
                "101": "0.00",
                "102": "700.00",
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
            "state": "CLEARED",
            "token": "19",
            "user_token": "bluebird_token",
            "acting_user_token": "bluebird_token",
            "card_token": "db389239-1ba4-4ffd-a1bd-5e0fd3ad46a9",
            "preceding_related_transaction_token": "17",
            "gpa": {
                "currency_code": "USD",
                "ledger_balance": 200.00,
                "available_balance": 0.00,
                "credit_balance": 0.00,
                "pending_credits": 0.00,
                "impacted_amount": 500.00,
                "balances": {
                    "USD": {
                        "currency_code": "USD",
                        "ledger_balance": 200.00,
                        "available_balance": 0.00,
                        "credit_balance": 0.00,
                        "pending_credits": 0.00,
                        "impacted_amount": 500.00
                    }
                }
            },
            "gpa_order": {
                "token": "f1df9218-933d-4d0a-8068-eb4f1c90ff07",
                "amount": 500.00,
                "created_time": "2019-03-25T15:30:52Z",
                "last_modified_time": "2019-03-25T15:33:48Z",
                "transaction_token": "20",
                "state": "REVERSED",
                "response": {
                    "code": "0000",
                    "memo": "Approved or completed successfully"
                },
                "funding": {
                    "amount": 500.00,
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
            "duration": 101,
            "created_time": "2019-03-25T15:33:47Z",
            "user_transaction_time": "2019-03-25T15:30:52Z",
            "request_amount": 500.00,
            "amount": 500.00,
            "currency_code": "USD",
            "approval_code": "326991",
            "response": {
                "code": "0000",
                "memo": "Approved or completed successfully"
            },
            "network": "DISCOVER",
            "acquirer_fee_amount": 0,
            "acquirer": {
                "system_trace_audit_number": "463163"
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
            "4": 500.00,
            "7": "0325153347",
            "11": "000004463163",
            "12": "20190325153347",
            "13": "0325",
            "21": "057182846687",
            "25": "0000",
            "26": "6411",
            "37": "1428",
            "38": "326991",
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
                "1": "2100",
                "2": "000004463163",
                "3": "20190325153347",
                "7": "17"
            },
            "63": "DISCOVER",
            "112": {
                "101": "0.00",
                "102": "200.00",
                "103": "840"
            },
            "113": {
                "2": "106",
                "35": "API"
            },
            "180": "twst"
        }
    }
