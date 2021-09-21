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

---

<h1>VPC</h1>
Define and launch AWS resources in a logically isolated virtual network

![](assets/images/saa/vpc0.png)

![](assets/images/saa/vpc.png)

![](assets/images/saa/vpc1.png)

![](assets/images/saa/vpc2.png)

<h2>Amazon VPC features</h2>

**Reachability Analyzer** Reachability Analyzer is a static configuration analysis tool that enables you to analyze and debug network reachability between two resources in your VPC.

**VPC Flow Logs**: You can monitor your VPC flow logs delivered to Amazon S3 or Amazon CloudWatch to gain operational visibility into your network dependencies and traffic patterns, detect anomalies and prevent data leakage, or troubleshoot network connectivity and configuration issues.

**VPC Traffic Mirroring:** VPC traffic mirroring allows you to copy network traffic from an elastic network interface of Amazon EC2 instances and then send the traffic to out-of-band security and monitoring appliances for deep packet inspection.

**Ingress Routing:** This allows you to route all incoming and outgoing traffic flowing to/from an Internet Gateway (IGW) or Virtual Private Gateway (VGW) to a specific EC2 instance’s Elastic Network Interface.

An elastic network interface is a logical networking component in a VPC that represents a virtual network card.

A customer gateway device is a physical or software appliance that you own or manage in your on-premises network (on your side of a Site-to-Site VPN connection).

An internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between your VPC and the internet.

![](assets/images/saa/vpc8.png)

Read more: https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html

**Security Groups:** Security groups act as a firewall for associated Amazon EC2 instances, controlling both inbound and outbound traffic at the **instance level.**

**Network Access Control List**: A network access control list (ACL) is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more **subnets.**

![](assets/images/saa/vpc3.png)

![](assets/images/saa/vpc4.png)
Add a route to the main route table that points all traffic (0.0.0.0/0) to the internet gateway.

By default, a default subnet is a public subnet, because the main route table sends the subnet's traffic that is destined for the internet to the internet gateway. You can make a default subnet into a private subnet by **removing the route from the destination 0.0.0.0/0 to the internet gateway**. However, if you do this, no EC2 instance running in that subnet can access the internet.

Instances that you launch into a **default subnet** receive both a public IPv4 address and a private IPv4 address, and both public and private DNS hostnames.

![](assets/images/saa/vpc5.png)

<h2>A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them privately. Instances in either VPC can communicate with each other as if they are within the same network.</h2>

![](assets/images/saa/vpc6.png)

![](assets/images/saa/vpc7.png)

Bastion hosts (also called “jump servers”) are often used as a best practice for accessing privately accessible hosts within a system environment.

you can reduce your system’s attack surface while also offering greater visibility into commands issued on your hosts. The solution is to replace your bastion host by using Amazon EC2 Systems Manager.

![](assets/images/saa/vpc9.png)

<h2>AWS Direct Connect</h2>
Create a dedicated network connection between your premises and AWS

![](assets/images/saa/vpc10.png)

![](assets/images/saa/vpc12.png)
Endpoints are powered by AWS PrivateLink.

There are _three types of VPC endpoints_:

- Interface endpoints - cost money
  elastic network interface with a private IP address from the IP address range of your subnet. an entry point for traffic destined to a **supported AWS service or a VPC endpoint service.**
  ![](assets/images/saa/vpc13.png)
- Gateway Load Balancer endpoints
  elastic network interface with a private IP address from the IP address range of your subnet. **entry point to intercept traffic and route it to a service that you've configured using Gateway Load Balancers**

- Gateway endpoints
  Free..
  supports:
  Amazon S3
  DynamoDB
  You specify a gateway endpoint as a route table target for traffic that is destined for the supported AWS services.

![](assets/images/saa/vpc14.png)

The ipv4 address of the network interface is always its private ipv4 adress.

![](assets/images/saa/vpc15.png)

![](assets/images/saa/nacl1.png)

**When you launch an instance in a VPC, you can assign up to five security groups to the instance. Security groups act at the instance level, not the subnet level. Therefore, each instance in a subnet in your VPC can be assigned to a different set of security groups.**

**You can specify allow rules, but not deny rules.** - something a NACL can do i.e. it can block specific IP address

