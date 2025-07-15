**HTTP** 
- It is a set of rules/protocol which should be followed for data communication.
- Browser uses https to communicate with the server which hosts the website.

**Methods**
- Get 
- Post 
- Put
- Delete

**HTTPS**
- We use this for its security and Encryption
- Uses SSL or TLS protocol

**API**
- An **API** defines **how software components should interact**.
- API's are the set of rules in the backend
- Web API: REST API, GraphQL (used over the internet using HTTP)
- These are like the intermediate between the server and you system.
- They fetch the things you request in the server and sends it back to you. 

**Rest API**
- A Rest API lets the client talk to server using http with methods.
- A style of API that uses HTTP with rules (like resources, statelessness, JSON, etc.)

**Sample HTTP request**
```
GET /current?city=Chennai HTTP/1.1
Host: api.weather.com

```
**Response**
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "city": "Chennai",
  "temperature": "34°C",
  "status": "Sunny"
}
```

## API is like the backend logic that responds by HTTP methods (like GET, POST) to share or retrieve data from the server.###


**Load Balancing**
- When in horizontal scaling a server crashes so we have to use another server it determines which to use next.

For applications like live chating, gaming using http is inefficient as it only request\response at a time leading to a single way communication.
so when we need a  two way communication we have to **Web Sockets**

**Web Sockets**
- A **WebSocket** is a **communication protocol** that provides **full-duplex** (two-way) communication between the **client** (browser or app) and the **server** over a **single, long-lived connection**.

