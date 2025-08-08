# ☁ Cloud Interview Prep — Hour 1 & Hour 2 Notes

## **Hour 1 — Core Cloud Basics**

### **1. What is Cloud Computing?**
Delivery of computing services (servers, storage, databases, networking, software) over the internet, paid per use.

**Benefits:**
- Scalability — Increase/decrease resources instantly.
- Cost efficiency — Pay-as-you-go.
- Accessibility — Access from anywhere.
- Reliability — Backup & disaster recovery.
- Security — Controlled access, encryption.

---

### **2. On-Premises vs Cloud**
| Feature     | On-Premises            | Cloud                 |
| ----------- | ---------------------- | --------------------- |
| Ownership   | You own infrastructure | Provider owns it      |
| Cost        | High upfront           | Pay-as-you-go         |
| Scaling     | Manual                 | Instant               |
| Maintenance | Your team              | Provider manages      |
| Access      | Location-limited       | Anywhere via internet |

---

### **3. Service Models**
- **IaaS (Infrastructure as a Service)**  
  Provides: Virtualized computing resources.  
  You manage OS, apps.  
  **Examples:** AWS EC2, Azure VM, GCP Compute Engine.  
  **Use Case:** Hosting custom applications.

- **PaaS (Platform as a Service)**  
  Provides: Ready-to-use development platforms.  
  You focus on code; provider manages infra.  
  **Examples:** AWS Elastic Beanstalk, Azure App Service, GCP App Engine.  
  **Use Case:** Deploying web apps quickly.

- **SaaS (Software as a Service)**  
  Provides: Ready software over the internet.  
  You just log in and use it.  
  **Examples:** Gmail, Google Docs, Salesforce.  
  **Use Case:** Email, CRM, collaboration tools.

---

### **4. Deployment Models**
- **Public Cloud:** Shared infra — AWS, Azure.
- **Private Cloud:** Dedicated infra — VMware Private Cloud.
- **Hybrid Cloud:** Combination of public & private.
- **Multi-Cloud:** Multiple providers used together.

---

## **Hour 2 — AWS, Azure, GCP Quick Notes**

### **1. AWS (Amazon Web Services)**
**Tagline:** Largest cloud provider, wide range of services.

**Key Services & Use Cases:**
- **EC2:** Virtual servers → Host backend applications.
- **S3:** Object storage → Store images/files for a web app.
- **RDS:** Managed SQL DB → Store user accounts.
- **Lambda:** Serverless → Auto-process uploaded images.
- **CloudFront:** CDN → Faster website loading globally.

**Example Statement:**  
> "In my project, I used S3 to store user-uploaded files, EC2 to run the backend, and RDS for the database."

---

### **2. Azure (Microsoft Azure)**
**Tagline:** Strong enterprise solutions, Windows integration.

**Key Services & Use Cases:**
- **Azure VM:** Virtual machines → Deploy a web app.
- **Blob Storage:** Object storage → Store backups.
- **Azure SQL Database:** Managed relational DB → Store transactional data.
- **Azure Functions:** Serverless → Run daily cleanup scripts.
- **Azure DevOps:** CI/CD → Automate build & deployment.

**Example Statement:**  
> "We hosted the backend on Azure VM, stored backups in Blob Storage, and used Azure Functions for scheduled maintenance."

---

### **3. GCP (Google Cloud Platform)**
**Tagline:** Strong in AI/ML and big data processing.

**Key Services & Use Cases:**
- **Compute Engine:** Virtual machines → Host data processing apps.
- **Cloud Storage:** Object storage → Store large datasets.
- **BigQuery:** Data warehouse → Analyze millions of rows quickly.
- **Cloud Functions:** Serverless → Process API requests.
- **Vertex AI:** Machine learning → Train & deploy ML models.

**Example Statement:**  
> "We stored datasets in Cloud Storage, processed them in Compute Engine, and analyzed them with BigQuery."

---


**1. EC2 (Elastic Compute Cloud)**  
AWS service to launch virtual servers in the cloud; fully customizable in CPU, RAM, storage, and OS.  
Used to host backend apps, websites, or any compute workloads.

---

**2. EC2 Instance**  
A running virtual server created from an AMI; can be accessed via SSH (Linux) or RDP (Windows).  
Multiple instances can be launched from the same AMI for scaling.

---

**3. Dynamic Scaling (Auto Scaling)**  
Automatically adds or removes EC2 instances based on traffic or load.  
Ensures performance during peak and saves cost during low usage.

---

**4. Load Balancing (Elastic Load Balancer — ELB)**  
Distributes incoming traffic evenly across multiple servers.  
Improves availability, fault tolerance, and scalability.

---

**5. SQS (Simple Queue Service)**  
Fully managed message queue to decouple components of an application.  
Ensures reliable message delivery between distributed systems.

---

**6. SNS (Simple Notification Service)**  
Pub/Sub messaging service for sending notifications to multiple subscribers at once.  
Supports email, SMS, push notifications, and HTTP endpoints.