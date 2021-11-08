# Tender Line Items

## Overview

This area details the variations around tendering, when applied against a sale (or return).

TenderTypes should include

- Cash/Change
- Afterpay
- On Account (e.g. Insurance)
- Credit/Debit

### **5.1 Scenario: Customer Tenders Purchase with Cash Tender without Cash Back (2.1)**

**Brief Description**

Customer selects one or more items and purchases them with exact cash.

Data:

- Tender Type = Cash
- Type = Sale
- The amount of the tender

**5.1 Conformance XML Instance Document - Cash Purchase without Change**

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
                  "ExtendedAmount": "4.89",
                  "Quantity": "3"
               },
               "SequenceNumber": "1"
            },
            {
               "Tender": {
                  "TenderType": "Cash",
                  "TypeCode": "Sale",
                  "Amount": "4.89"
               },
               "SequenceNumber": "2"
            }
         ]
      }
   }
}
```

### **5.2 Scenario: Customer Tenders Purchase with Cash Tender with Cash Back (V2.1)**

**Brief Description**

Customer selects one or more items and purchases them with cash, getting cash back.

**Scenario Description**

A customer buys a hamburger for $2.50 and pays with a $5.00 bill.

**Data**

- Tender Type = Cash
- Type = Sale
- Amount Tendered
- Amount of Change

**5.2 Conformance XML Instance Document – Cash Purchase with Change**

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
                  "ExtendedAmount": "4.89",
                  "Quantity": "3"
               },
               "SequenceNumber": "1"
            },
            {
               "Tender": {
                  "TenderType": "Cash",
                  "TypeCode": "Sale",
                  "Amount": "5.00",
                  "TenderChange": {
                     "Amount": "0.11"
                  }
               },
               "SequenceNumber": "2"
            }
         ]
      }
   }
}
```

### **6.0 USE CASE: Credit/Debit Tender**

Credit/Debit are different only in where the money comes from. In debit, it comes from the customer’s account directly. If credit, it comes from a loan from the credit card company

**Brief Description**

Customer selects one or more items and purchases them with a debit or credit card. Scenario Description Custoemr comes into the restaurant and orders a steak meal to go. He pays for it with his credit card.

Data

- Tender Type = Credit
- Type = Sale
- Tender Amount
- Credit Card Information
  - Card Type
  - Card Holder Name
  - Account Number
  - Expiration Date
- Authorization Information
  - Terminal where Transaction was Authorized 
  - Amount Authorized
  - Authorization Code
  - Provider who Authorized Transaction
  - Date Time of Authorization

**6.2 Conformance JSON Document - Credit Purchase without Cash Back**

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
                  "ExtendedAmount": "4.89",
                  "Quantity": "3"
               },
               "SequenceNumber": "1"
            },
            {
               "Tender": {
                  "TenderType": "CreditDebit",
                  "TypeCode": "Sale",
                  "Amount": "4.89",
                  "CreditDebit": {
                     "CardType": "Credit"
                  }
               },
               "SequenceNumber": "2"
            }
         ]
      }
   }
}
```

### **6.3 Scenario: Customer Tenders Purchase with Debit or Credit Tender with Cash Back (V2.1)**

**Brief Description**

Customer selects one or more items and purchases them with debit or credit card getting cash back. 

**Scenario Description**

Customer comes into the restaurant and orders a steak meal to go. He pays for it with his debit card and gets $10 in change

Data 

- Tender Type = Debit
- Type = Sale
- Tender Amount
- Credit Card Information
  - Card Type
  - Card Holder Name
  - Account Number
  - Expiration Date
- Authorization Information
  - Terminal where Transaction was Authorized
  - Amount Authorized
  - Authorization Code
  - Provider who Authorized Transaction
  - Date Time of Authorization
- Change Back to the Customer

 

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
                  "ExtendedAmount": "4.89",
                  "Quantity": "3"
               },
               "SequenceNumber": "1"
            },
            {
               "Tender": {
                  "TenderType": "CreditDebit",
                  "TypeCode": "Sale",
                  "Amount": "9.89",
                  "Cashback": "5.00",
                  "CreditDebit": {
                     "CardType": "Credit",
                  }
               },
               "SequenceNumber": "2"
            }
         ]
      }
   }
}
```

### **19.1 Scenario: Customer Tenders Co-Pay Purchase, i.e. Drug Purchase (V2.1)**

**Brief Description**

Customer selects one or more items and pays co-pay, instead of the total price, typically insurance picks up the remainder of the cost of the item(s).

**Data**

- Tender Type = Co-Pay
- Type = Sale
- Co-Pay Tender Amount
- Total Amount

**19.1 Conformance XML Instance Document - Co-Pay Tender**

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
                  "ExtendedAmount": "25.00"
               },
               "SequenceNumber": "1"
            },
            {
               "Tender": {
                  "TenderType": "Cash",
                  "TypeCode": "Sale",
                  "CoPayFlag": "true",
                  "Amount": "10.00",
                  "CoPay": {
                     "CoPayAmount": "10.00",
                     "TotalAmount": "25.00"
                  }
               },
               "SequenceNumber": "2"
            }
         ]
      }
   }
}
```

