# Inventory

[Out of Scope:](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297495690/Inventory#Out-of-Scope:)

- [6.1 Scenario: Store Goods Receipt](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297495690/Inventory#6.1-Scenario:-Store-Goods-Receipt)
- [7.1 Scenario: Inventory Breakage](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297495690/Inventory#7.1-Scenario:-Inventory-Breakage)
- [7.2 Conformance JSON Document – Inventory Spoilage](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297495690/Inventory#7.2-Conformance-JSON-Document-–-Inventory-Spoilage)
- [8.2 Conformance JSON Document – Return To Vendor](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297495690/Inventory#8.2-Conformance-JSON-Document-–-Return-To-Vendor)
- [X.X Conformance JSON Document – Order](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297495690/Inventory#X.X-Conformance-JSON-Document-–-Order)

## Out of Scope:

- 8.1 Conformance JSON Document Document - Merchandise for Store Use

**4.1 Scenario: Transfer between stores**

Within a retail chain there is sometimes a need to transfer goods from one store to another. This might be due to one store being sold out of a popular item.

**Brief Description**

A manager from store X where a particular item is out of stock goes into store Y where there is a large inventory of that item. He selects several of the items that his store is out of and identifies himself to the store personnel. The items are entered into an inventory control transaction. Both the sending and receiving stores are identified.

**Data**

- Store transfer transaction - Transfer
  - Item information
  - Store ID of the store that is receiving the items – To Party.
  - Store ID of the store that is sending the items – From Party
- Store receipt transaction – Receipt 
  - Item information 
  - Store ID of the store that is receiving the items – To Party
  - Store ID of the store that is sending the items – From Party

**4.1 Conformance JSON Document – Store Transafer**

```json
{
   "Transaction": {
      "BusinessUnit": {
         "UnitID": "RetailStoreID"
      },
      "WorkstationID": "WorkstationID",
      "SequenceNumber": "1234",
      "OperatorID": {
         "OperatorName": "Taro",
         "ID": "e11111"
      },
      "CurrencyCode": "JPY",
      "InventoryControlTransaction": {
         "Transfer": {
            "SourceBusinessUnitID": "123",
            "DestinationBusinessUnitID": "456",
            "LineItem": {
               "ItemID": "97"
            }
         }
      }
   }
}
```

### **6.1 Scenario: Store Goods Receipt**

**Brief Description**

100 shirts were received and logged into inventory through the POS.

**6.1 Conformance JSON Document - Store Goods Receipt**

```json
{
   "Transaction": {
      "BusinessUnit": {
         "UnitID": "HighStreet"
      },
      "WorkstationID": "POS5",
      "SequenceNumber": "4294967295",
      "OperatorID": "John",
      "InventoryControlTransaction": {
         "ReceiveInventory": {
            "DocumentID": "12341234",
            "ActualDeliveryDate": "2001-08-13",
            "LineItem": {
               "ItemID": "1234",
               "QuantityReceived": "100"
            }
         }
      }
   }
}
```

### 7.1 Scenario: Inventory Breakage

**Brief Description**

Customer dropped a vase and broke it.

**7.1 Conformance JSON Document – Inventory Breakage**

```json
{
   "Transaction": {
      "BusinessUnit": {
         "UnitID": "HighStreet"
      },
      "WorkstationID": "POS5",
      "SequenceNumber": "4294967295",
      "OperatorID": "John",
      "CurrencyCode": "USD",
      "InventoryControlTransaction": {
         "InventoryLoss": {
            "TypeCode": "Breakage",
            "ItemID": "1231234",
            "Quantity": "1"
         }
      }
   }
}
```

### **7.2 Conformance JSON Document – Inventory Spoilage**

```json
{
   "Transaction": {
      "OfflineFlag": "false",
      "TrainingModeFlag": "false",
      "BusinessUnit": {
         "UnitID": "HighStreet"
      },
      "WorkstationID": "POS5",
      "SequenceNumber": "4294967295",
      "InventoryControlTransaction": {
         "InventoryLoss": {
            "TypeCode": "Spoilage",
            "ItemID": "1231234",
            "Quantity": "100"
         }
      }
   }
}
```

### **8.2 Conformance JSON Document – Return To Vendor**

```json
{
  "Transaction": {
      "BusinessUnit": {
         "UnitID": "HighStreet"
      },
      "WorkstationID": "POS5",
      "SequenceNumber": "4294967295",
      "InventoryControlTransaction": {
         "ReturnToVendor": {
            "LineItem": {
               "ItemID": "1234"
            }
         }
      }
   }
}
```

### **X.X Conformance JSON Document – Order**

Note: Cannot find the portion of the spec, that defines this section although I can see it in the ODM, therefor I will try my best to blend retailtransaction and inventorycontrol concepts.

```json
{
  "Transaction": {
      "BusinessUnit": {
         "UnitID": "HighStreet"
      },
      "WorkstationID": "POS5",
      "SequenceNumber": "4294967295",
      "InventoryControlTransaction": {
         "Order": {
            "SupplierBusinessUnitID": "456",
            "LineItem": [
              {
                "SupplierItemID": "ABCD123",
                "TypeCode": "Merchandise" // Freight, Charge, Allowance, FreeText, Tax, Merchandise, 
                "ItemID": "1234",
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
                    "ID": "ZXY123"
                  },
                ],
                "ItemDescription": "GLAM ADRIANA LASHES NEW",
                "UnitCount": 3,
                "UnitBaseCostAmount": 13.60, 
                "UnitsShippedCount": 0,
                "Tax": {
                     "TaxType": "GST",
                     "Amount": "1.36"
                },
                "TaxIncludedInPriceFlag": "true"
              }
            ]
         }
      }
   }
}
```

