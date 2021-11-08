# Retail Transaction (Return)

[Overview](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2287861865/Retail+Transaction+Return#Overview)

[Out of Scope Use Cases](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2287861865/Retail+Transaction+Return#Out-of-Scope-Use-Cases)

[4. Use Case: Item Return](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2287861865/Retail+Transaction+Return#4.-Use-Case:-Item-Return)

- [4.2 Scenario: Return to Store (V2.1)](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2287861865/Retail+Transaction+Return#4.2-Scenario:-Return-to-Store-(V2.1))

**NOTE: THESE SCENARIOS DON’T SHOW TENDER REFUNDS. TENDER REFUNDS ARE SHOWN IN VOLUME 2 TENDERS.**

## Out of Scope Use Cases

- **4.0 Use Case: Item purchase**
  - 4.2C Alternative Conformance XML Instance Document - Return to Store (w/ OperatoryBypassApproval)
  - 4.3 Scenario: Return for Delivery by Customer (V2.1)
  - 4.4 Return for Pickup from Customer (V2.1)
  - 4.5 Scenario: Return (to multiple) Linked Transactions (V2.2)
- 5 Return with Commission
  - 5.1 Scenario: Newspaper With Commission (V2.2)
  - 5.2 Scenario: Return with Commissions (V2.2)
- 6.0 Post-Purchase Price Adjustment
  - 6.1 Scenario: Customer Gets Refund in Cash after Returning to the Store (V2.1)

## 4. Use Case: Item Return

Items are returned to a retailer for various reasons, and the return process may be conducted online, through a call center or in stores. The scenarios in this use case illustrate the fact that the resultant XML follows the pattern established by the sale of items via the various channels. All scenarios in this use case use the same set of actors.

### 4.2 Scenario: Return to Store (V2.1)

**Brief Description**

Customer returns an item to a store, and the number of those items available in inventory may or may not be incremented, depending on whether the returned item is put back into stock.

**Scenario Description**

Suzy and Dan are getting married in two months on October 31. Their friends bought them a set of chinaware for their wedding gift on September 1. The normal refund/return is 30 days.

**Data**

- Transaction header data, including:
  - Identifiers for Store, Workstation, & Operator performing the transaction. 
  - The date the transaction was performed 
  - A workstation assigned sequence number identifying the transaction
- Item data, including: 
  - A department identifier for the item being sold. 
  - Which level in the department hierarchy is being used to identify the item. 
  - The number of multiples of the item being sold. 
  - The current unit-price of the item 
- Return data, including: 
  - Transaction link information identifying the original purchase that validates the return.
  - Approval information identifying the manager who approved the return.
  - Disposal information identifying how the returned item is to be treated.

**4.2b Conformance Json Document - Return to Store**

Use Case: Item Return

Note: Addition of Disposal and OperatorBypassApproval elements

Note: Inclusion of TransactionLink at line item level to validate the return

```json
{
   "Transaction": {
      "BusinessUnit": {
         "UnitID": "HighStreet"
      },
      "WorkstationID": "POS5",
      "SequenceNumber": "4294967295",
      "OperatorID": "John",
      "RetailTransaction": {
         "LineItem": {
            "Return": {
               "ItemType": "Stock",
               "ExtendedAmount": "4.89",
               "Quantity": "3",
               "TransactionLink": {
                  "ReasonCode": "Return",
                  "BusinessUnit": "HighStreet",
                  "WorkstationID": "POS5",
                  "BusinessDayDate": {
                     "Date": "2001-08-12"
                  },
                  "SequenceNumber": "42949672912"
               },
               "Disposal": {
                  "Method": "ReturnToStock"
               }
            },
            "SequenceNumber": "1"
         }
      }
   }
}
```

**4.2b Alternative Conformance JSON Document - Return to Store**

Use case: Item Return

Note: Addition of Disposal and OperatorBypassApproval elements

Note: Inclusion of TransactionLink at transaction header to validate return

```json
{
   "Transaction": {
      "BusinessUnit": {
         "UnitID": "HighStreet"
      },
      "WorkstationID": "POS5",
      "SequenceNumber": "4294967295",
      "OperatorID": "John",
      "RetailTransaction": {
         "LineItem": {
            "Return": {
               "ItemType": "Stock",
               "ExtendedAmount": "4.89",
               "Quantity": "3",
               "Disposal": {
                  "Method": "ReturnToStock"
               }
            },
            "SequenceNumber": "1"
         },
         "TransactionLink": {
            "ReasonCode": "Return",
            "BusinessUnit": "HighStreet",
            "WorkstationID": "POS5",
            "BusinessDayDate": {
               "Date": "2001-08-12"
            },
            "SequenceNumber": "42949672912"
         }
      }
   }
}
```

