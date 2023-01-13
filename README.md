# Microservices_Tutorial

🙂 You can find the GitHub Repo (Kindly run npm install in Order, Payment, and API-Gateway directories before running) Here. We have two services Order and Payment with API Gateway.

NodeJS_Microservices

---> Order

------> server.js (Running on PORT 8081)

---> Payment

------> server.js (Running on PORT 8082)

---> API-Gateway

------> server.js (Running on Port 9091)
    
Whenever a client makes a request to the API-Gateway, We have defined some routes (Using prefixes) that redirect the request to the appropriate service (Depends which route is called). Payment and Order services are independent means If one fails other will not be affected.

Also we can add Auth or Middlewares so that no one can call the services directly or without Authentication. We have implemented a very basic architecture.

Now, we can start the services including the gateway

Terminal running microservices

📍 And we can request http://localhost:9001/order Or http://localhost:9001/payment
