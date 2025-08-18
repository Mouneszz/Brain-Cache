**Amazon Virtual Private Cloud(Amazon VPC)**
- It let you to create a logically isolated section where you can launch aws resources/services.
- Its a private network and provide private IP range.

**SUBNET**
Subnets are used to organize your resources and can be made publicly or privately accessible. A private subnet is commonly used to contain resources like a database storing customer or transactional information. A public subnet is commonly used for resources like a customer-facing website.

- Subnets are chunk of IP address which is used to group resources.

 To allow public traffic from the internet to access you VPC you have to attach **internet gateway** . 
 -  An internet gateway is a connection between a VPC and the internet.

A **virtual private gateway** is the virtual private network (VPN) endpoint on the AWS side. It provides a way for you to establish a secure, encrypted connection between your on-premises network and your virtual private cloud (VPC).

Network ACL:
- Packet(data entering through the internet gateway) is constantly checked by ACL every time they enter a subnet.


**Stateless packet filtering**

**Network** **ACLs** (Access Control List) perform stateless packet filtering. They remember nothing and check packets that cross the subnet border each way: inbound and outbound.

When a packet response for that request comes back to the subnet, the network ACL does not remember your previous request. The network ACL checks the packet response against its list of rules to determine whether to allow or deny.

**Stateful packet filtering**

**Security groups** perform stateful packet filtering. They remember previous decisions made for incoming packets.

Consider the same example of sending a request out from an Amazon EC2 instance to the internet. When a packet response for that request returns to the instance, the security group remembers your previous request. The security group allows the response to proceed, regardless of inbound security group rules.

| Feature            | Security Groups                                                       | Network ACLs                                                 |
| ------------------ | --------------------------------------------------------------------- | ------------------------------------------------------------ |
| **Scope**          | Instance level (attached to EC2 instances)                            | Subnet level (associated with subnets)                       |
| **State**          | Stateful (remembers state)                                            | Stateless (doesn't remember state)                           |
| **Rule types**     | Only allow type rules                                                 | Both allow and deny type rules                               |
| **Return traffic** | Return traffic is automatically allowed if inbound traffic is allowed | Return traffic must be implicitly allowed in both directions |
| **Uses**           | Fine-grained control of traffic for individual EC2 instances          | Broad control of traffic in and out of subnets               |

**Edge Computing**:
- Edge networking is the process of bringing information storage and computing abilities closer to the devices

**Amazon Route 53**  
Route 53 is a highly available and scalable cloud DNS service.


> **Amazon CloudFront**

CloudFront is a content delivery network (CDN) service that delivers your content with faster loading times, cost savings, and reliability.

