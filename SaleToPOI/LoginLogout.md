# Login/Logout Request

Login Request:

| Attribute                                                    | Requ. | Format | Description                                                  |
| ------------------------------------------------------------ | ----- | ------ | ------------------------------------------------------------ |
| [DateTime](https://datameshgroup.github.io/fusion/#data-dictionary-datetime) | ✔     | String | Current Sale System time, formatted as [ISO8601](https://en.wikipedia.org/wiki/ISO_8601) DateTime. e.g. "2019-09-02T09:13:51.0+01:00" |
| **SaleSoftware**                                             | ✔     | Object | Object containing Sale System identification                 |
| [ProviderIdentification](https://datameshgroup.github.io/fusion/#data-dictionary-provideridentification) | ✔     | String | The name of the company supplying the Sale System. Provided by DataMesh. |
| [ApplicationName](https://datameshgroup.github.io/fusion/#data-dictionary-applicationname) | ✔     | String | The name of the Sale System application. Provided by DataMesh. |
| [SoftwareVersion](https://datameshgroup.github.io/fusion/#data-dictionary-softwareversion) | ✔     | String | The software version of the Sale System. Must be the software version of the current build. |
| [CertificationCode](https://datameshgroup.github.io/fusion/#data-dictionary-certificationcode) | ✔     | String | Certification code for this Sale System. Provided by DataMesh. |
| **SaleTerminalData**                                         | ✔     | Object | Object containing Sale System configuration                  |
| [TerminalEnvironment](https://datameshgroup.github.io/fusion/#data-dictionary-terminalenvironment) | ✔     | String | "Attended", "SemiAttended", or "Unattended"                  |
| [SaleCapabilities](https://datameshgroup.github.io/fusion/#data-dictionary-salecapabilities) | ✔     | Array  | Advises the POI System of the Sale System capabilities. See [SaleCapabilities](https://datameshgroup.github.io/fusion/#data-dictionary-salecapabilities) |
| [TotalsGroupId](https://datameshgroup.github.io/fusion/#data-dictionary-totalsgroupid) |       | String | Groups transactions in a login session                       |
| [OperatorLanguage](https://datameshgroup.github.io/fusion/#operatorlanguage) |       | String | Operator language. Set to 'en'                               |
| [OperatorId](https://datameshgroup.github.io/fusion/#data-dictionary-operatorid) |       | String | Groups transactions under this operator id                   |
| [ShiftNumber](https://datameshgroup.github.io/fusion/#data-dictionary-shiftnumber) |       | String | Groups transactions under this shift number                  |
| [POISerialNumber](https://datameshgroup.github.io/fusion/#data-dictionary-poiserialnumber) |       | String | The POISerialNumber from the last login response, or absent if this is the first login |

```json
{
   "SaleToPOIRequest":{
      "MessageHeader":{
         "ProtocolVersion":"3.1",
         "MessageClass":"Service",
         "MessageCategory":"Login",
         "MessageType":"Request",
         "ServiceID":"xxx",
         "SaleID":"xxx",
         "POIID":"xxx"
      },
      "LoginRequest":{
         "DateTime":"xxx",
         "SaleSoftware":{
            "ProviderIdentification":"xxx",
            "ApplicationName":"xxx",
            "SoftwareVersion":"xxx",
            "CertificationCode":"xxx"
         },
         "SaleTerminalData":{
            "TerminalEnvironment":"xxx",
            "SaleCapabilities":[
               "xxx",
               "xxx",
               "xxx"
            ],
            "TotalsGroupID":"xxx"
         },
         "OperatorLanguage":"en",
         "OperatorID":"xxx",
         "ShiftNumber":"xxx",
         "POISerialNumber":"xxx"
      }
   }
}
```

Logout Request:

| Attribute                                                    | Requ. | Format  | Description                                                  |
| ------------------------------------------------------------ | ----- | ------- | ------------------------------------------------------------ |
| [MaintenanceAllowed](https://datameshgroup.github.io/fusion/#data-dictionary-maintenanceallowed) |       | Boolean | Indicates if the POI Terminal can enter maintenance mode. Default to true if not present. |

```json
{
   "SaleToPOIRequest":{
      "MessageHeader":{
         "MessageClass":"Service",
         "MessageCategory":"Logout",
         "MessageType":"Request",
         "ServiceID":"xxxx",
         "SaleID":"xxx",
         "POIID":"xxx"
      },
      "LogoutRequest":{
         "MaintenanceAllowed":"true or false"
      },
      "SecurityTrailer":{...}
   }
}
```

