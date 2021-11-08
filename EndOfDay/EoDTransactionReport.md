# End Of Day Transaction Report

# Overview

 

**Out of scope:**

- Cash tender amounts deemed out of scope. Therefor the cash reconciliation piece in the EOD is now out of scope. (View history to see its inclusion.)

 

## Context

## 5.9 Scenario: Store Open/Close – Business EOD (V6.0)

**Brief Description**

![](..\img\Eod.png)

Control Transactions are events used to report the change of state of various systems in the retail store.

- Business SOD/EOD – reports the opening or closing of the store for business for selling. 
- POS SOD/EOD – reports a particular POS is ready to begin the selling operations. Start of Day or End of Day. Depending on business rules, this can occur for one POS or for all POS’s at one time. 
- POS Startup/Restart/Shutdown – reports when the POS has powered up, restarted, or shutdown. If one reports the POS SOD on this POS then the order is reversed in the drawing. 
- TillSOD/Movement/EOD – reports the insertion, movement and removal of the till into the cash drawer.
- Operator Sign on/Signoff – now the POS is ready to begin selling, the operator signs onto the POS to begin selling. Can also be used to report time punch information. 
- Operator Lock/Unlock/Auto-Signoff – reports the state of the POS when the operator leaves the POS to help a customer
- Day Part Start/End – in foodservice sales can be recorded by day part (breakfast, lunch, or dinner). This reports the start and end of those time periods. 
- Shift Start/End – reports the beginning and ending of particular shifts. In foodservice there are associates who work shifts as well as associates who work day parts. Both day parts and shifts can be used in either retail or foodservice.

**5.9 Conformance JSON Document: Business EOD**

```json
{
   "Transaction": {
      "BusinessUnit": {
         "UnitID": {
            "TypeCode": "RetailStore",
            "ID": "12"
         }
      },
      "WorkstationID": {
         "TypeCode": "POS",
         "ID": "5"
      },
      "SequenceNumber": "350",
      "OperatorID": {
         "OperatorName": "John",
         "OperatorType": "Cashier",
         "ID": "205"
      },
      "ControlTransaction": {
         "BusinessEOD": {
            "StartDateTimestamp": "2012-11-11T20:20:20",
            "EndDateTimestamp": "2011-11-11T20:20:20",
            "TillID": "23",
            "OpenBusinessDayDate": "2012-02-20",
            "CloseBusinessDayDate": "2012-02-19",
            "SessionSettle": {
               "TransactionCount": 160,
               "TotalNetSalesAmount": 19888,
               "TotalNetReturnAmount": 0,
               
               /* Start: Corum Custom Field: GSTBreakdown */
               "GSTBreakdown": {
                "Account Sales": {
                  "Taxable": 1300,
                  "NonTaxable": 300,
                  "Tax": 130.00
                },
                "Non Account Sales": {
                  "Taxable": 1300,
                  "NonTaxable": 300,
                  "Tax": 130.00
                },
                "Stock Transfers": {
                  "Taxable": 1300,
                  "NonTaxable": 300,
                  "Tax": 130.00
                },
                "Stock Transfers Excluded From Sales": {
                  "Taxable": 1300,
                  "NonTaxable": 300,
                  "Tax": 130.00
                },
                "Total": {
                  "Taxable": 1300,
                  "NonTaxable": 300,
                  "Tax": 130.00
                },
               }
               /* End: Corum Custom Field: GSTBreakdown */
               
               /* Start: Corum Custom Field: LayBy */
               "LayBy": {
                "ForfeitedLaybyDeposits": 0.00,
                "Deposits": 0.00,
                "Payments": 0.00,
                "Cancelled": 0.00,
                "TotalNetLayByAmount": 0.00
               }
               /* Start: Corum Custom Field: LayBy */
               
               /* Start: Corum Custom Fields Totals*/
               "TotalJournalAdjustments": 0,
               "TotalGovernmentRecovery": 0,
               "TotalGovernmentIncentives": 0,
               "TotalCostOfGoodsSold": 0,
               "TotalLaybyDepositsForfeited": 0,
               "TotalGrossProfit": 0,
               /* End: Corum Custom Fields Totals */
               
               "TotalTaxAmount": 130,
               "TenderSummary": {
                  "Beginning": {
                     "TenderType": "Cash",
                     "Total": {
                        "Amount": 2000
                     }
                  },
                  "Sales": [
                  {
                     "TenderType": "Cash",
                     "Total": {
                        "Amount": 2000
                     }
                  },
                  {
                     "TenderType": "CreditDebit",
                     "Total": {
                        "Amount": 2000
                     },
                     "CardTypes": [
                      {
                        "CardType": "American Express",
                        "Total":
                        {
                          "Amount": 1000
                        }
                      },
                      {
                        "CardType": "Debit",
                        "Total":
                        {
                          "Amount": 1000
                        }
                      },
                      {
                        "CardType": "Mastercard",
                        "Total":
                        {
                          "Amount": 1000
                        }
                      },
                      {
                        "CardType": "Visa",
                        "Total":
                        {
                          "Amount": 1000
                        }
                      }
                     ]
                  }
                  ],
                  "Returns": [{
                     "TenderType": "Cash",
                     "Total": {
                        "Amount": 2000
                     }
                  }],
                  "PaidIn": {
                     "TenderType": "Cash",
                     "Total": {
                        "Amount": 2000
                     }
                  },
                  "PaidOut": {
                     "TenderType": "Cash",
                     "Total": {
                        "Amount": 2000
                     }
                  },
                  "Loan": {
                     "TenderType": "Cash",
                     "Total": {
                        "Amount": 2000
                     }
                  },
                  "Pickup": {
                     "TenderType": "Cash",
                     "Total": {
                        "Amount": 2000
                     }
                  },
                  "Deposit": {
                     "TenderType": "Cash",
                     "Total": {
                        "Amount": 2000
                     }
                  },
                  "Ending": {
                     "TenderType": "Cash",
                     "Total": {
                        "Amount": 2000
                     }
                  }
               },
            },
            "LastTransactionSequenceNumber": "350"
         }
      }
   }
}
```

Definitions:

 

| **Field**            | **Definition**                                               |
| -------------------- | ------------------------------------------------------------ |
| TransactionCount     |                                                              |
| TotalNetSalesAmount  | The total value of all sales (net of returns) performed at the Till |
| TotalNetReturnAmount | The total value of all returns performed at the till         |
| TotalTaxAmount       | including full- and half taxes independent of state, county or city taxes |
| GrossPositiveAmount  | The sum of the monetary value for all tenders put into the Till |
| GrossNegativeAmount  | The sum of the monetary value for all tenders taken from the Till |
| Refunds              | The monetary value of the sum of all refunds taken from the Till |