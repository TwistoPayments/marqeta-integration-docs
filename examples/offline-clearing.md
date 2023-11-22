### Offline clearing transaction

Offline clearing transactions don't have a preceding authorization so preceding_related_transaction_token is either null or not present at all.

    {
        "transaction": {
            "type": "authorization.clearing",
            "state": "COMPLETION",
            "token": "9",
            "user_token": "bluebird_token",
            "acting_user_token": "bluebird_token",
            "card_token": "db389239-1ba4-4ffd-a1bd-5e0fd3ad46a9",
            "gpa": {
                "currency_code": "USD",
                "ledger_balance": 200.00,
                "available_balance": 0.00,
                "credit_balance": 0.00,
                "pending_credits": 0.00,
                "impacted_amount": -200.00,
                "balances": {
                    "USD": {
                        "currency_code": "USD",
                        "ledger_balance": 200.00,
                        "available_balance": 0.00,
                        "credit_balance": 0.00,
                        "pending_credits": 0.00,
                        "impacted_amount": -200.00
                    }
                }
            },
            "gpa_order": {
                "token": "88732f84-9141-4fd9-86ea-43ceb4f592ce",
                "amount": 200.00,
                "created_time": "2019-03-25T12:41:24Z",
                "last_modified_time": "2019-03-25T12:43:29Z",
                "transaction_token": "10",
                "state": "COMPLETION",
                "response": {
                    "code": "0000",
                    "memo": "Approved or completed successfully"
                },
                "funding": {
                    "amount": 200.00,
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
            "duration": 190,
            "created_time": "2019-03-25T12:43:29Z",
            "user_transaction_time": "2019-03-25T12:41:24Z",
            "settlement_date": "2019-03-25T00:00:00Z",
            "request_amount": 200.00,
            "amount": 200.00,
            "currency_code": "USD",
            "approval_code": "324398",
            "response": {
                "code": "0000",
                "memo": "Approved or completed successfully"
            },
            "network": "DISCOVER",
            "acquirer_fee_amount": 0,
            "acquirer": {
                "institution_id_code": "000000",
                "system_trace_audit_number": "000387"
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
            "4": 200.00,
            "7": "0325124329",
            "11": "000000000387",
            "12": "20190325124329",
            "13": "190325",
            "14": "2303",
            "15": "20190325",
            "17": "0325",
            "21": "056686431597",
            "25": "9000",
            "26": "6411",
            "32": "000000",
            "37": "1364",
            "38": "324398",
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
                "7": "7"
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
