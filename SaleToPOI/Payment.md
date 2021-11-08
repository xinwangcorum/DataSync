# Payment Request

## Introduction

To initiate a payment, you make a request from your cash register. This routes the message to the terminal (via a payment gateway), which prompts the shopper to present their card and verify the payment. The terminal then sends the payment to the payment gateway for processing.

Once processed, your integration receives the result of the payment.

## Scope

Scenario 1: Make a payment

 

## Details

### Scenario 1: Make a payment request

The first step in making a card payment is to initiate it, with an API  request from your cash register. Once you make this request, the  terminal will prompt the shopper to present their card by swiping,  inserting, or tapping it on the terminal. If required, the shopper then  verifies the payment by entering their PIN or signature.

| **Parameter**   | **Required** | **Description**                                              |
| --------------- | ------------ | ------------------------------------------------------------ |
| ProtocolVersion | Yes          | 3.0                                                          |
| MessageClass    | Yes          | Service                                                      |
| MessageCategory | Yes          | Payment                                                      |
| MessageType     | Yes          | Request                                                      |
| SaleID          | Yes          | Your unique ID for the cash register.                        |
| ServiceID       | Yes          | Your unique ID for this request, consisting of 1-10 alphanumeric characters. Must be unique within the last 48 hours. |
| POIID           | Yes          | Unique ID of the terminal that you want to route this request to. Format: [device model]-[serial number]. |

PaymentRequest: The request body. This must include:

| **Parameter**                 | **Required** | **Description**                                              |
| ----------------------------- | ------------ | ------------------------------------------------------------ |
| SaleData.SaleTransactionID    | Yes          | An object with: TransactionID: Your unique reference for this request. In your Customer Area and Adyen reports, this will show as the merchant reference for the transaction. TimeStamp: Date and time of the request in UTC format. |
| PaymentTransaction.AmountsReq | Yes          | An object with: Currency: The transaction currency. RequestedAmount: The final transaction amount. |

 

