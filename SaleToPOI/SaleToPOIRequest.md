# SaleToPOIRequest

Examples of SaleToPOIRequest Implementations:

- Adyen:  https://docs.adyen.com/point-of-sale/make-a-payment
- DataMesh: https://datameshgroup.github.io/fusion/#getting-started-design-your-integration-receipt-printing

Official Nexo Standard:  https://www.nexo-standards.org/

 

High level design:

![](..\img\SaleToPOI_HLSD.png)

![](..\img\SaleToPOI_Flow.png)

Datamesh Interface:

- Listens to the queue with session empty (i.e. retrieves and locks the first inbound session.)
- Passes this off to a service who:
  - Subscribes to the session
  - Opens a websocket to datamesh
  - Validates, Transforms & Forwards Messages back and forth