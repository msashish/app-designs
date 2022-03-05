# All about SSL - Applicartion development point of view

    https://www.ibm.com/docs/en/ibm-mq/7.5?topic=ssl-how-tls-provide-authentication-confidentiality-integrity

    Certificate == public
    Private key == confidential and private


## Server Authentication (SSL encryption)

    This is quite common in web application, where we prefer secure/encrypted request via https traffic.
    In such a case, client will have to do a server authentication & encrypt their request.      
        - Client verifies server's authenticity, uses server's certificate (public) to encrypt and then send encrypted request to server.
        - Server will store privake key in its keystore and uses private key to decrypt the request. This is also called SSL termination.

    Things to be stored at server side (service provider):
        The personal certificate issued to the server by CA Y
        The server's private key        

    Things to be stored at client side (consumer):
        The CA certificate for CA Y


## Client Authentication 

    This is not that common, used when we want to limit clients accessing servers. Example in limiting Kafka consumer/producer clients.
    In such a case, server will have to do a client authentication.
        - If the SSL or TLS server requires client authentication, the server verifies the client's identity by verifying the client's digital certificate with the public key for the CA that issued the personal certificate to the client, in this case CA X .

    Things to be stored at server side (service provider):
         The CA certificate for CA X     

    Things to be stored at client side (consumer):
        The personal certificate issued to the client by CA X
        The client's private key  


## Server Authentication and Client Authentication 

    Case where you want secured encrypted interaction and allow only authenticated clients.
    Both the SSL or TLS server and client might need other CA certificates to form a certificate chain to the root CA certificate.

    Things to be stored at server side (service provider):
        The personal certificate issued to the server by CA Y
        The server's private key
        The CA certificate for CA X 

    Things to be stored at client side (consumer):
        The personal certificate issued to the client by CA X
        The client's private key
        The CA certificate for CA Y