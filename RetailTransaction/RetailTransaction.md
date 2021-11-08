# Retail Transaction (Sale)

[Overview](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297561116/Retail+Transaction+Sale#Overview)

[Out of Scope Use Cases](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297561116/Retail+Transaction+Sale#Out-of-Scope-Use-Cases)

[4. Use Case: Item Purchase](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297561116/Retail+Transaction+Sale#4.-Use-Case:-Item-Purchase)

- [4.1 Scenario: Item Purchase at POS (v2.1)](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297561116/Retail+Transaction+Sale#4.1-Scenario:-Item-Purchase-at-POS-(v2.1))
- [4.2 Scenario: Item purchase via www or Tele-Sales (v2.1)](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297561116/Retail+Transaction+Sale#4.2-Scenario:-Item-purchase-via-www-or-Tele-Sales-(v2.1))

[5.0 Use case: Fees](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297561116/Retail+Transaction+Sale#5.0-Use-case:-Fees)

- [5.1 Miscellaneous Fee (V6.0) ](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297561116/Retail+Transaction+Sale#5.1-Miscellaneous-Fee-(V6.0))

[9.0 Use Case: Merchandise Hierarchy](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297561116/Retail+Transaction+Sale#9.0-Use-Case:-Merchandise-Hierarchy)

- [9.1 Scenario: Item Purchase from Category (V6.0)](https://corumgroup.atlassian.net/wiki/spaces/DTS/pages/2297561116/Retail+Transaction+Sale#9.1-Scenario:-Item-Purchase-from-Category-(V6.0))

## Out of Scope Use Cases

- **4.0 Use Case: Item purchase**

  - 4.2 SCENARIO: ITEM PURCHASE VIA WWW OR TELE-SALES (V2.1)
  - 4.3 SCENARIO: ITEM PURCHASE FOR ALTERATION & SUBSEQUENT PICKUP (V2.1)
  - 4.4 SCENARIO: ITEM PURCHASE OF SERIALIZED ITEM (V2.1)
  - 4.5 SCENARIO: ITEM PURCHASE WITH PART EXCHANGE (V2.1)
  - 4.6 SCENARIO: ITEM PURCHASE WITH QUANTITY PRICING (V2.1)
  - 4.7 SCENARIO: ITEM PURCHASE OF MULTI-PACKAGE ITEMS (V2.1)
  - 4.8 SCENARIO: ITEM PURCHASE BY SELLING LOCATION (V2.1)
  - 4.9 SCENARIO: ITEM PURCHASE WITH SPECIAL ORDER (V2.1)

- **5.0 USE CASE: FEES**

  - 5.2 SCENARIO: MULTIPLE SHIPPING CHARGES (V2.2)
  - 5.3 SCENARIO: RESTOCKING FEE (V2.2)

- **6.0 USE CASE: One Retail Transaction Referencing Multiple Customer Order**

  **Transactions (V6.0)**

  - 6.1 SCENARIO: ONE RETAIL TRANSACTION REFERENCING MULTIPLE CUSTOMER ORDER

    TRANSACTIONS (V6.0)

- **7.0 Use Case: Required age to purchase item (V6.0)**

  - 7.1 SCENARIO: ITEMS ARE BEING SCANNED AT A SELF CHECKOUT DEVICE AND AT A

    PAYSTATION THE AGE VERIFICATION IS DONE.(V6.0)

  - 7.2 SCENARIO: PURCHASE OF A GUN AND ALCOHOL (V6.0)

- **8.0 Use Case: Mix & Match**

  - 8.1 SCENARIO: TRANSACTION APLICABLE TO MIX & MATCH (V2.2)
  - 8.2 SCENARIO: MIX-MATCH NORMAL PRICE (V2.2)

- **10. Use Case: Item purchase of kit/combo/Collection items**

  - 10.1 SCENARIO: KIT RECURSION (V6.0)
  - 10.2 SCENARIO KIT/COMBO/COLLECTION PURCHASE WITHOUT SUBSTITUTION (V2.1)
  - 10.3 SCENARIO: KIT/COMBO/COLLECTION PURCHASE WITH SUBSTITUTION (V2.1)

- **11. Use Case: Item purchase with manual price override**

  - 11.1 SCENARIO: OPEN PLU (UNPRICED ITEM) (V2.1)
  - 11.2 SCENARIO: CUSTOMER COMPLAINT ABOUT PRICE (V2.1)
  - 11.3 SCENARIO: DIFFERENT TAG PRICE (V2.1)
  - 11.4 SCENARIO: MANAGER COMPLIMENTARY (V2.1)
  - 11.5 SCENARIO:CHARITABLE CONTRIBUTION (V2.1)

- \12. **USE CASE: Weighted Sales**

  - 12.1 SCENARIO: ITEM PURCHASE BY MANUAL WEIGHT (V2.1)

  - 12.2 SCENARIO: PROVIDE RESOLUTION FOR QUANTITY FOR ENTRY METHOD WEIGHED (V6.0)

  - 12.3 SCENARIO: ITEM PURCHASE BY RANDOM WEIGHT (V2.1)

  - 12.4 SCENARIO: SOLD BY WEIGHT WITH TARE REMOVED (V2.2)

  - 12.5 SCENARIO: SOLD BY WEIGHT WITH DIFFERENT MEASUREMENTS FOR PRICING AND

    INVENTORY (V6.0)

- **13. Ticketing**

  - 13.1 SCENARIO: SEAT INFORMATION (V6.0)
  - 13.2 SCENARIO: TICKET SPECIFIC INFORMATION (V6.0)

## 4. Use Case: Item Purchase

One or more items are purchased via any one of a number of sales channels. The transaction is entered in via an appropriate application, and is sent using the POSLog schema to the POSLog application, which may forward to the transaction to other applications in the enterprise.

### 4.1 Scenario: Item Purchase at POS (v2.1)

**Brief Description**

Customer selects one or more items and purchases them. The number of those items available in inventory is decremented.

**Scenario Description**

Tom purchases three 4 oz. bars of dark chocolate. After this purchase, the store’s inventory 4oz dark chocolate bars is reduced by three.

**Data**

- Transaction header data, including: 
  - Identifiers for Store, Workstation, & Operator performing the transaction. 
  - The date & time the transaction was performed 
  - A workstation assigned sequence number identifying the transaction 
- Item sale data, including: 
  - An identifier for the item being sold. 
  - The number of multiples of the item being sold. 
  - Unit price for the item being sold. 
  - The extended amount (i.e. Unit price * the number of items being sold)

**Sample JSON (Sample Json Document (shows what could be done)**

Use Case: Item Purchase from shelf

Note: This example includes all optional fields

```json
{
   "Transaction": {
      "CancelFlag": "false",
      "WorkstationID": "POS5",
      "BusinessUnit": {
         "ID": "120",
         "Name": "eStore",
      },
      "TillID": "22",
      "SequenceNumber": "4294967295",
      "BusinessDayDate": "2001-08-13",
      "BeginDateTime": "2001-08-13T09:03:00",
      "EndDateTime": "2001-08-13T09:05:00",
      "OperatorID": "John",
      "CurrencyCode": "USD",
      "RetailTransaction": {
         "ManagerApproval": "false",
         "ReceiptDateTime": "2001-08-13T09:04:32",
         "LineItem": [
         {
            "VoidFlag": "false",
            "SequenceNumber": "1",
            "BeginDateTime": "2001-09-16T09:04:00",
            "EndDateTime": "2001-09-16T09:04:03",
            "Sale": {
               "ItemType": "Stock",
               "ItemID": "CA7865",
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
               "MerchandiseHierarchy": [
                {
                    "Level": "Department",
                    "Value": "Confectionary"
                },
                {
                    "Level": "SubDepartment",
                    "Value": "Chocolates"
                }
               ],
               "ItemNotOnFileFlag": "false",
               "Description": "4oz Dark Chocolate",
               "TaxIncludedInPriceFlag": "false",
               "UnitCostPrice": "1.23",
               "UnitListPrice": "1.79",
               "RegularSalesUnitPrice": "1.63",
               "InventoryValuePrice": "1.23",
               "ActualSalesUnitPrice": "1.63",
               "ExtendedAmount": "4.89",
               "DiscountAmount": "0.00",
               "ExtendedDiscountAmount": "4.89",
               "Quantity": "3"
            }
         },
         {
          "Tender": {
              "TenderType": "Cash",
              "TypeCode": "Sale",
              "Amount": "0.83",
              "TenderChange": {
                "Amount": "0.00"
              }
          },
          "SequenceNumber": "2"
          },
          {
            "Tender": {
                "TenderType": "CreditDebit",
                "TypeCode": "Sale",
                "Amount": "4.00",
                "CreditDebit": {
                  "CardType": "Credit"
                }
            },
            "SequenceNumber": "3"
          }
         ],
         "Total": {
            "TotalType": "TransactionGrossAmount",
            "Amount": "4.89"
         }
      }
   }
}
```

**Sample Json Document – Item Purchase from Shelf**

Use case: Item purchase from shelf

Note: This example includes no optional data, and shows the most minimal set of data requried to record a sale.

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
         "LineItem": {
            "Sale": {
               "ItemType": "Stock",
               "POSIdentity": {
                  "POSItemID": "01234567890123"
               },
               "ExtendedAmount": "4.89"
            },
            "SequenceNumber": "1"
         }
      }
   }
}
```

### 4.2 Scenario: Item purchase via www or Tele-Sales (v2.1)

**Brief Description**

Customer selects one or more items for purchase via a website, or from a printed catalogue. Purchase order is accepted via one of www, fax or telephone along with payment details. The items purchased, are shipped to the customer, and inventory count for the items is decremented.

**Data**

- Transaction header data, including:
  - Identifier for the store performing the transaction. 
  - The date the transaction was performed
  -  A system assigned sequence number identifying the transaction o Identifier for the WWW server that processed the transaction.
- Item sale data, including:
  - An identifier for the item being sold.
  - The number of multiples of the item being sold.
  - Unit price for the item being sold. 
  - The extended amount (i.e. Unit price * the number of items being sold) o Item inventory reservation tracking number
- Delivery information for the transaction, or for each individual item purchased, including:
  - Name & Address for delivery o Preferred delivery method
  - Preferred delivery date & time

**4.2a Conformance XML Instance Document – Item Purchase via WWW**

- UseCase: Item Purchase via WWW
- Note: the eCommerce operation is treated as a particular store (called "eStore" in this example)
- WorkstationID is used to identify the eCommerce server 
- OperatorID is not relevant, and is missing
- Addition of InventoryReservation & Delivery

```json
{
   "Transaction": {
      "BusinessUnit": {
         "ID": "120",
         "Name": "eStore",
      },
      "WorkstationID": "Server2",
      "SequenceNumber": "4294967295",
      "OperatorID": "John",
      "RetailTransaction": {
         "LineItem": {
            "SaleForDelivery": {
               "ItemType": "Stock",
               "POSIdentity": {
                  "POSItemID": "01234567890123"
               },
               "ExtendedAmount": "489.00",
               "Quantity": "3",
               "Delivery": {
                  "Name": {
                     "Name": "Jones"
                  },
                  "Address": {
                     "AddressLine": [
                        "325 7th St. NW.",
                        "Suite 1100"
                     ],
                     "City": "Washington",
                     "Territory": "D.C."
                  },
                  "TelephoneNumber": {
                     "AreaCode": "601",
                     "LocalNumber": "555-4793"
                  }
               }
            },
            "SequenceNumber": "1"
         }
      }
   }
}
```

## 5.0 Use case: Fees

### **5.1 Miscellaneous Fee (V6.0)** 

**Brief Description**

Whenever there is a fee associated with an item, POSLog records the fee as a separate sale line item and links it to the line item where the fee applies.

**Scenario Description**

Suzy takes 1000 pictures in to have them printed for $.25 each. She is going to visit her grandmother so she needs them immediately. Because of the priority there is an additional processing fee of $5.00.

**Data**

Sale = ItemType = “Fee”

Line Item – Item Link

**5.1 Conformance XML Instance Document – Miscellaneous Fee**

```json
{
   "Transaction": {
      "BusinessUnit": {
         "ID": "2234",
         "Name": "HighStreet",
      },
      "WorkstationID": "Register 2",
      "SequenceNumber": "4294967295",
      "POSLogDateTime": "2001-08-13T08:05:00",
      "OperatorID": "John",
      "RetailTransaction": {
         "LineItem": [
            {
               "Sale": {
                  "ItemType": "Stock",
                  "POSIdentity": {
                     "POSItemID": "01234567890123"
                  },
                  "ExtendedAmount": "100.00"
               },
               "SequenceNumber": "1"
            },
            {
               "Sale": {
                  "ItemType": "Fee",
                  "POSIdentity": {
                     "POSItemID": "asdfasdf"
                  },
                  "ExtendedAmount": "10.00",
                  "ItemLink": "1"
               },
               "SequenceNumber": "2"
            },
            {
               "Tender": {
                  "TypeCode": "Refund",
                  "Amount": "90.00"
               },
               "SequenceNumber": "3"
            }
         ]
      }
   }
}
```

## 9.0 Use Case: Merchandise Hierarchy

### **9.1 Scenario: Item Purchase from Category (V6.0)**

**Brief Description**

Customer purchases items in a particular merchandise hierarchy.

**Scenario Description**

Ralph purchases a soft drink for $2.79

**Data** 

9.1 ARTS XML Conformance XML Instance Document – Item Purchase from Category

<!--  UseCase: Item Purchase with Multi-Package Items              -->
<!--  Note: no ItemID; Merchandise Hierarchy use to identify item  -->

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
                  "MerchandiseHierarchy": {
                     "Level": "Department",
                     "Value": "Soft Drinks"
                  },
                  "ExtendedAmount": "2.79"
               },
               "SequenceNumber": "1"
            },
            {
               "Tender": {
                  "TenderType": "Cash",
                  "TypeCode": "Sale",
                  "Amount": "2.79"
               },
               "SequenceNumber": "2"
            }
         ]
      }
   }
}
```

