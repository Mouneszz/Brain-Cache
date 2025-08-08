**Going Global**
Compliance is an important consideration when selecting regions.

### **What is a Region?**
An **AWS Region** is a **geographic area** (like a country or part of a continent) where **AWS has multiple data centers**.
- Each region have three availability zones(group of data centers)

Availability  zones
- AZs are **isolated from each other** (own power, network, cooling) but are **connected via low-latency links**.
- If one AZ fails (power outage, flood, etc.), your app still runs in others.

Edge Locations
- To cover the area which are not in regions



**CloudFormation**
 - it is a service which helps to set up your aws resources.
 - Can define  the infrastructure as a code, example if you want to create ec2 instance CloudFormation takes cares the configuring those resources.