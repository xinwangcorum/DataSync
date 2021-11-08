# CoPay

## **19. USE CASE: Co-Pay**

### **19.1 Scenario: Customer Tenders Co-Pay Purchase, i.e. Drug Purchase (V2.1)**

**Brief Description**

Customer selects one or more items and pays co-pay, instead of the total price, typically insurance picks up the remainder of the cost of the item(s).

**Data** 

-  Tender Type = Co-Pay 
-  Type = Sale 
-  Co-Pay Tender Amount 
-  Total Amount

19.1 Conformance JSON Instance Document - Co-Pay

Move co-pay details to the tender section.

```json
{
   "Transaction": {
      "BusinessUnit": {
         "ID": "100",
         "Name": "HighStreet",
      },
      "WorkstationID": "POS5",
      "SequenceNumber": "4294967295",
      "OperatorID": "John",
      "RetailTransaction": {
         "LineItem": [
            {
               "Sale": {
                  "ItemType": "Stock",
                  "Quantity": 1,
                  "UnitPrice": 2.79,
                  "ExtendedAmount": 2.79,
               },
               "SequenceNumber": "1"
            },
            {
               "Tender": {
                  "TenderType": "CoPay",
                  "CoPayType": "Government Recovery",
                  "Amount": "1.74"
               },
               "ItemLink": "1"
            },
            {
               "Tender": {
                  "TenderType": "Cash",
                  "Amount": "1.05"
               },
               "SequenceNumber": "2"
            }
         ],
         "Total": {
            "TransactionGrossAmount": 2.79
         }
      }
   }
}
```

Lots Perspective:

```json

{
   "Transaction": {
      "BusinessUnit": {
         "ID": "100",
         "Name": "HighStreet",
      },
      "WorkstationID": "POS5",
      "SequenceNumber": "4294967295",
      "OperatorID": "John",
      "RetailTransaction": {
         "LineItem": [
            {
               "Sale": {
                  "ItemType": "Stock",
                  "Quantity": {Quantity},
                  "UnitPrice": {Retail + GovtRecovery},
                  "ExtendedAmount": {Quantity * (Retail + GovtRecovery)},
               },
               "SequenceNumber": "1"
            },
            {
               "Tender": {
                  "TenderType": "CoPay",
                  "CoPayType": "Government Recovery"
                  "Amount": {Quantity * GovtRecovery}
               },
               "ItemLink": "1"
            },
            {
               "Tender": {
                  "TenderType": "Cash",
                  "Amount": "1.05"
               },
               "SequenceNumber": "2"
            }
         ],
         "Total": {
            "TransactionGrossAmount": {sum(Quantity * (Retail + GovtRecovery))}
         }
      }
   }
}
```

https://www.pbs.gov.au/info/healthpro/explanatory-notes/front/fee