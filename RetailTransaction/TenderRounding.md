# Tender Rounding

# Overview

According to specific legislation rules or currency specifics in several countries, rounding of amounts is required. To which kind of amounts – transaction totals, tender amounts, or others – the rounding rules apply may differ from country to country.

A retailer may also decide on his own to round amounts in favor of the customer in specific situations like e.g. when the customer returns items, or when he is granted a discount.

Rounding is always done by using a defined method (round-up or round-down) and with a defined precision (e.g. the smallest possible denomination of the currency used for tendering).

For example, because of its cost, Canada is phasing out the penny and allowing retailers to round cash tenders to cover the difference. Cash payments or transactions only will need to be rounded, either up or down, to the nearest five-cent increment. For example if the amount is $1.01 or $1.02 the cash tender will be rounded down to $1.00. However if the amount is 1$1.03 or $1.04, the cash tender will be rounded up to $1.05.

In Canada these only apply to cash transactions, checks and transactions using electronic payments—debit, credit and payments cards—do not need to be rounded, because they can be settled electronically to the exact amount.

The interesting twist in Canada is to allow the rounding of the amount on either the transaction or on the change given back to the customer. For example if the amount of the transaction is $4.92, the transaction can be rounded down to $4.90 or the change given back can be rounded up to $0.10 (in this case the receipt will show $4.92). If the customer pays with a credit/debit then the amount is $4.92 and no rounding takes place.

 

### **4. Use Case: Rounding**

**4.1 Scenario: Rounding of Transaction Totals**

**Brief Description**

In some countries, cash transaction totals are to be rounded to multiples of a defined currency denomination. This applies, for example in Finland, where transaction totals are to be rounded to multiples of .05 EUR.

**Scenario Description**

Hakon buys a bottle of milk for 1.19 EUR and some bread for 1.49 EUR. His total of 2.68 EUR is rounded up to 2.70 EUR. The rounded amount is .02 EUR.

Data

Rounding amount for the transaction

- Threshold Value
- Amount
- Direction

**4.1 Conformance JSON Document – Rounding of Transaction Total**s

```json
{
   "Transaction": {
      "BusinessUnit": {
         "UnitID": "Speciality Sandwich Shop"
      },
      "WorkstationID": "POS5",
      "SequenceNumber": "4294967295",
      "OperatorID": "John",
      "RetailTransaction": {
         "LineItem": [
            {
               "Sale": {
                  "POSIdentity": {
                     "POSItemID": "01234567890123"
                  },
                  "ExtendedAmount": {
                     "Currency": "EUR",
                     "Amount": "1.19"
                  }
               },
               "SequenceNumber": "1"
            },
            {
               "Sale": {
                  "POSIdentity": {
                     "POSItemID": "sdf"
                  },
                  "ExtendedAmount": {
                     "Currency": "EUR",
                     "Amount": "1.49"
                  }
               },
               "SequenceNumber": "2"
            },
            {
               "Tender": {
                  "TenderType": "Cash",
                  "Amount": "2.70",
                  "Rounding": {
                     "RoundingDirection": "Up",
                     "Amount": "0.02"
                  }
               },
               "SequenceNumber": "3"
            }
         ]
      }
   }
}
```

