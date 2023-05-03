# PeerToPeer_Broadcast
Peer-to-peer messaging and broadcast message
Introduction
This project involves building a client and a server application that allows client-to-client communication, excluding a server. The server application will only be used to share contact information about active clients. Clients can connect to the server, authenticate themselves using a password, and see the active client list. They can choose any active client to connect with, and the remote client will be asked to approve the new connection. Once a connection is successful, clients can send messages between themselves without the server. Besides that, a client can request the server to broadcast a message to every client in the csv file. All clients who will be active within 30 mins should receive the broadcast message.


Server Application
The server application will listen to port 4400 and allow at least 50 connections simultaneously. The server tasks are listed below:
* Create socket: It will create a TCP and UDP socket. TCP socket to communicate over clients and UDP socket to broadcast messages.
* It will use port 4400 and at least allow 50 connections at a time, using either multiprocessing/multithreading.
* If there are more than 50 connections at some time, TCP will ignore the new connections, and clients will retry (automatically) at least 5 more times in the next 10 minutes.


Client Connection to the Server
* Once the client connects to the server, the server will respond with a question with login/signup.
* If the client chooses signup, the server will reply back asking new username and password (asked twice, including confirming the password).
* The server then replies to clients to log in and asks for the username and password.
* If the client chooses login, then the server will ask for the username and password.
* If the authentication passes, the server will allow the client with two options: list of active clients or broadcast a message.


List of Active Clients
* The server will show all active clients (only client username and IP address).
* The client can request the server to let connect to one of the clients by typing their IP address.
* If that is a valid request, a peer-to-peer connection will be open between clients.
* Otherwise, the server will penalize the client by terminating their connection.
<img width="468" alt="image" src="https://user-images.githubusercontent.com/127074287/235826162-8e803ddf-0df8-44d8-a29a-0f56b6bfd6eb.png">
<img width="468" alt="image" src="https://user-images.githubusercontent.com/127074287/235826176-62c94334-84cf-4f3e-a32a-cfb5a5879e53.png">


Broadcast a Message
* If a client chooses to broadcast a message, the server will use its UDP socket to broadcast the message.
* The server asks the client to type the message and then broadcast it on behalf of the client.
* The broadcast message, by default, will include the sender's information (client username) and date/time (broadcast).
* The server will keep broadcast messages for up to 30 mins. After that, the broadcast will be dropped.
<img width="468" alt="image" src="https://user-images.githubusercontent.com/127074287/235826189-3489e04d-3da9-44e1-a05c-d3b9ba2a9dec.png">
<img width="468" alt="image" src="https://user-images.githubusercontent.com/127074287/235826200-af254392-3dc6-43a3-b460-4cfdd5115f0e.png">


Running Server and Client
* To run the server application , we need to compile the file using g++ compiler and run the following command. ì g++ server.cpp -o server -pthread î
* Server can be started by running the following command. ì ./server î
* To run the client application, we need to compile the file using g++ compiler and run the following command. ìg++ client.cpp -o client  -pthread î
* Client can be started by running the following command. ì ./client <IP address> <port> î.

Libraries Used
* #include <arpa/inet.h>
* #include <netinet/in.h>
* #include <unistd.h>
* #include <pthread.h>
* #include <iostream>
* #include <cstring>
* #include <string.h>
* #include <cstring>
* #include <unistd.h>
