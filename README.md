# Microservices_Tutorial

🙂 You can find the GitHub Repo (Kindly run npm install in Order, Payment, and API-Gateway directories before running) Here. We have two services Order and Payment with API Gateway.

NodeJS_Microservices
|
---> Order
|
------> server.js (Running on PORT 8081)
|
---> Payment
|
------> server.js (Running on PORT 8082)
|
---> API-Gateway
|
------> server.js (Running on Port 9091)
    
    🙂 Whenever a client makes a request to the API-Gateway, We have defined some routes (Using prefixes) that redirect the request to the appropriate service (Depends which route is called). Payment and Order services are independent means If one fails other will not be affected.

🔥 Also we can add Auth or Middlewares so that no one can call the services directly or without Authentication. We have implemented a very basic architecture.

Order Server.js
const express = require("express");
const app = express();

const port = 8081;
app.get("/order-list", (req,res)=>{
    let response = {
        data: {
            item: [
                {
                    id: 1,
                    name: 'order-1'
                },
                {
                    id: 2,
                    name: 'order-2'
                }
            ]
        }
    };
    res.status(200).json(response);
});
app.get("/", (req,res)=>{
    res.send("Order called");
});

app.listen(port, ()=>{
    console.log("Listening at localhost "+ port);    
})


Payment server.js
const express = require("express");
const app = express();

const port = 8082;
app.get("/payment-list", (req,res)=>{
    let response = {
        data: {
            item: [
                {
                    id: 1,
                    name: 'Payment-1'
                },
                {
                    id: 2,
                    name: 'Payment-2'
                }
            ]
        }
    };
    res.status(200).json(response);
});

app.get("/", (req,res)=>{
    res.send("Payment called");
});

app.listen(port, ()=>{
    console.log("Listening at localhost "+ port);    
})


API-Gateway
const gateway = require("fast-gateway");

const port = 9001;
const server = gateway({
    routes: [
        {
            prefix: "/order",
            target: "http://localhost:8081/",
            hooks: {}
        },
        {
            prefix: "/payment",
            target: "http://localhost:8082/",
            hooks: {}
        }
    ]
});

server.get('/mytesting', (req,res)=> {
    res.send("Gateway Called");
})

server.start(port).then(server=>{
    console.log("Gateway is running "+port);
})

😌 Now, we can start the services including the gateway

Terminal running microservices

📍 And we can request http://localhost:9001/order Or http://localhost:9001/payment
