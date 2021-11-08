# Reports/Reconcilliations/Displays

Any messages around here that should be crafted, how can I direct the messages to print either of the POS or the terminal?

Can any of these reports be triggered by the device?

Which is more common, pos reciept printer or terminal?

The SDK contains some logic:

```json
        // Sending some reports.. Where do I send parameters? e.g. the acquirer?
        await client.SendAsync(new ReconciliationRequest(ReconciliationType.AcquirerReconciliation));
        await client.SendAsync(new ReconciliationRequest(ReconciliationType.InternalReconciliation)); // Without closing current period. Implies there is a close function?
        await client.SendAsync(new ReconciliationRequest(ReconciliationType.PreviousReconciliation));
        await client.SendAsync(new ReconciliationRequest(ReconciliationType.SaleReconciliation));     // Is this the only way to close the current period?
        await client.SendAsync(new ReconciliationRequest(ReconciliationType.Unknown));

        // What does this display request do?
        await client.SendAsync(new DisplayRequest());
```

Importnat ones:

- SalesReconcilliation
- PreviousReconcilliation

 

DMG to check about Shift Total.

- Going to be a sales reconcilliation
- Can do end of day per terminal
- All in nexo format, check DMGs documentation
- Important if they do standalone transactions, and miss-keyed.

 

From Nexo:

- No way to get end of day numbers for other terminals.

 

Display requests:

- Shows current status, awaiting card, awaiting pin, we recieve these as a stream, whent he payment request is open.
- DMG wraps a displayRquest to saleToPoiRequest. Designed this way by nexo.