![](assets/images/saa/nacl2.png)

Security group rules
You can add or remove rules for a security group (also referred to as authorizing or revoking inbound or outbound access). A rule applies either to inbound traffic (ingress) or outbound traffic (egress). You can grant access to a specific CIDR range, or to another security group in your VPC or in a peer VPC (requires a VPC peering connection).

Stale security group rules
If your VPC has a VPC peering connection with another VPC, a security group rule can reference another security group in the peer VPC. This allows instances that are associated with the referenced security group and those that are associated with the referencing security group to communicate with each other.

If the owner of the peer VPC deletes the referenced security group, or if you or the owner of the peer VPC deletes the VPC peering connection, the security group rule is marked as stale.

![](assets/images/saa/sn1.png)

![](assets/images/saa/sn2.png)

![](assets/images/saa/nat1.png)

We use the term NAT in this documentation to follow common IT practice, though the actual role of a NAT device is both address translation and port address translation (PAT).

![](assets/images/saa/nat2.png)

You can now launch NAT Gateways in your Amazon Virtual Private Cloud (VPC) without associating an internet gateway to your VPC.

We recommend that you use NAT gateways because they provide better availability and bandwidth and require less effort on your part to administer.

![](assets/images/saa/nat3.png)

<h2>AWS Identity and Access Management (IAM)</h2>
Securely manage access to AWS services and resources

![](assets/images/saa/iam1.png)

![](assets/images/saa/iam2.png)

_Best Practices_

Users – Create individual users.

Groups – Manage permissions with groups.

Permissions – Grant least privilege.

Auditing – Turn on AWS CloudTrail.

Password – Configure a strong password policy.

MFA – Enable MFA for privileged users.

Roles – Use IAM roles for Amazon EC2 instances.

Sharing – Use IAM roles to share access.

Rotate – Rotate security credentials regularly.

Conditions – Restrict privileged access further with conditions.

Root – Reduce or remove use of root.

![](assets/images/saa/iam3.png)

![](assets/images/saa/iam4.png)

![](assets/images/saa/iam5.png)

<h2>Amazon Cognito</h2>
Amazon Cognito lets you add user sign-up, sign-in, and access control to your web and mobile apps quickly and easily.

![](assets/images/saa/cog1.png)

![](assets/images/saa/cog2.png)

![](assets/images/saa/cog3.png)

![](assets/images/saa/cog4.png)

<h2>AWS Single Sign-On</h2>
Centrally manage access to multiple AWS accounts or applications.AWS Single Sign-On (AWS SSO) is where you create, or connect, your workforce identities in AWS once and manage access centrally across your AWS organization. You can choose to manage access just to your AWS accounts or cloud applications.

 <h2>AWS CLI & SDK</h2>
 AWS Command Line Interface
The AWS Command Line Interface (CLI) is a unified tool to manage your AWS services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts.

SDK:
Tools to Build on AWS
Easily develop applications on AWS in the programming language of your choice

<h2>DNS</h2>

https://www.cloudflare.com/en-gb/learning/dns/what-is-dns/

![](assets/images/saa/dns.png)

<h2>Amazon Route 53</h2>

Amazon Route 53 is a highly available and scalable cloud **Domain Name System (DNS) web service**. It is designed to give developers and businesses an extremely reliable and cost effective way to route end users to Internet applications by translating names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other. Amazon Route 53 is fully compliant with IPv6 as well.

Amazon Route 53 effectively connects user requests to infrastructure running in AWS – such as Amazon EC2 instances, Elastic Load Balancing load balancers, or Amazon S3 buckets – and can also be used to route users to infrastructure outside of AWS.

![](assets/images/saa/route.png)

![](assets/images/saa/route2.png)

<h2>Amazon Elastic Compute Cloud (Amazon EC2)</h2>

![](assets/images/saa/ec2.png)

![](assets/images/saa/ec3.png)

![](assets/images/saa/ec23.png)

![](assets/images/saa/ec24.png)

![](assets/images/saa/ec2a.png)

![](assets/images/saa/ec2p.png)
You can also pay for Dedicated Hosts which provide you with EC2 instance capacity on physical servers dedicated for your use.
![](assets/images/saa/ec2p1.png)

![](assets/images/saa/ami.png)
