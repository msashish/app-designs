## Useful links and key notes

### Youtube video Martin Fowler – Microservices
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