# Chat Application design

## High level design of whatsapp

    https://www.cometchat.com/blog/whatsapps-architecture-and-system-design
    https://www.codekarle.com/system-design/Whatsapp-system-design.html 

### High level components:

    - Gateway/box
    - Parser service (Parse a unformatted message from gateway and pass it to Session service)
    - Session Service (Authentication; Mapping of user to gateway id; Routes service to gateway)
    - Group Service (Mapping of group id to user Id; Acts as router)
    - Last Seen Service (DB: Cassandra cluster)
    - Message/Task queues
    - User profile service (DB: MySQL)
    - Each service to have a DB 


    Clients --> Gateway --> Session Service --> Group Service --> Message queue --> Gateway --> Clients

### Key points

    1) Websocket or TCP is used when server has to send message to client. HTTP is used when client has to send a request/message to server. WhatsApp uses a highly modified version of XMPP on an Ejabberd server.

    2) The XMPP on the client opens an SSL socket to the WhatsApp servers. All the sent messages are queued on the servers until the client opens or reconnects to this socket to retrieve the messages. Once a message is successfully retrieved by the client, a success status is sent back to the WhatsApp server. The server then forwards this status to the original sender; letting them know that the message was received by adding the “checkmark” icon next to the successfully sent message.

    3) WhatsApp’s encryption technology is called Signal Encryption Protocol, which was developed by Open System Whispers to be a modern, open-source, strong encryption protocol for asynchronous messaging systems.

    4) WhatsApp's choice of programming language is Erlang. Erlang is a functional programming language that is oriented towards building concurrent, scalable, and reliable systems.
    
    5) Backend OS is FreeBSD and not Linux
    when it comes to raw performance, especially in regards to system load per packet, no other operating system can beat FreeBSD. 

    6) To handle message routing, deliverability, and general instant messaging aspects of the app, Whatsapp uses Ejabberd.
    Ejabberd is an open-source XMPP server that is written in Erlang. WhatsApp uses a modified version of XMPP as its protocol for handling message delivery.


## System design of Chat App

    https://bytebytego.com/courses/system-design-interview/design-a-chat-system


### Possible Approaches for server-initiated connection

    Since HTTP is client-initiated and stateless (plus not bi-directional), it is not trivial to send messages from the server. Techniques are used to simulate a server-initiated connection: 
    
    1) Polling
        Client periodically asks the server if there are messages available
    
    2) Long polling
        Client holds the connection open until there are actually new messages available or a timeout threshold has been reached. Once the client receives new messages, it immediately sends another request to the server, restarting the process.
    
   3)  WebSocket
        WebSocket connection is initiated by the client. It is bi-directional and persistent. It starts its life as a HTTP connection and could be “upgraded” via some well-defined handshake to a WebSocket connection.



### Detailed design

    - We shall use WebSocket for both client-initiated and server-initiated connections
    - Storage: There are two categories of data
        Relational data: User profile, group, settings, friend list. Use Relational DB.
        Chat history: Textual. Use Key Value stores.
            


### Learnings

    - HTTP keep-alive header allows a client to maintain a persistent connection. Reduces number of TCP handshakes.
    - 