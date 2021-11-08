# **Message Header**

The transaction header helps the network with routing requests, and  informing appropriate parties. Nested in this, POS Transactions, have a  shared set of POS transaction headers as well. (e.g. Operator,  BusinessDayDate etc.)

At a high level the Message header and Transaction header contains:

| **Field**                       | **Type**               | **Mandatory/Optional** | **Description**                                              |
| ------------------------------- | ---------------------- | ---------------------- | ------------------------------------------------------------ |
| MessageID                       | string                 | Mandatory              | A unique identifier for the transaction                      |
| MessageDateTime                 | DateTime               | Mandatory              | Indicates the UTC time when the message is created           |
| MessageType                     | string                 | Mandatory              | Indicates the contract contained within                      |
| MessageDirection                | string                 | Mandatory              | Indicate the direction of the Message                        |
| InitiatingBusinessUnit          | object<BusinessUnit>   | Optional               | Indicates the business that initiated the transaction        |
| OriginatingBusinessUnit         | object<BusinessUnit>   | Optional               | Indicates the business unit, that emitted the message, which may be different to the initiator, in the event of delegated authorisation. |
| DestinationBusinessUnit         | object<BusinessUnit>   | Optional               | Indicates the business that should recieve a copy of the message. an Id of * indicates, that all eligible participants should recieve a copy. |
| NotifiedBusinessUnits           | object<BusinessUnit>[] | Optional               | The notified recipient will see the target recipient is not them. |
| **Request**                     | **Object**             | Optional               | Indicates the message may require at least a response        |
| **Response**                    | **Object**             | Optional               | If responding to a prior RequestId.                          |
| **RetailTransaction**           | **Object**             | Optional               | One of the potential message payload                         |
| **CatalogMaintenance**          | **Object**             | Optional               | One of the potential message payload                         |
| **ControlTransaction**          | **Object**             | Optional               | One of the potential message payload                         |
| **Price**                       | **Object**             | Optional               | One of the potential message payload                         |
| **InventoryControlTransaction** | **Object**             | Optional               | One of the potential message payload                         |
| **InventoryAction**             | **Object**             | Optional               | One of the potential message payload                         |
| Telemetry                       | Object                 | Optional               | For performance analysis                                     |

 

### JSON Example

```json
{
    "MessageId": "B0AF5655-C5A1-4713-8963-44362C0DEA33",
    "MessageType": "RetailTransaction",
    "InitiatingBusinessUnit": {
        "ID": "112.1",
        "Name": "SampleStore"
    },
    "OriginatingBusinessUnit": {
        "ID": "112",
        "Name": "SampleStore"
    },
    "DestinationBusinessUnit": {
        "ID": "113",
    },
    "NotifiedBusinessUnits": [{
        "ID": "113",
        "Name": "HeadOffice"
    }],
    "Response": {
      "RequestID": "D0BF5623-D6A1-4713-8963-44312C0DEA44"
    },
    "RetailTransaction": {
          <!-- Transaction Header Here -->
          "BusinessDayDate": "2019-11-12",
          "DateTime": "2021-05-11T07:13:25.143",
          "Operator": {
              "ID": "1",
              "Name": "John"
          },
          "TrainingModeFlag": false,
          "WorkstationID": "?",
          <!-- Transaction Message Here -->
    },
}
```

