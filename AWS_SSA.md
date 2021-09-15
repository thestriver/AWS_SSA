## AWS Certified Solutions Architect – Associate

(SAA-C02)
To Delete: Use A Cloud Guru 7 days trial after reading

![](assets/images/saa/domain.png)

720/1000 - 65 Questions

-  Define a solution using architectural design principles based on customer requirements.
-  Provide implementation guidance based on best practices to an organization throughout the lifecycle of a
  project

**Whitepapers**

Study tip: Focus on the following whitepapers

AWS Well-Architected webpage : https://aws.amazon.com/architecture/well-architected/

Study tip: Focus on the following FAQs

Amazon EC2(https://aws.amazon.com/ec2/faqs/) || Amazon S3(https://aws.amazon.com/s3/faqs/) || Amazon VPC(https://aws.amazon.com/vpc/faqs/) || Amazon Route 53(https://aws.amazon.com/route53/faqs/) || Amazon RDS(https://aws.amazon.com/rds/faqs/) || Amazon SQS(https://aws.amazon.com/sqs/faqs/)

Readinesss: https://www.aws.training/Details/Curriculum?id=20685

---

<h2>S3: Simple Storage Service - Scalable storage in the cloud</h2>
You can store 0 - 5 terabytes. Amazon S3 are managed at a regional level. Note: Amazon S3 is a global namespace but you still create your buckets within a region

- S3: object storage / S3 Glacier: low cost long-term archive and backup / Storage Gateway: Hybrid cloud storage with local caching / Snowcone (8TB)/ Snowballs Edge (50TB(compute-optimized) and 80TB(storage optimized) versions) / ~~Snowball Edge (100TB)~~, Snowmobile (100PB)

- S3 Intelligent-Tiering uses ML to automatically monitors access patterns of objects and automatically moves them between the S3 Standard and S3 Standard-IA storage classes. It is not designed for archival data.
- S3 Standard-IA is ideal for data that is infrequently accessed but requires high availability when needed.

![](assets/images/saa/s3classes.png)

- Buckets are private by default and access is controlled by **Bucket Policies** and **ACL**

- Encryption:
  Encryption in transit - traffic between local host and s3 is achieved by SSL/TLS

SSE KMS (envelope encrption) - can be used for both server side and client side encryption

a. Server side encryption(SSE) - Encryption at Rest is done using S3 Managed Keys (which manages all risks)

- SSE-S3 AES (key is handled using AES-256 Algorithm) requires that Amazon S3 manage the data and the encryption keys

- SSE KMS (envelope encrption) - requires that AWS manage the data key but you manage the AWS KMS keys in AWS KMS.

- SSE C- where you manage the encryption key. (N.B To upload an object with a customer-provided encryption key (SSE-C), use the AWS CLI, AWS SDK, or Amazon S3 REST API.)

b. Client side encryption - here you encrypt your files yourself before uploading to s3

---

- Data Consistency:
  a. New Objects(PUTS) (**read after write consistency**) b. Overwrite(PUTS) or Delete (DELETE) - (**eventual consistency**) - means it takes a couple of seconds for AWS to replicate the updated copies across AZ.

N.B Delete can only be done by a root user.

- CRR - (Cross Region Replication) -
  S3 Cross-Region Replication (CRR) is used to copy objects from one Amazon S3 bucket to the _destination bucket_ in different accounts in AWS Regions. after upload, object is **automatically replicated** to other regions.

- Versioning has to be turned on for CRR replication to be done to another AWS account. You can't disable versioning after enabling it. It can only be suspended.

- MFA delete can also be done with the CLI. Versioning must be turned on though.

- Transfer Acceleration:
  Amazon S3 Transfer Acceleration can speed up content transfers to and from Amazon S3 by as much as 50-500% for long-distance transfer of larger objects.
  S3 Transfer Acceleration (S3TA) reduces the variability in Internet routing, congestion and speeds that can affect transfers, and logically shortens the distance to S3 for remote applications. S3TA improves transfer performance by routing traffic through Amazon CloudFront’s globally distributed Edge Locations and over AWS backbone networks, and by using network protocol optimizations. A distinct url is used by the users.

- Presigned URLS - generated using AWS **CLI or SDK** and provides temp access to **private objects**

Official doc:
https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html

![](assets/images/saa/s3cheatsheet.png)
![](assets/images/saa/s3csheet2.png)
![](assets/images/saa/s3csheet3.png)

---

Snowcone (8TB)
Snowball - (50TB(compute-optimized) and 80TB(storage optimized) versions)

~~Snowball Edge (100TB) - storage, compute and GPU optimized - can be used in clusters

~~ Snowmobile (100PB)

![](assets/images/saa/snow.png)



___

<h1>VPC</h1>
Define and launch AWS resources in a logically isolated virtual network

![](assets/images/saa/vpc.png)

![](assets/images/saa/vpc1.png)

![](assets/images/saa/vpc2.png)


