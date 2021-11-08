# Verify transaction status

While making a transaction, a communication or technical issue can prevent your cash register from receiving a response. Without this response your store staff may be unable to verify whether the transaction has been processed, or its result. They may also attempt to cancel or refund the transaction, or risk a duplicate transaction.

Instead, your integration should request the transaction's status to verify whether the transaction is:

- Processed
- In progress
- Not found

 

If the transaction has been processed you also receive the original transaction response, indicating the result.

## Request transaction status

We recommend that your integration automatically requests the status of a transaction, any time it fails to receive a transaction response.
Payment requests time out after a while. If you do not receive a payment response (or you receive a response indicating a time-out) after 120 seconds (local integration) or 150 seconds (cloud integration), and the internet connection hasn't dropped, your integration should automatically request the transaction status.

To request the status of a transaction, your cash register should:

`MessageHeader`: The standard `SaleToPOIRequest.MessageHeader` object. This includes:

| **Parameter**     | **Required** | **Description**                                              |
| ----------------- | ------------ | ------------------------------------------------------------ |
| `ProtocolVersion` | Yes          | **3.0**                                                      |
| `MessageClass`    | Yes          | **Service**                                                  |
| `MessageCategory` | Yes          | **TransactionStatus**                                        |
| `MessageType`     | Yes          | **Request**                                                  |
| `SaleID`          | Yes          | Your unique ID for the cash register.                        |
| `ServiceID`       | Yes          | Your unique ID for this request, consisting of 1-10 alphanumeric characters. Must be unique within the last 48 hours. |
| `POIID`           | Yes          | Unique ID of the terminal that you want to route this request to. Format: *[device model]-[serial number]*. |

 

- `TransactionStatusRequest`: The request body with:
  - `ReceiptReprintFlag`: **true**
  - `DocumentQualifier`: Receipt data you want to receive in the response. Can be one or both of:
    - **CashierReceipt**: Cashier receipt, including signature data.
    - **CustomerReceipt**: Shopper receipt.
  - `MessageReference`: This object is optional. If you do not include it you receive the status of the most recent transaction made by the terminal that you route the transaction status request to.
    - `SaleID`: The `SaleID` of the cash register that made the original transaction.
    - `ServiceID`: The `ServiceID` of the original transaction.
    - `MessageCategory`: The original transaction type, either:
      - **Payment**: Payment request.
      - **Reversal**: Refund request.
      - **StoredValue**: Request to activate or load balance on a gift card.

The example below shows how you would request the status of a payment with the `ServiceID` **29235**.

```json
{
  "SaleToPOIRequest": {
    "MessageHeader": {
      "ProtocolVersion": "3.0",
      "MessageClass": "Service",
      "MessageCategory": "TransactionStatus",
      "MessageType": "Request",
      "SaleID": "POSSystemID12345",
      "ServiceID": "29245",
      "POIID": "V400m-324688179"
    },
    "TransactionStatusRequest": {
      "ReceiptReprintFlag": true,
      "DocumentQualifier": [
        "CashierReceipt",
        "CustomerReceipt"
      ],
      "MessageReference": {
        "SaleID": "POSSystemID12345",
        "ServiceID": "29235",
        "MessageCategory": "Payment"
      }
    }
  }
}
```

The response contains a `TransactionStatusResponse.Response.Result`, indicating whether the transaction has been processed:

