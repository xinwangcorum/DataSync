# DataSync Documentation

### Content

[Header](MessageHeader/Header.md)

[Catalog Maintenance](CatalogMaintenance/CatalogMaintenance.md)

[Retail Transaction](RetailTransaction/RetailTransaction.md)

- [Tender Line Items](RetailTransaction/TenderLineItems.md)
- [Tender Rounding](RetailTransaction/TenderRounding.md)
- [Return](RetailTransaction/Return.md)
- [Tax](RetailTransaction/Tax.md)
- [CoPay](RetailTransaction/CoPay.md)

[End of Day Transaction Report](EndOfDay/EoDTransactionReport.md)

[Inventory](Inventory/Inventory.md)

- [Inventory Action](Inventory/InventoryAction.md)

[SaleToPOI](SaleToPOI/SaleToPOIRequest.md)

- [Login/Logout Request](SaleToPOI/LoginLogout.md)
- [Payment Request](SaleToPOI/Payment.md)
- [Payment Refund](SaleToPOI/PaymentRefund.md)
- [Cancel Transaction](SaleToPOI/CancelTransaction.md)
- [Verify Transaction](SaleToPOI/VerifyTransactionStatus.md)
- [Reports/Reconcilliations/Displays](SaleToPOI/ReportsReconcilliationsDisplays.md)



### Contact Catalogue

| Contract | Current Version | Direction | Contract Purpose | Field Guide |
| --- | --- | --- | --- | --- |
| RetailTransaction | RC1 | POS -> PharmX | - Sales - Returns | https://www.omg.org/retail-depository/arts-odm-73/ |
| InventoryControlTransaction | RC1 | POS -> PharmX | - Store Transfer - Store Goods Receipt - Breakage - Spoilage - Return to Vendor - Order | https://www.omg.org/retail-depository/arts-odm-73/ |
| InventoryAction | RC1 | POS → PharmX | - InventoryUpdate |  |
| Price Rules (Aka Deals, Aka Promotions, Aka Supplier Deals, Aka Supplier Promotions) | RC1 | PharmX → POS | - Publish Price | https://www.omg.org/retail-depository/arts-odm-73/ |
| Item | RC1 | PharmX → POS | - AddItem - UpdateItem - DeleteItem | https://www.omg.org/retail-depository/arts-odm-73/ |
| ControlTransaction | RC1 | POS -> PharmX | - Business End of Day - Till End of Day | https://www.omg.org/retail-depository/arts-odm-73/ |
| SaleToPOIRequest | RC1 | POS -> PharmX | - PaymentRequest *AbortRequest *TransactionStatusRequest - PaymentResponse - ReversalRequest | https://www.omg.org/retail-depository/arts-odm-73/ |
| RetailTransaction | RC1 | POS -> PharmX | - Sales - Returns | https://www.omg.org/retail-depository/arts-odm-73/ |