| **SaleData**                                                 | ✔    | Object  | Sale System information attached to this payment             |
| ------------------------------------------------------------ | ---- | ------- | ------------------------------------------------------------ |
| [SaleReferenceID](https://datameshgroup.github.io/fusion/#data-dictionary-salereferenceid) |      | String  | Mandatory for pre-authorisation and completion, otherwise optional. See [SaleReferenceID](https://datameshgroup.github.io/fusion/#data-dictionary-salereferenceid) |
| **SaleTransactionID**                                        | ✔    | Object  |                                                              |
| [TransactionID](https://datameshgroup.github.io/fusion/#data-dictionary-transactionid) | ✔    | String  | Unique reference for this sale ticket. Not necessarily unique per payment request; for example a sale with split payments will have a number of payments with the same [TransactionID](https://datameshgroup.github.io/fusion/#data-dictionary-transactionid) |
| [TimeStamp](https://datameshgroup.github.io/fusion/#data-dictionary-timestamp) | ✔    | String  | Time of initiating the payment request on the POI System, formatted as [ISO8601](https://en.wikipedia.org/wiki/ISO_8601) DateTime. e.g. "2019-09-02T09:13:51.0+01:00" |
| **PaymentTransaction**                                       | ✔    | Object  |                                                              |
| **AmountsReq**                                               | ✔    | Object  | Object which contains the various components which make up the payment amount |
| [Currency](https://datameshgroup.github.io/fusion/#currency) | ✔    | String  | Three character currency code. Set to "AUD"                  |
| [RequestedAmount](https://datameshgroup.github.io/fusion/#requestedamount) | ✔    | Decimal | The requested amount for the transaction sale items, including cash back and tip requested |
| [PaidAmount](https://datameshgroup.github.io/fusion/#paidamount) |      | Decimal | Sum of the amount of sale items – `RequestedAmount`. Present only if an amount has already been paid in the case of a split payment. |
| [MinimumSplitAmount](https://datameshgroup.github.io/fusion/#minimumsplitamount) |      | Decimal | Present only if the POI Terminal can process an amount < `RequestedAmount` as a split amount. Limits the minimum split amount allowed. |
| [**OriginalPOITransaction**](https://datameshgroup.github.io/fusion/#data-dictionary-originalpoitransaction) |      | Object  | Identifies a previous POI transaction. Mandatory for Refund and Completion. See [OriginalPOITransaction](https://datameshgroup.github.io/fusion/#data-dictionary-originalpoitransaction) |
| [SaleID](https://datameshgroup.github.io/fusion/#data-dictionary-saleid) | ✔    | String  | [SaleID](https://datameshgroup.github.io/fusion/#data-dictionary-saleid) which performed the original transaction |
| [POIID](https://datameshgroup.github.io/fusion/#data-dictionary-poiid) | ✔    | String  | [POIID](https://datameshgroup.github.io/fusion/#data-dictionary-poiid) which performed the original transaction |
| **POITransactionID**                                         | ✔    | Object  |                                                              |
| [TransactionID](https://datameshgroup.github.io/fusion/#data-dictionary-transactionid) | ✔    | String  | `TransactionID` from the original transaction                |
| [TimeStamp](https://datameshgroup.github.io/fusion/#data-dictionary-timestamp) | ✔    | String  | `TimeStamp` from the original transaction                    |
| [ReuseCardDataFlag](https://datameshgroup.github.io/fusion/#reusecarddataflag) |      | Boolean | If 'true' the POI Terminal will retrieve the card data from file based on the `PaymentToken` included in the request. Otherwise the POI Terminal will read the same card again. |
| [ApprovalCode](https://datameshgroup.github.io/fusion/#approvalcode) |      | String  | Present if a referral code is obtained from an Acquirer      |
| [LastTransactionFlag](https://datameshgroup.github.io/fusion/#lasttransactionflag) | ✔    | Boolean | Set to true to process the Last Transaction with a referral code |
| **TransactionConditions**                                    |      | Object  | Optional transaction configuration. Present only if any of the JSON elements within are present. |
| [AllowedPaymentBrands](https://datameshgroup.github.io/fusion/#data-dictionary-allowedpaymentbrands) |      | Array   | Restricts the request to specified card brands. See [AllowedPaymentBrands](https://datameshgroup.github.io/fusion/#data-dictionary-allowedpaymentbrands) |
| [AcquirerID](https://datameshgroup.github.io/fusion/#data-dictionary-paymenttransaction.transactionconditions.acquirerid) |      | Array   | Used to restrict the payment to specified acquirers. See [AcquirerID](https://datameshgroup.github.io/fusion/#data-dictionary-paymenttransaction.transactionconditions.acquirerid) |
| [DebitPreferredFlag](https://datameshgroup.github.io/fusion/#debitpreferredflag) |      | Boolean | If present, debit processing is preferred to credit processing. |
| [ForceOnlineFlag](https://datameshgroup.github.io/fusion/#data-dictionary-forceonlineflag) |      | Boolean | If 'true' the transaction will only be processed in online mode, and will fail if there is no response from the Acquirer. |
| [MerchantCategoryCode](https://datameshgroup.github.io/fusion/#data-dictionary-merchantcategorycode) |      | String  | If present, overrides the MCC used for processing the transaction if allowed. Refer to ISO 18245 for available codes. |
| [**SaleItem**](https://datameshgroup.github.io/fusion/#data-dictionary-saleitem) | ✔    | Array   | Array of [SaleItem](https://datameshgroup.github.io/fusion/#data-dictionary-saleitem) objects which represent the product basket attached to this transaction. See [SaleItem](https://datameshgroup.github.io/fusion/#data-dictionary-saleitem) for examples. |
| [ItemID](https://datameshgroup.github.io/fusion/#data-dictionary-itemid) | ✔    | Integer | A unique identifier for the sale item within the context of this payment. e.g. a 0..n integer which increments by one for each sale item. |
| [ProductCode](https://datameshgroup.github.io/fusion/#data-dictionary-productcode) | ✔    | String  | A unique identifier for the product within the merchant, such as the SKU. For example if two customers purchase the same product at two different stores owned by the merchant, both purchases should contain the same `ProductCode`. |
| [EanUpc](https://datameshgroup.github.io/fusion/#data-dictionary-eanupc) |      | String  | A standard unique identifier for the product. Either the UPC, EAN, or ISBN. Required for products with a UPC, EAN, or ISBN |
| [UnitOfMeasure](https://datameshgroup.github.io/fusion/#data-dictionary-unitofmeasure) | ✔    | String  | Unit of measure of the `Quantity`. If this item has no unit of measure, set to "Other" |
| [Quantity](https://datameshgroup.github.io/fusion/#data-dictionary-quantity) | ✔    | Decimal | Sale item quantity based on `UnitOfMeasure`.                 |
| [UnitPrice](https://datameshgroup.github.io/fusion/#data-dictionary-unitprice) | ✔    | Decimal | Price per sale item unit. Present if `Quantity` is included. |
| [ItemAmount](https://datameshgroup.github.io/fusion/#data-dictionary-itemamount) | ✔    | Decimal | Total amount of the sale item                                |
| [TaxCode](https://datameshgroup.github.io/fusion/#data-dictionary-taxcode) |      | String  | Type of tax associated with the sale item. Default = "GST"   |
| [SaleChannel](https://datameshgroup.github.io/fusion/#data-dictionary-salechannel) |      | String  | Commercial or distribution channel of the sale item. Default = "Unknown" |
| [ProductLabel](https://datameshgroup.github.io/fusion/#data-dictionary-productlabel) | ✔    | String  | a short, human readable, descriptive name of the product. For example, `ProductLabel` could contain the product name typically printed on the customer receipt. |
| [AdditionalProductInfo](https://datameshgroup.github.io/fusion/#data-dictionary-additionalproductinfo) |      | String  | Additional information, or more detailed description of the product item. |
| [ParentItemID](https://datameshgroup.github.io/fusion/#parentitemid) |      | Integer | *Required* if this item is a 'modifier' or sub-item. Contains the [ItemID](https://datameshgroup.github.io/fusion/#data-dictionary-itemid) of the parent `SaleItem` |
| [CostBase](https://datameshgroup.github.io/fusion/#costbase) |      | Decimal | Cost of the product to the merchant per unit                 |
| [Discount](https://datameshgroup.github.io/fusion/#discount) |      | Decimal | If applied, the amount this sale item was discounted by      |
| [Categories](https://datameshgroup.github.io/fusion/#data-dictionary-categories) |      | Array   | Array of categories. Top level "main" category at categories[0]. See [Categories](https://datameshgroup.github.io/fusion/#data-dictionary-categories) for more information. |
| [Brand](https://datameshgroup.github.io/fusion/#brand)       |      | String  | Brand name - typically visible on the product packaging or label |
| [QuantityInStock](https://datameshgroup.github.io/fusion/#data-dictionary-quantityinstock) |      | Decimal | Remaining number of this item in stock in same unit of measure as `Quantity` |
| [Tags](https://datameshgroup.github.io/fusion/#sale-item-tags) |      | Array   | String array with descriptive tags for the product           |
| [Restricted](https://datameshgroup.github.io/fusion/#restricted) |      | Boolean | `true` if this is a restricted item, `false` otherwise. Defaults to `false` when field is null. |
| [PageURL](https://datameshgroup.github.io/fusion/#productpageurl) |      | String  | URL link to the sale items product page                      |
| [ImageURLs](https://datameshgroup.github.io/fusion/#productimageurls) |      | Array   | String array of images URLs for this sale item               |
| [Style](https://datameshgroup.github.io/fusion/#style)       |      | String  | Style of the sale item                                       |
| [Size](https://datameshgroup.github.io/fusion/#size)         |      | String  | Size of the sale item                                        |
| [Colour](https://datameshgroup.github.io/fusion/#colour)     |      | String  | Colour of the sale item                                      |
| [Weight](https://datameshgroup.github.io/fusion/#weight)     |      | Decimal | Sale item weight, based on `WeightUnitOfMeasure`             |
| [WeightUnitOfMeasure](https://datameshgroup.github.io/fusion/#data-dictionary-unitofmeasure) |      | String  | Unit of measure of the `Weight`.                             |
| **PaymentData**                                              | ✔    | Object  | Object representing the payment method. Present only if any of the JSON elements within are present. |
| [PaymentType](https://datameshgroup.github.io/fusion/#data-dictionary-paymenttype) | ✔    | String  | Defaults to "Normal". Indicates the type of payment to process. "Normal", "Refund", or "CashAdvance". See [PaymentType](https://datameshgroup.github.io/fusion/#data-dictionary-paymenttype) |
| [**PaymentInstrumentData**](https://datameshgroup.github.io/fusion/#data-dictionary-paymentinstrumentdata) |      | Object  | Object with represents card details for token or manually enter card details. See for object structure |

The example (with headers) shows how you would initiate a payment of 10.99 AUD on the terminal with the POIID V400m-324688179

```json
{
    "MessageId": "B0AF5655-C5A1-4713-8963-44362C0DEA33",
    "MessageType": "SaleToPOIRequest",
    "InitiatingBusinessUnit": {
        "ID": "112",
        "Name": "SampleStore"
    },
    "DestinationBusinessUnit": {
        "ID": "81",
        "Name": "DataMesh Group"
    },
    "NotifiedBusinessUnits": [{
        "ID": "113",
        "Name": "HeadOffice"
    }],
    "SaleToPOIRequest": {
        "MessageHeader": {
            "MessageCategory": "Payment",
            "MessageClass": "Service",
            "MessageType": "Request",
            "ProtocolVersion": "3.1",
            "SaleID": "test-123456789",
            "ServiceID": {{ServiceID}},
            "POIID": {{POIID}}
        },
        "PaymentRequest": {
            "PaymentTransaction": {
                "AmountsReq": {
                    "Currency": "AUD",
                    "RequestedAmount": 10.99
                }
            },
            "SaleData": {
                "SaleTransactionID": {
                    "TimeStamp": "2020-03-16T12:30:00+0100",
                    "TransactionID": "12345678-abcd-abcd-abcd-123456789abc"
                },
                <!-- DMG Custom Element -->
                "SaleToAcquirerData": "
                                        
                                      "
                "SaleItems": [
                    {
                        "ItemID": 0,
                        "Brand": "Gucci",
                        "EanUpc": "000112345",
                        "ParentItemID": null,
                        "ProductCode": "1234",
                        "ProductLabel": "Panadol",
                        "AdditionalProductInfo": "",
                        "QuantityInStock": 5,
                        "SaleChannel": "Unknown",
                        "Category": "Analgesics",
                        "SubCategory":  "Analgesics - OTC",
                        "Tags": ["tagA", "tagB"],
                        "TaxCode": "GST",
                        "UnitOfMeasure": "Unit",
                        "Quantity": 1,
                        "ItemAmount": 15.00,
                        "UnitPrice": 15.00,
                        "CostBase": 12.00,
                        "Discount": 0.00
                    }
                ]
                <!-- End DMG Custom Element -->
            }
        }
    }
}
```

The response message is:

```json
{
    "MessageId": "B0AF5655-C5A1-4713-8963-44362C0DEA33",
    "MessageType": "SaleToPOIRequest",
    "InitiatingBusinessUnit": {
        "ID": "81",
        "Name": "DataMesh Group"
    },
    "DestinationBusinessUnit": {
        "ID": "112",
        "Name": "SampleStore"
    },
    "NotifiedBusinessUnits": [{
        "ID": "113",
        "Name": "HeadOffice"
    }],
    {
      "SaleToPOIResponse":{
        "MessageHeader":{...},
        "PaymentResponse":{
          "POIData":{
            "POITransactionID":{
              "TransactionID": "oLkO0012498220087000.981517998282382C"
            },
            ...
          },
          "Response":{
            "Result":"Success",
            "AdditionalResponse":"...shopperEmail=shoppersemail%40address.com..."
          },
          ...
        },
        "PaymentReceipt":{...}
      }
    }
}
```

