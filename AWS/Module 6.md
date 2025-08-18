
## **1. Block Storage in AWS**

* **AWS Service:** **Amazon EBS** (Elastic Block Store)
* **What it is:**
  * Stores data in fixed-size blocks, similar to a hard disk or SSD.
  * You attach it to an **EC2 instance** like a local drive.
  * The EC2 OS handles file systems, formatting, and structure.
* **Best for:**
  Databases, OS boot volumes, low-latency apps, transactional workloads.
* **Example:**
  An EC2 instance running MySQL stores its DB files on an EBS volume.
* **Key features in AWS:**

  * Persistent storage even if EC2 stops (unless deleted).
  * Snapshots to S3 for backups.
  * Can be provisioned with specific IOPS for performance.

---

## **2. File Storage in AWS**

* **AWS Service:** **Amazon EFS** (Elastic File System)
* **What it is:**
  * Stores data as files in a shared directory/folder structure.
  * Multiple EC2 instances can mount the same EFS and read/write files simultaneously.
  * Uses **NFS protocol**.
* **Best for:**
  Shared access across multiple EC2s, content management systems, user directories.
* **Example:**
  A web application hosted on multiple EC2 instances stores images and static files on EFS so all instances can access them.
* **Key features in AWS:**

  * Automatically scales storage as you add files.
  * Regional service — accessible across multiple AZs.
  * Pay-per-use for storage consumed.

---

## **3. Object Storage in AWS**

* **AWS Service:** **Amazon S3** (Simple Storage Service)
* **What it is:**
  * Stores data as **objects** (data + metadata + unique key).
  * No folder hierarchy — “folders” are virtual (key prefixes).
  * Access via API or console, not like a mounted drive.
* **Best for:**
  Backups, logs, videos, static web hosting, big data storage.
* **Example:**
  Hosting a static website entirely on S3, or storing user-uploaded photos.
* **Key features in AWS:**

  * Practically unlimited storage.
  * Multiple storage classes (Standard, IA, Glacier) for cost optimization.
  * Integrated with many AWS services (CloudFront, Athena, Lambda).

---

### **AWS Mapping Table**

| Storage Type   | AWS Service | Mounted Like Drive?       | Protocol / Access | Common Use Case          |
| -------------- | ----------- | ------------------------- | ----------------- | ------------------------ |
| Block Storage  | EBS         | Yes (to EC2)              | OS-level          | Databases, OS disk       |
| File Storage   | EFS         | Yes (shared to many EC2s) | NFS               | Shared files between EC2 |
| Object Storage | S3          | No (API-based)            | HTTP/HTTPS        | Backups, media, big data |

---

# Block Storage Service
## **Amazon Elastic Block Store (EBS)**

Amazon EBS provides _persistent block-level storage_ volumes for use with Amazon EC2 instances. EBS volumes act like external hard drives, offering consistent and low-latency performance for workloads like databases and file systems.

- Even when you **stop or terminate EC2 instances the data will be persistence** unlike the inbuild instance block store

## **EBS Snapshots**

EBS snapshots are point-in-time backups of EBS volume. They can be used for disaster recovery, data migration, volume resizing, and for creating consistent backups of production workloads.


## **Amazon Data Lifecycle Manager**

You can automate the creation, retention, and deletion of EBS snapshots using Amazon Data Lifecycle Manager.



# Object Storage Service

## **Amazon Simple Storage Service(S3)**
- Amazon S3 is an object storage service that can store unlimited amounts of data in the AWS Cloud. Object storage is particularly well-suited for handling large amounts of unstructured data, such as documents, images, and videos.

- Amazon S3 stores files as **objects** in containers known as **buckets**, and each object can range in size from a few bytes to several terabytes.

- Amazon S3 has no fixed storage limit, scaling automatically to accommodate any  amount of data you need to store.

- Each object typically includes the _data_ itself, _metadata_, and a unique identifier, or _key_. Objects can be of any file type, such as images, videos, documents, or application data.

## **S3 Lifecycle**

- Transition actions: define when objects should transition to another storage class.

- Expiration actions: define when objects expire and should be permanently deleted.

For example, you might transition objects to S3 Standard-IA storage class 30 days after you create them. Or you might archive objects to the S3 Glacier Deep Archive storage class 1 year after creating them.


# File Storage Service
## **Amazon Elastic File System (EFS)**
- Amazon EFS is a fully managed, scalable file storage service for use with AWS cloud services and on-premises resources.
- Amazon EFS automatically scales as data is added or removed. This means AnyCompany Financial can scale their compute resources independently while maintaining access to the same elastic file system.
- Amazon EFS is designed for concurrent shared access from multiple EC2 instances across different Availability Zones with consistent performance.




##  **AWS Storage Gateway**
Storage Gateway is a hybrid cloud storage service that makes it possible to seamlessly integrate on-premises environments with AWS Cloud storage. You can use it to extend your local storage to the cloud while maintaining low-latency access to frequently used data.


**Elastic Disaster Recovery** replicates critical workloads to AWS with minimal downtime. Your servers' block-level data is continuously replicated to AWS, making it ideal for uses that require robust disaster recovery solutions.