- [Success ](https://docs.adyen.com/point-of-sale/verify-transaction-status#success)

  : Transaction has been processed. The original transaction response is also provided.

- `Failure`: Transaction has not been processed. The reason is indicated by the `ErrorCondition`:

  - [InProgress ](https://docs.adyen.com/point-of-sale/verify-transaction-status#transaction-in-progress)

    : Transaction is still being processed.

  - `NotFound` : We were not able to find the transaction.

An example of each result is provided below.

## Transaction processed

A `TransactionStatusResponse.Response.Result` of **Success** indicates that the transaction reached an end state: approved, cancelled, or declined.

To determine the result of the transaction, use the original transaction response, provided in the `RepeatedResponseMessageBody`. For example:

- `PaymentResponse.Response` has `Result` **Success**: The payment succeeded.
- `PaymentResponse.Response` has `Result` **Failure** and `ErrorCondition` **Aborted**: The payment was cancelled from the cash register.
- `PaymentResponse.Response` has `Result` **Failure** and `ErrorCondition` **Cancel**: The payment was cancelled from the terminal.

```json
{
    "SaleToPOIResponse": {
        "MessageHeader": {
            "MessageCategory": "TransactionStatus",
            "MessageClass": "Service",
            "MessageType": "Response",
            "POIID": "e280-324688179",
            "ProtocolVersion": "3.0",
            "SaleID": "POSSystemID12345",
            "ServiceID": "987"
        },
        "TransactionStatusResponse": {
            "RepeatedMessageResponse": {
                "MessageHeader": {
                    "MessageCategory": "Payment",
                    "MessageClass": "Service",
                    "MessageType": "Response",
                    "POIID": "e280-324688179",
                    "ProtocolVersion": "3.0",
                    "SaleID": "POSSystemID12345",
                    "ServiceID": "816"
                },
                "RepeatedResponseMessageBody": {
                    "PaymentResponse": {
                        "POIData": {
                            "POIReconciliationID": "1000",
                            "POITransactionID": {
                                "TimeStamp": "2021-01-21T09:47:32.000Z",
                                "TransactionID": "BV0q001611222452000.8515658977098900"
                            }
                        },
                        "PaymentReceipt": [...],
                        "PaymentResult": {
                            "AmountsResp": {
                                "AuthorizedAmount": 19.30,
                                "Currency": "EUR"
                            },
                            "OnlineFlag": true,
                            "PaymentAcquirerData": {...},
                            "PaymentInstrumentData": {...}
                        },
                        "Response": {
                            "AdditionalResponse": "...pspReference=8515658977098900...",
                            "Result": "Success"
                        },
                        "SaleData": {
                            "SaleTransactionID": {
                                "TimeStamp": "2021-01-21T09:47:21.092Z",
                                "TransactionID": "280"
                            }
                        }
                    }
                }
            },
            "Response": {
                "Result": "Success"
            }
        }
    }
}
```

```json
{
    "SaleToPOIResponse": {
        "MessageHeader": {
            "MessageCategory": "TransactionStatus",
            "MessageClass": "Service",
            "MessageType": "Response",
            "POIID": "V400m-324688179",
            "ProtocolVersion": "3.0",
            "SaleID": "POSSystemID12345",
            "ServiceID": "800"
        },
        "TransactionStatusResponse": {
            "MessageReference": {
                "MessageCategory": "Payment",
                "SaleID": "POSSystemID12345",
                "ServiceID": "172218"
            },
            "RepeatedMessageResponse": {
                "MessageHeader": {
                    "MessageCategory": "Payment",
                    "MessageClass": "Service",
                    "MessageType": "Response",
                    "POIID": "V400m-324688179",
                    "ProtocolVersion": "3.0",
                    "SaleID": "POSSystemID12345",
                    "ServiceID": "172218"
                },
                "RepeatedResponseMessageBody": {
                    "PaymentResponse": {
                        "POIData": {
                            "POIReconciliationID": "1000",
                            "POITransactionID": {
                                "TimeStamp": "2021-02-17T08:57:37.000Z",
                                "TransactionID": "8ha5001613552257008"
                            }
                        },
                        "PaymentResult": {
                            "PaymentAcquirerData": {
                                "AcquirerPOIID": "V400m-324688179",
                                "MerchantID": "YOUR_MERCHANT_ACCOUNT"
                            },
                            "PaymentInstrumentData": {
                                "CardData": {},
                                "PaymentInstrumentType": "Card"
                            }
                        },
                        "Response": {
                            "AdditionalResponse": "refusalReason=104%20Merchant%20cancelled%20tx&tid=46403161&transactionType=GOODS_SERVICES&backendGiftcardIndicator=false&posadditionalamounts.originalAmountValue=1553&posAmountGratuityValue=0&giftcardIndicator=false&batteryLevel=85%25&store=StoreOne&txtime=09%3a57%3a37&iso8601TxDate=2021-02-17T08%3a57%3a37.0000000%2b0000&posOriginalAmountValue=1553&txdate=17-02-2021&merchantReference=569&posadditionalamounts.originalAmountCurrency=EUR&posAuthAmountCurrency=EUR&message=104%20Merchant%20cancelled%20tx&posAmountCashbackValue=0&posAuthAmountValue=1553",
                            "ErrorCondition": "Aborted",
                            "Result": "Failure"
                        },
                        "SaleData": {
                            "SaleTransactionID": {
                                "TimeStamp": "2021-02-17T08:57:32.850Z",
                                "TransactionID": "569"
                            }
                        }
                    }
                }
            },
            "Response": {
                "Result": "Success"
            }
        }
    }
}
```

## Transaction in-progress

A `TransactionStatusResponse.Response.ErrorCondition` of **InProgress** indicates the transaction is still being processed. This is usually due to the terminal waiting for input from the shopper. For example, the shopper is entering their PIN, adding a tip, or selecting currency conversion.

When you receive an **InProgress** response, you can submit repeated transaction status requests in a loop until you receive a response that indicates the transaction reached an end state. There is no need to apply a polling delay, because the terminal will handle that for you.

The example response below indicates that this transaction is still in-progress.

 

**TransactionStatusResponse for an in-progress transaction**

```json
{
  "SaleToPOIResponse":{
    "MessageHeader":{
      "MessageType":"Response",
      "MessageCategory":"TransactionStatus",
      "MessageClass":"Service",
      "ProtocolVersion":"3.0",
      "POIID":"V400m-324688179",
      "SaleID":"POSSystemID12345",
      "ServiceID":"29235status"
    },
    "TransactionStatusResponse":{
      "Response":{
        "Result":"Failure",
        "ErrorCondition":"InProgress",
        "AdditionalResponse":"message=Uncompleted%20transaction"
      }
    }
  }
}
```

## Transaction not found

A `TransactionStatusResponse.Response.ErrorCondition` of **NotFound** indicates that we were not able to find the transaction with the `SaleID` and `ServiceID` you specified. The `AdditionalResponse` has **Message not found** and echoes the category of the transaction (such as Payment), the `SaleID`, and the `ServiceID` you specified in the request.

When the transaction is not found, this means that either:

- The `POIID`, `SaleID` or `ServiceID` you specified in the transaction status request are incorrect. Check that you provided the `POIID`, `SaleID`, and `ServiceID` from the *original* transaction in the `TransactionStatusRequest.MessageReference`.
- We did not receive your transaction request. This could be due to a dropped internet connection or an unexpected power loss. You can attempt the *original* transaction again.

The example response below indicates that this transaction was not found.

 

**TransactionStatusResponse for a transaction that's not found**

```json
{
  "SaleToPOIResponse":{
    "MessageHeader":{
      "POIID":"V400m-324688179",
      "SaleID":"POSSystemID12345",
      "ServiceID":"29235-status",
      "ProtocolVersion":"3.0",
      "MessageCategory":"TransactionStatus",
      "MessageType":"Response",
      "MessageClass":"Service"
    },
    "TransactionStatusResponse":{
      "Response":{
        "ErrorCondition":"NotFound",
        "Result":"Failure",
        "AdditionalResponse":"message=Message%20not%20found.%20Category%3dPayment%2c%20last%20such%20Request%20has%20SaleID%3dPOSSystemID12345%20ServiceID%3d29235",
      }
    }
  }
}
```

