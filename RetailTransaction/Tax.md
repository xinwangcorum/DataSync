# Tax

### 5.1 Scenario: Normal VAT Tax (V2.1)

**Brief Description**

A customer purchases an item. The VAT taxes are included in the item lookup prices. They are reported at the item level.

**Assumption**

In many places VAT tax is calculated on the transaction level but for this example Tax is calculated on item level. Pre-Conditions Post-Conditions Scenario Description Customer buys 3 soft drinks for 1.65 AUD each. The lookup price of the soft drinks includes a 10% VAT tax.

**Data** 

- By Item
  - Taxable Amount
  - Tax Amount
  - Indication whether or not this is an included tax

**5.1 Conformance Json Document – Normal GST Taxes**

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
         "LineItem": [
            {
               "Sale": {
                  "ItemType": "Stock",
                  "POSIdentity": {
                     "POSItemID": "01234567890123"
                  },
                  "ExtendedAmount": "4.95",
                  "Quantity": "3",
                  "Tax": {
                     "TaxType": "GST",
                     "Amount": "0.45"
                  },
                  "TaxIncludedInPriceFlag": "true"
               },
               "SequenceNumber": "1"
            },
            {
               "Tender": {
                  "TenderType": "Cash",
                  "TypeCode": "Sale",
                  "Amount": "4.95"
               },
               "SequenceNumber": "2"
            }
         ]
      }
   }
}
```

