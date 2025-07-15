**Local Host:**
- It is like calling yourself from your home.
- It does not query a DNS server(No lookup) and get back the website from the server unlike other websites
- local host  is mapped to `127.0.0.1` - Predefined IP address.

**Domain Name System**
- DNS translates human-readable domain names (like `www.google.com`) into IP addresses (like `142.250.195.78`) that computers use to identify each other.
- It is used when fetching the web we are looking for.

**IP Address** 
- A unique address for every device which is connected to the internet.
- what is the diff between the IPv4 and IPv6. IPv4 only have 4.3 billion unique addresses.
- IPv6 have 340 undecillion unique addresses.

**What is happening when browsing**
- You type www.google.com in the browser.
- The browser asks the DNS system to find the IP address.
- DNS resolves the domain into an IP address (like 142.250.195.78).
- Using that IP, your browser sends a request to the actual web server.
- The web server responds with the website content, and you see the page.


**1. Client–Server Architecture**  
A model where the client requests services and the server provides them.  
The client is usually a browser or app; the server handles logic and data.  
This separation allows scalability and reusability.

---

**2. IP Address**  
An IP address uniquely identifies a device on a network.  
It acts like a digital address that lets computers find each other.  
Every server on the internet has one.

---

**3. DNS (Domain Name System)**  
DNS maps domain names (like google.com) to IP addresses.  
It’s like the phonebook of the internet.  
Without it, we’d need to remember numbers instead of names.

---

**4. Proxy / Reverse Proxy**  
A proxy sits between the client and server, often for security or filtering.  
A reverse proxy hides backend servers and distributes traffic.  
Useful for load balancing, caching, and SSL termination.

---

**5. Latency**  
Latency is the time it takes for data to travel from client to server.  
It depends on distance, network quality, and processing time.  
Lower latency = faster user experience.

---

**6. HTTP / HTTPS**  
HTTP is the protocol used for web communication.  
HTTPS is the secure version, using SSL/TLS encryption.  
It enables communication between browsers and servers.

---

**7. API (Application Programming Interface)**  
An API lets clients talk to servers in a structured way.  
It defines rules for sending/receiving data (like JSON).  
APIs hide the backend complexity from the user.

---

**8. REST API**  
REST is an API style that uses HTTP methods like GET, POST, PUT, DELETE.  
It treats everything as a resource, accessed via URLs.  
Stateless and easy to scale, making it very popular.

---

**9. GraphQL**  
GraphQL is an alternative to REST with flexible queries.  
The client asks for exactly the data it needs.  
It reduces over-fetching and under-fetching.

---

**10. Databases**  
Databases store and organize data for quick access.  
They support CRUD operations: Create, Read, Update, Delete.  
Can be relational (SQL) or non-relational (NoSQL).

---

**11. SQL vs NoSQL**  
SQL databases use structured schemas and support joins.  
NoSQL is flexible, scalable, and works well with unstructured data.  
Choose based on your app’s consistency and scaling needs.

---

**12. Vertical Scaling**  
Add more power (CPU, RAM) to a single server.  
It’s simple but has physical and cost limits.  
Often used in early-stage systems.

---

**13. Horizontal Scaling**  
Add more servers to handle increased load.  
It improves redundancy and fault tolerance.  
Better for systems that expect high traffic.

---

**14. Load Balancer**  
Distributes incoming traffic across multiple servers.  
Helps prevent any one server from overloading.  
Improves performance and uptime.

---

**15. Database Indexing**  
An index is like a book’s table of contents for quick lookup.  
It speeds up search queries dramatically.  
But it uses extra storage and needs updates.

---

**16. Replication**  
Replication copies data from one main database to others.  
Improves read performance and provides backups.  
Used for fault tolerance and high availability.

---

**17. Sharding**  
Sharding splits a large database into smaller parts called shards.  
Each shard holds part of the data, improving performance.  
It’s great for large-scale systems.

---

**18. Vertical Partitioning**  
Split a wide table into multiple tables by column groups.  
Each smaller table handles a specific use case or module.  
Improves performance and reduces unused data access.

---

**19. Caching**  
Caching stores frequently-used data in memory (e.g., Redis).  
It reduces load on the database and speeds up responses.  
Critical for performance in high-traffic systems.

---

**20. Denormalization**  
Storing redundant data to avoid expensive joins.  
It improves read speed but increases write complexity.  
Often used in read-heavy systems.

---

**21. CAP Theorem**  
You can’t have Consistency, Availability, and Partition Tolerance all at once.  
In a network failure, you must choose: C + P or A + P.  
Understand trade-offs when designing distributed systems.

---

**22. Blob/Object Storage**  
Used for storing large binary files like images, videos, backups.  
Services like AWS S3 are examples of object storage.  
It’s scalable, cheap, and good for static content.

--- 

**23. CDN (Content Delivery Network)**  
A CDN caches content at edge locations closer to users.  
It reduces latency and offloads traffic from your main server.  
Used for static assets like images, videos, and scripts.

---

**24. WebSockets**  
WebSockets enable two-way, real-time communication over a single connection.  
Unlike HTTP, the server can also push data to the client.  
Used in chat apps, games, stock tickers, etc.

---

**25. Webhooks**  
A webhook lets one server send real-time updates to another.  
Used for event-driven actions (e.g., payment success notification).  
The receiver must have a public endpoint to accept it.

---

**26. Microservices**  
Break a big app into small, independent services.  
Each service handles one feature and runs independently.  
Helps scale teams and services better than monoliths.

---

**27. Message Queues**  
A queue holds tasks to be processed asynchronously.  
Helps decouple services and avoid system overload.  
Popular tools include RabbitMQ, Kafka, AWS SQS.

---

**28. Rate Limiting**  
Restricts how many requests a user/client can make in a time frame.  
Protects APIs from abuse or accidental overload.  
Algorithms include fixed window, sliding window, and token bucket.

---

**29. API Gateway**  
Sits in front of your microservices as a single entry point.  
Handles routing, rate-limiting, authentication, and logging.  
Makes your architecture cleaner and more secure.

---

**30. Idempotency**  
A request is idempotent if repeating it gives the same result.  
Important for retries (e.g., charging a card once only).  
Ensures safe API behavior under network failures.