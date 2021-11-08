# InventoryAction

### 6.0 USE CASE: INVENTORY POSITION STATEMENT

This use case describes the ability for one system to communicate inventory position to another system. The scenarios in this use case demonstrate both an unsolicited statement and a more targeted, solicited statement.

**6.1 Scenario: Master Inventory system publishes an inventory position statement**

**Brief Description**

A store based inventory system is used for perpetual inventory. The store system publishes an inventory position statement on a periodic basis.

**Pre Condition**

\1. Publisher holds the master inventory position for the store

 

**6.1 Conformance JSON Document – Inventory Position**

```json
{
    "InventoryAction": {
      "InventoryPosition": {
        "Items": [
          {
              "ItemID": "1234",
              "State": "AvailableToSell",
              "AlternativeItemIDs": [
                  {
                    "Type": "UPI",
                    "ID": "ABCD123"
                  },
                  {
                    "Type": "UPC",
                    "ID": "221341234"
                  },
                  {
                    "Type": "HOID",
                    "ID": "ZXY124"
                  },
                ],
              "Quantity": 100
          },
          {
              "ItemID": "1234",
              "State": "AvailableOnHand",
              "AlternativeItemIDs": [
                  {
                    "Type": "UPI",
                    "ID": "ABCD124"
                  },
                  {
                    "Type": "UPC",
                    "ID": "221341234"
                  },
                  {
                    "Type": "HOID",
                    "ID": "ZXY124"
                  },
                ],
              "Quantity": 20
          }
        ]
      }
    }
}
```

