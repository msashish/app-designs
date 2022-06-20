## Useful links and key notes

## Basics of request-response pattern and Event based

    https://www.kai-waehner.de/blog/2020/05/25/api-management-gateway-apache-kafka-comparison-mulesoft-kong-apigee/

### Request-response pattern

    - Provides point to point messaging
    - Suitable for synchronous integration use cases
    - Not suitable when request continuously flows in (like a stream). 
        REST / SOAP web services do not provide characteristics to build a scalable, reliable real time infrastructure for a high throughput of events.
    - Technologies: HTTP, REST/SOAP, gRPC

### Event based pattern

    - Provides Messaging / Pub Sub (sending data from A to B and C)
    - Suitable when request continuously flows in (continuous data processing)
    - Often asynchronous 
    - Event-driven, supporting patterns like Event Sourcing and CQRS (command Query request segregation)
    - Technologies: Kafka, MQ, PubSub


## Youtube video Martin Fowler – Microservices
    https://www.youtube.com/watch?v=2yko4TbC8cI

    - Microservices thinks interms of breaking Application into components. 
        Idea of benefit is that a component can be replaced or thrown away if required without affecting other components.
    - Smart endpoints and dumb pipes
        SOA has systems that communicate with very smart middleware/infrastructure area (ESB - enterprise bus). The smart pipes figure out how to communicate.
        In Microservices the network / communication is dumb and intelligence is moved to end points. This is how microservices differ from SOA
    - Decentralised decision making
        Monoliths has 1 database for entire Application. 
        Microservice and SOA mandates each service gets its own database and they cannot be shared.
    - Design for failure
        Being ready for failure
        Netflix has chaos monkey that goes around and randomly brings down services