## UNMANAGED Services

![[Pasted image 20250807094745.png]]

EC2 is  a unmanaged AWS service which only provides physical infrastructure, but you're responsible for setting up, securing, and maintaining the operating system, network configurations, and applications on your instances. 


**Lambda**
It is a serverless service which automatically executes the  code as when a specific condition like file upload or user action.
Example: 
- Real-time event handling for an online game
- A gaming company uses Lambda to handle in-game events like player actions, game state changes, and real-time leader board updates. Each event (like scoring a point or unlocking an achievement) triggers a Lambda function that updates player data and game status.

## **Containers and Orchestration**

**Containers** provide a consistent environment across different devices.
- Containers provide a reliable way to package your application’s code and dependencies into a single, portable unit, making them ideal for workflows that require high security, reliability, and scalability.



Orchestration:
- As a application scales more containers is required so to manage these containers **Orchestration** comes handy 
- They manage the life cycle.

- ECS- Amazon Elastic Container Service (Amazon ECS) is a scalable container orchestration service for running and managing containers on AWS, like Docker containers.
 
- EKS- Amazon Elastic Kubernetes Service (Amazon EKS) is a fully managed service for running Kubernetes on AWS. It simplifies deploying, managing, and scaling containerized applications using open-source Kubernetes
### Fargate:
AWS Fargate is a serverless compute engine for containers. It works with both Amazon ECS and Amazon EKS. Fargate is a container hosting platform, unlike Amazon ECS and Amazon EKS, which are both container orchestration services.

**Elastic Beanstalk**
- Beanstalk fully manages the streamlines the deployment, management, and scaling of web applications.
- It is a PaaS, so you dont have to manage the infrastructure but have to perform the deployment of you work

**AWS Batch**
- Its is a service which is used for big data ,machine learning etc..
- Can compute workloads that are in batches.

**Lightsail**
- Offers virtual private servers, storage and networking.
- It is designed for beginners

