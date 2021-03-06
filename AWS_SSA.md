## AWS Certified Solutions Architect – Associate

Go through all the 6 FAQs after the video

(SAA-C02)
To Delete: Use A Cloud Guru 7 days trial after reading

![](assets/images/saa/domain.png)

720/1000 - 65 Questions
Response types
There are two types of questions on the exam:

- Multiple choice: Has one correct response and three incorrect responses (distractors)
- Multiple response: Has two or more correct responses out of five or more response options

---

 Define a solution using architectural design principles based on customer requirements.

 Provide implementation guidance based on best practices to an organization throughout the lifecycle of a
project

**Whitepapers**

Study tip: Focus on the following whitepapers

AWS Well-Architected webpage : https://aws.amazon.com/architecture/well-architected/

⦁ TO attain operational excellence, a key AWS service is AWS cloud formation which lets you create templates that you can use to consistently provision whatever resources that you want for your application

⦁ To attain the security pillar you need to use the key AWS service IAM to control user and programmatic access
⦁ you can use cloudtrail to record API calls and VPC to launch resources into a virtual network

⦁ For reliability you can use AWS shield to safe guard against DDOS attacks

⦁ For performance the key service is cloudwatch which you can use to see how your services are holding up
⦁ for cost optimization, you can use the cost explorer to see how much services are costing you

AWS also has 6 FAQs that covers some of the key services in this exam:

Study tip: Focus on the following FAQs
⦁ EC2: https://aws.amazon.com/ec2/faqs/
⦁ S3: https://aws.amazon.com/s3/faqs/
⦁ VPC: https://aws.amazon.com/vpc/faqs/
⦁ Route 53: https://aws.amazon.com/route53/faqs/
⦁ rds: https://aws.amazon.com/rds/faqs/
⦁ sqs: https://aws.amazon.com/sqs/faqs/

Readinesss: https://www.aws.training/Details/Curriculum?id=20685

---

<h2>S3: Simple Storage Service - Scalable storage in the cloud</h2>
You can store 0 - 5 terabytes. Amazon S3 are managed at a regional level. 
Note: Amazon S3 is a global namespace but you still create your buckets within a region

highlyavailable and durable


- S3: object storage 
 S3 Glacier: low cost long-term archive and backup 

 Storage Gateway: Hybrid cloud storage with **local caching** 
 An AWS Storage Gateway volume gateway connects an on-premises software application with cloudbacked storage volumes that can be mounted as Internet Small Computer System Interface (iSCSI) devices from
on-premises application servers. In cached volumes mode, all the data is stored in Amazon S3 and a copy of
frequently accessed data is stored locally.
 
  Snowcone (8TB)/ Snowballs Edge (50TB(compute-optimized) and 80TB(storage optimized) versions) / ~~Snowball Edge (100TB)~~, Snowmobile (100PB)

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



You can generate a presigned URL programmatically using the REST API, the AWS Command Line Interface, and the AWS SDK for Java, .NET, Ruby, PHP, Node.js, Python, and Go.

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

A NAT gateway forwards traffic from the instances in the private subnet to the internet or other AWS
services, and then sends the response back to the instances. 
After a NAT gateway is created, the route tables for private subnets must be updated to point internet traffic to the NAT gateway

<h2>Amazon VPC features</h2>

**Reachability Analyzer** Reachability Analyzer is a static configuration analysis tool that enables you to analyze and debug network reachability between two resources in your VPC.

**VPC Flow Logs**: You can monitor your VPC flow logs delivered to Amazon S3 or Amazon CloudWatch to gain operational visibility into your network dependencies and traffic patterns, detect anomalies and prevent data leakage, or troubleshoot network connectivity and configuration issues.

**VPC Traffic Mirroring:** VPC traffic mirroring allows you to copy network traffic from an elastic network interface of Amazon EC2 instances and then send the traffic to out-of-band security and monitoring appliances for deep packet inspection.

**Ingress Routing:** This allows you to route all incoming and outgoing traffic flowing to/from an Internet Gateway (IGW) or Virtual Private Gateway (VGW) to a specific EC2 instance’s Elastic Network Interface.

An elastic network interface is a logical networking component in a VPC that represents a virtual network card.

A customer gateway device is a physical or software appliance that you own or manage in your on-premises network (on your side of a Site-to-Site VPN connection).

An internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between your VPC and the internet.

![](assets/images/saa/vpc8.png)

 Whether a subnet is private or public depends on its route table. A public subnet has a route pointing to an internet gateway, and a private subnet does not.

Read more: https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html

**Security Groups:** Security groups act as a firewall for associated Amazon EC2 instances, controlling both inbound and outbound traffic at the **instance level.**



port 443 - HTTPS

**Network Access Control List**: A network access control list (ACL) is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more **subnets.**

![](assets/images/saa/vpc3.png)

![](assets/images/saa/vpc4.png)
Add a route to the main route table that points all traffic (0.0.0.0/0) to the internet gateway.

By default, a default subnet is a public subnet, because the main route table sends the subnet's traffic that is destined for the internet to the internet gateway. You can make a default subnet into a private subnet by **removing the route from the destination 0.0.0.0/0 to the internet gateway**. However, if you do this, no EC2 instance running in that subnet can access the internet.

Instances that you launch into a **default subnet** receive both a public IPv4 address and a private IPv4 address, and both public and private DNS hostnames.

![](assets/images/saa/vpc5.png)

<h2>A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them privately. Instances in either VPC can communicate with each other as if they are within the same network.</h2>
In a VPC peering connection, using the NAT Gateway of another VPC becomes transitive routing and is not supported in AWS.

![](assets/images/saa/vpc6.png)

![](assets/images/saa/vpc7.png)

Bastion hosts (also called “jump servers”) are often used as a best practice for accessing privately accessible hosts within a system environment.


Configure the security groups of the Windows server instances to only accept TCP/3389 connections from the security group of the Windows bastion host. because with this option, Windows server instances only allow the RDP traffic from the bastion host instance. Users need to login to the bastion host to connect to the Windows servers.

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
  elastic network interface with a private IP address from the IP address range of your subnet. **entry point to intercept traffic and route it to a service that you've configured using Gateway Load Balancers**for example, for security inspection.

- Gateway endpoints  supports:
  Amazon S3
  DynamoDB
    Free..

  You specify a gateway endpoint as a route table target for traffic that is destined for the supported AWS services.

**to integrate with S3 with  restricting any internet-bound traffic = Use A gateway endpoint.**

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

Amazon Route 53 alias records provide a Route 53–specific extension to DNS functionality. Alias records let you route traffic to selected AWS resources, such as CloudFront distributions and Amazon S3 buckets.
![](assets/images/saa/route4.png)

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

![](assets/images/saa/ami2.png)

– Hibernating an instance saves the contents of RAM to the Amazon EBS root volume. When the instance restarts, the RAM contents are reloaded.

<h2>Auto Scaling groups</h2>

An Auto Scaling group contains a collection of Amazon EC2 instances that are treated as a logical grouping for the purposes of automatic scaling and management.

![](assets/images/saa/asg.png)

![](assets/images/saa/asg1.png)


With target tracking, you select a load metric for your application, such as “Average CPU Utilization” or the new “Request Count Per Target” metric from Application Load Balancer, set the target value, and Auto Scaling adjusts the number of EC2 instances in your Auto Scaling group as needed to maintain that target.

launch templates is launch configurations with versioning

The Cooldown period is a configurable setting for your Auto Scaling group, ensuring that it doesn't launch or terminate additional instances before the previous scaling activity takes effect. After the Auto Scaling group dynamically scales using a simple Scaling Policy, it waits for the Cooldown period to complete before resuming scaling activities.

<h2>Elastic Load Balancing</h2>

![](assets/images/saa/elb1.png)

Elastic Load Balancing types

Elastic Load Balancing provides **four types of load balancers** that can be used with your Auto Scaling group: Application Load Balancers, Network Load Balancers, Gateway Load Balancers, and Classic Load Balancers.

There is a key difference in how the load balancer types are configured. With Application Load Balancers, Network Load Balancers, and Gateway Load Balancers, instances are registered as targets with a target group, and you route traffic to the target group. With Classic Load Balancers, instances are registered directly with the load balancer.

Application Load Balancer
Routes and load balances at the application layer (HTTP/HTTPS), and supports path-based routing. An Application Load Balancer can route requests to ports on one or more registered targets, such as EC2 instances, in your virtual private cloud (VPC).

**Today we’re launching support for multiple TLS/SSL certificates on Application Load Balancers (ALB) using Server Name Indication (SNI). You can now host multiple TLS secured applications, each with its own TLS certificate, behind a single load balancer. In order to use SNI, all you need to do is bind multiple certificates to the same secure listener on your load balancer. ALB will automatically choose the optimal TLS certificate for each client. These new features are provided at no additional charge.**

Network Load Balancer
Routes and load balances at the transport layer (TCP/UDP Layer-4), based on address information extracted from the TCP packet header, not from packet content. Network Load Balancers can handle traffic bursts, retain the source IP of the client, and use a fixed IP for the life of the load balancer.

Gateway Load Balancer
Distributes traffic to a fleet of appliance instances. Provides scale, availability, and simplicity for third-party virtual appliances, such as firewalls, intrusion detection and prevention systems, and other appliances. Gateway Load Balancers work with virtual appliances that support the GENEVE protocol. Additional technical integration is required, so make sure to consult the user guide before choosing a Gateway Load Balancer.

Classic Load Balancer
Routes and load balances either at the transport layer (TCP/SSL), or at the application layer (HTTP/HTTPS). A Classic Load Balancer supports either EC2-Classic or a VPC.
![](assets/images/saa/elb2.png)

![](assets/images/saa/elb3.png)

![](assets/images/saa/elb4.png)

![](assets/images/saa/elb5.png)

**ELB Health checks : it doesnt terminate unhelathy instances it just redirects to helathy instances**

An Application Load Balancer (ALB) sends requests to healthy instances only. An ALB performs periodic
health checks on targets in a target group. An instance that fails health checks for a configurable number of consecutive times is considered unhealthy. The load balancer will no longer send requests to the instance until it
passes another health check.

![](assets/images/saa/elb6.png)

<h2>Amazon Elastic File System</h2>
Simple, serverless, set-and-forget, elastic file system

Amazon Elastic File System (EFS) automatically grows and shrinks as you add and remove files with no need for management or provisioning.

![](assets/images/saa/efs.png)

<h2>Amazon Elastic Block Store (EBS)</h2>
Easy to use, high performance block storage at any scale. **Virtual hard drive in the cloud.** Create new volumes to EC2 instances, backup via snapshots and easy encryption.

Throughput - data transfer rate
Volumes are automatically replicated within their AZ.

Amazon EBS provides multiple volume types that allow you to optimize storage performance and cost for a broad range of applications. These volume types are divided into **two major categories:**
**SSD-backed storage for transactional workloads, such as databases, virtual desktops and boot volumes,** and

**HDD-backed storage for throughput intensive workloads, such as MapReduce and log processing.**

SSD-based volumes include the **highest performance EBS volumes (io2 and io1)** for your most demanding transactional applications including SAP HANA, Microsoft SQL Server and IBM DB2, and **General Purpose SSD volumes (gp3 and gp2)** that balance price and performance for transactional applications, including virtual desktops, test and development environments, and interactive gaming applications.

HDD-based volumes include **Throughput Optimized HDD (st1)** for frequently accessed, throughput intensive workloads and the **lowest cost Cold HDD (sc1) for less frequently accessed data.**

![](assets/images/saa/ebs1.png)

![](assets/images/saa/ebs2.png)

![](assets/images/saa/ebs3.png)

![](assets/images/saa/ebs4.png)

![](assets/images/saa/ebs5.png)

![](assets/images/saa/ebs7.png)

After you no longer need an Amazon EBS volume, you can delete it. After deletion, its data is gone and the volume can't be attached to any instance. However, before deletion, you can store a snapshot of the volume, which you can use to re-create the volume later.

![](assets/images/saa/ebs6.png)

![](assets/images/saa/ebs8.png)

<h2>Amazon CloudFront - CDN</h2>
Fast, highly secure and programmable content delivery network (CDN)

Amazon CloudFront automatically maps network conditions and intelligently routes your user’s traffic to the most performant **_AWS edge location_** to serve up cached or dynamic content.

![](assets/images/saa/cf.png)

CloudFront offers the most advanced security capabilities, including field level encryption and HTTPS support, seamlessly integrated with AWS Shield, AWS Web Application Firewall and Amazon Route 53 to protect against multiple types of attacks including network and application layer DDoS attacks. These services co-reside at edge networking locations – globally scaled and connected via the AWS network backbone – providing a more secure, performant, and available experience for your users.

CloudFront works seamlessly with any AWS origin, such as Amazon S3, Amazon EC2, Elastic Load Balancing, or with any custom HTTP origin.

You can customize your content delivery through CloudFront using the secure and programmable edge computing features CloudFront Functions and AWS Lambda@Edge.

Lambda@Edge is a feature of Amazon CloudFront that lets you run code closer to users of your application, which improves performance and reduces latency.

![](assets/images/saa/cf2.png)

![](assets/images/saa/cf3.png)

![](assets/images/saa/cf9.png)

<h2>Amazon Relational Database Service (RDS)</h2>

Amazon RDS encrypts your databases using keys you manage with the AWS Key Management Service (KMS).

Amazon RDS also supports Transparent Data Encryption (TDE) for SQL Server (SQL Server Enterprise Edition) and Oracle (Oracle Advanced Security option in Oracle Enterprise Edition).

Automated backups
The automated backup feature of Amazon RDS enables point-in-time recovery for your database instance. Amazon RDS will backup your database and transaction logs and store both for a user-specified retention period. This allows you to restore your database instance to any second during your retention period, up to the last five minutes. Your automatic backup retention period can be configured to up to thirty-five days.

Database snapshots - Manual
Database snapshots are user-initiated backups of your instance stored in Amazon S3 that are kept until you explicitly delete them.

Automatic host replacement
Amazon RDS will automatically replace the compute instance powering your deployment in the event of a hardware failure.

![](assets/images/saa/rds.png)

![](assets/images/saa/rds2.png)

<h2>Amazon Aurora</h2>
MySQL and PostgreSQL-compatible relational database built for the cloud.

fault-tolerant and self-healing

Get 5X the throughput of standard MySQL and 3X the throughput of standard PostgreSQL.

To scale read capacity and performance, you can add up to 15 low latency read replicas across three Availability Zones

Amazon Aurora automatically grows storage as needed, **up to 128TB per database instance**

Amazon Aurora is designed to offer 99.99% availability, **replicating 6 copies of your data across 3 Availability Zones and backing up your data continuously to Amazon S3.** It transparently recovers from physical storage failures; instance failover typically takes less than 30 seconds

Losing 2 copies wont affect write availability while losing up to 3 copies wont affect read avail.

Babelfish is a new translation layer for Amazon Aurora PostgreSQL that enables Aurora to understand commands from applications written for Microsoft SQL Server. Run Microsoft SQL Server applications on PostgreSQL with little to no code change

Amazon Aurora Parallel Query is a feature of the Amazon Aurora database that provides faster analytical queries over your current data, without having to copy the data into a separate system. It can speed up queries by up to two orders of magnitude, while maintaining high throughput for your core transactional workload.



![](assets/images/saa/aur.png)

![](assets/images/saa/aur1.png)

![](assets/images/saa/aur3.png)

<h2>Amazon Redshift - cloud data warehouse</h2>

petabyte-scaling, columnar Storage

If enhanced VPC routing is not enabled, Amazon Redshift routes traffic through the internet, including traffic to other services within the AWS network.

![](assets/images/saa/red.png)

AQUA (Advanced Query Accelerator) is a new distributed and hardware-accelerated cache that enables Amazon Redshift to run up to 10x faster than other enterprise cloud data warehouses by automatically boosting certain types of queries. AQUA is included with the with the Redshift RA3 ra3.4xl and ra3.16xl node types at no additional cost.

![](assets/images/saa/red2.png)

Amazon Redshift Concurrency Scaling
Get consistent, fast query performance for highly concurrent workloads

With new Amazon Redshift RA3 instances with managed storage, you can choose the number of nodes based on your performance requirements, and only pay for the managed storage that you use. This gives you the flexibility to size your RA3 cluster based on the amount of data you process daily without increasing your storage costs

![](assets/images/saa/red3.png)

![](assets/images/saa/red4.png)

<h2>Amazon DynamoDB </h2>

is a NoSQL **key-value and document database** that delivers single-digit millisecond performance at any scale. It's a fully managed, **multi-region, multi-active**, durable database with built-in security, backup and restore, and **in-memory caching** for internet-scale applications. DynamoDB can handle more than **10 trillion requests per day and can support peaks of more than 20 million requests per second.**

SSD Storage - 3 regions

Table:
primary key: Partition and sort key
item and attribute

![](assets/images/saa/ddb.png)

Amazon DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache for Amazon DynamoDB

Point-in-time recovery (PITR) for Amazon DynamoDB

Use PartiQL, a SQL-compatible query language, to query, insert, update, and delete table data in DynamoDB.
Use Amazon Kinesis Data Streams to capture item-level changes in your DynamoDB tables.

AWS Pricing Calculator now supports Amazon DynamoDB.

NoSQL Workbench is a unified visual tool that provides data modeling, data visualization, and query development features to help you design, create, query, and manage DynamoDB tables.

Global tables replicate your DynamoDB tables automatically across your choice of AWS Regions.

gateway endpoint + route table entry  = ensure that API calls to Amazon DynamoDB from Amazon EC2 instances in a VPC do not traverse the internet

indexed metadata  =  DynamoDB

<h2>AWS Cloud​Formation - IaC</h2>
Speed up cloud provisioning with infrastructure as code

CF templates must list at least one resource

Build serverless applications with SAM

AWS Elastic Beanstalk provides an environment where you can easily deploy and run applications in the cloud

Behind the scenes, Elastic Beanstalk uses CloudFormation to create and maintain resources

AWS Quickstarts - a collection of pre-built CF templates

![](assets/images/saa/cf1.png)

<h2>Amazon CloudWatch</h2>
Amazon CloudWatch is a monitoring and observability service
Amazon CloudWatch is basically a metrics repository. An AWS service—such as Amazon EC2—puts metrics into the repository, and you retrieve statistics based on those metrics.

![](assets/images/saa/cw.png)

![](assets/images/saa/cw1.png)

Amazon CloudWatch allows you to collect default metrics from more than 70 AWS services, such as Amazon EC2, Amazon DynamoDB, Amazon S3, Amazon ECS, AWS Lambda, and Amazon API Gateway, without any action on your part. For example, EC2 instances automatically publish CPU utilization, data transfer, and disk usage metrics to help you understand changes in state. You can use one of seven built-in metrics for API Gateway to detect latency or leverage one of eight built-in metrics for AWS Lambda to detect errors and throttles. If you need more detailed metrics beyond the default metrics, such as shard-level Amazon Kinesis Data Streams metrics, then you can simply opt-in per resource.
Custom Metrics.

Amazon CloudWatch allows you to collect custom metrics from your own applications to monitor operational performance, troubleshoot issues, and spot trends.

Amazon CloudWatch dashboards enable you to create re-usable graphs and visualize your cloud resources and applications in a unified view.

High resolution alarms
Amazon CloudWatch alarms allow you to set a threshold on metrics and trigger an action.

![](assets/images/saa/cw2.png)

![](assets/images/saa/cw3.png)

Anomaly Detection
Amazon CloudWatch Anomaly Detection applies machine-learning algorithms to continuously analyze data of a metric and identify anomalous behavior.

ServiceLens
You can use Amazon CloudWatch ServiceLens to visualize and analyze the health, performance, and availability of your applications in a single place.

Synthetics
Amazon CloudWatch Synthetics allows you to monitor application endpoints more easily

Amazon CloudWatch Logs is also PCI and FedRamp compliant.

Data is encrypted at rest and during transfer. You can also use AWS KMS encryption to encrypt your log groups for added compliance and security.

Amazon EventBridge
Amazon EventBridge is a serverless event bus that makes it easier to build event-driven applications at scale using events generated from your applications, integrated Software-as-a-Service (SaaS) applications, and AWS services

EventBridge is the evolution of the CloudWatch Events service. It brings new features, including the ability to integrate data from popular SaaS providers as events within AWS.

![](assets/images/saa/cw4.png)

<h2>AWS CloudTrail</h2>
Track user activity and API usage

![](assets/images/saa/ct.png)
**who to blame**

![](assets/images/saa/ct1.png)

AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. With CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure.

![](assets/images/saa/ct3.png)
Event history allows you to view, search, and download the past 90 days of activity in your AWS account.

With AWS CloudTrail, you can simplify your compliance audits by automatically recording and storing event logs for actions made within your AWS account. Integration with Amazon CloudWatch Logs provides a convenient way to search through log data, identify out-of-compliance events, accelerate incident investigations, and expedite responses to auditor requests.

ith Amazon CloudWatch Events integration, you can define workflows that execute when events that can result in security vulnerabilities are detected.

![](assets/images/saa/ct-cw.png)

![](assets/images/saa/ct4.png)
. There are three types of events that can be logged in CloudTrail: management events, data events, and CloudTrail Insights events. By default, trails log management events, but not data or Insights events.

![](assets/images/saa/ct5.png)

<h2>AWS Lambda</h2>
Run code without thinking about servers or clusters. Only pay for what you use.

AWS Lambda is a serverless compute service that lets you run code without provisioning or managing servers, creating workload-aware cluster scaling logic, maintaining event integrations, or managing runtimes.

The code you run on AWS Lambda is called a “Lambda function.” It is stateless with no affinity to the underlying infrastructure After you create your Lambda function, it is always ready to run as soon as it is triggered, similar to a formula in a spreadsheet.

The AWS Lambda free usage tier includes 1M free requests per month and 400,000 GB-seconds of compute time per month.

AWS Lambda automatically monitors Lambda functions and reports metrics through Amazon CloudWatch. Lambda tracks the number of requests, the latency per request, and the number of requests resulting in an error. You can view the request rates and error rates using the AWS Lambda Console, the CloudWatch console, and other AWS resources.

![](assets/images/saa/la.png)

![](assets/images/saa/la1.png)

![](assets/images/saa/la2.png)


<h2>Amazon Simple Queue Service</h2>
Fully managed message queues for microservices, distributed systems, and serverless applications

![](assets/images/saa/sqs.png)

![](assets/images/saa/sqs1.png)

**To manage large Amazon Simple Queue Service (Amazon SQS) messages, you can use Amazon Simple Storage Service (Amazon S3) and the Amazon SQS Extended Client Library for Java. This is especially useful for storing and consuming messages between 256kb to 2 GB.**

![](assets/images/saa/sqs3.png)

![](assets/images/saa/sqs2.png)

![](assets/images/saa/sqs4.png)


![](assets/images/saa/sqs5.png)


![](assets/images/saa/sqs6.png)


![](assets/images/saa/sqs7.png)

– When the ReceiveMessageWaitTimeSeconds property of a queue is set to a value greater than zero,long
polling is in effect. Long polling reduces the number of empty responses by allowing Amazon SQS to wait until a message is available before sending a response to a ReceiveMessage request. 

<h2>Amazon Simple Notification Service</h2>

Amazon Simple Notification Service (Amazon SNS) is a fully managed messaging service for both application-to-application (A2A) and application-to-person (A2P) communication.
![](assets/images/saa/sns.png)


![](assets/images/saa/sns1.png)

![](assets/images/saa/sns2.png)

Amazon SNS enables you to modernize your applications and decouple them into smaller, independent components that are easier to develop, deploy, and maintain. 

![](assets/images/saa/sns3.png)

![](assets/images/saa/sns4.png)


![](assets/images/saa/sns5.png)

![](assets/images/saa/sns6.png)

<h2>Amazon ElastiCache</h2>
Fully managed in-memory data store, compatible with Redis or Memcached. Power real-time applications with sub-millisecond latency.

![](assets/images/saa/es.png)


![](assets/images/saa/es1.png)


![](assets/images/saa/es2.png)

![](assets/images/saa/es3.png)

<h1>High availability - VIP</h1>

![](assets/images/saa/ha.png)


![](assets/images/saa/scio.png)

<h2>AWS Elastic Beanstalk</h2> is an easy-to-use service for deploying and scaling web applications and services 
without worrying about infastructure

You can simply upload your code and Elastic Beanstalk automatically handles the deployment, from capacity provisioning, load balancing, auto-scaling to application health monitoring.
There is no additional charge for Elastic Beanstalk - you pay only for the AWS resources needed to store and run your applications.

![](assets/images/saa/eb.png)

Elastic Beanstalk collects 40+ key metrics and attributes to determine the health of your application

![](assets/images/saa/es5.png)


<h2>Amazon API Gateway</h2>
 is a fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale. APIs act as the "front door" for applications to access data, business logic, or functionality from your backend services. Using API Gateway, you can create **RESTful APIs and WebSocket APIs that enable real-time two-way communication applications**. API Gateway supports containerized and serverless workloads, as well as web applications.

![](assets/images/saa/ag.png)

API Gateway **handles all the tasks involved in accepting and processing up to hundreds of thousands of concurrent API calls, including traffic management, CORS support, authorization and access control, throttling, monitoring, and API version management.** API Gateway has no minimum fees or startup costs. You pay for the API calls you receive and the amount of data transferred out and, with the API Gateway tiered pricing model, you can reduce your cost as your API usage scales.


![](assets/images/saa/ag2.png)

![](assets/images/saa/ag1.png)

![](assets/images/saa/ag3.png)


<h2>Amazon Kinesis</h2>
Easily collect, process, and analyze video and data streams in **real time**

![](assets/images/saa/ki.png)


![](assets/images/saa/ki1.png)


![](assets/images/saa/ki2.png)

![](assets/images/saa/ki4.png)


<h2>AWS Storage Gateway</h2>
On-premises access to virtually unlimited cloud storage

![](assets/images/saa/sg.png)

![](assets/images/saa/sg1.png)


![](assets/images/saa/sg2.png)



![](assets/images/saa/sg4.png)


![](assets/images/saa/sg5.png)

![](assets/images/saa/sg3.png)

![](assets/images/saa/sg6.png)















___
<h2>Other Apps:</h2>

**Analytics:**

**Amazon Athena**

Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL. Athena is serverless, so there is no infrastructure to manage. Amazon Athena allows you to tap into all your data in S3 without the need to set up complex processes to extract, transform, and load the data (ETL). Start querying data instantly. Get results in seconds. Pay only for the queries you run.


**AWS Glue**
Simple, scalable, and serverless data integration
Data integration is the process of preparing and combining data for analytics, machine learning, and application development. Data engineers and ETL (extract, transform, and load) developers can visually create, run, and monitor ETL workflows with a few clicks in AWS Glue Studio.


**Amazon Elasticsearch Service (Amazon ES)** is a managed service that makes it easy to deploy, operate, and scale Elasticsearch clusters in the AWS Cloud.

**Amazon OpenSearch Service** (successor to Amazon Elasticsearch Service) is a managed service that makes it easy to deploy, operate, and scale OpenSearch clusters in the AWS Cloud.


**Amazon EMR** is the industry-leading cloud big data platform for processing vast amounts of data using open source tools such as Apache Spark, Apache Hive, Apache HBase, Apache Flink, Apache Hudi, and Presto. 

**Amazon QuickSight - Business Intelligence Service**
Amazon QuickSight is a scalable, serverless, embeddable, machine learning-powered business intelligence (BI) service built for the cloud.


**AWS Billing and Cost Management:**

**AWS Cost Explorer** helps you visualize, understand, and manage your AWS costs and usage over a daily or monthly granularity.

**AWS Budgets** is the simplest way to monitor your AWS spend and be alerted when you exceed or are forecasted to exceed your desired spending limit.


Compute:

**AWS Fargate** is a serverless, pay-as-you-go compute engine that lets you focus on building applications without managing servers
**Amazon Elastic Kubernetes Service (EKS)** is a managed service and certified Kubernetes conformant to run Kubernetes on AWS and on-premises

**Amazon Elastic Container Service**
Amazon Elastic Container Service (Amazon ECS) is a fully managed container orchestration service that helps you easily deploy, manage, and scale containerized applications. 

**AWS Step Functions** is a low-code visual workflow service used to orchestrate AWS services, automate business processes, and build serverless applications.

Management and Governance:
**AWS Config**
AWS Config is a service that enables you to assess, audit, and evaluate the configurations of your AWS resources.

**AWS Organizations** helps you quickly scale your environment by allowing you to programmatically create new AWS accounts.


**AWS Resource Access Manager (RAM)** helps you securely share your resources across AWS accounts, within your organization or organizational units (OUs) in AWS Organizations, and with IAM roles and IAM users for supported resource types. You can use AWS RAM to share transit gateways, subnets, AWS License Manager license configurations, Amazon Route 53 Resolver rules, and more resource types.

**AWS Trusted Advisors** provides recommendations that help you follow AWS best practices. Trusted Advisor evaluates your account by using checks.

**AWS Systems Manager** is the operations hub for AWS. Systems Manager provides a unified user interface so you can track and resolve operational issues across your AWS applications and resources from a central place.


**Migration and Transfer:**

**AWS Database Migration Service (AWS DMS)** helps you migrate databases to AWS quickly and securely.


**AWS DataSync** is an online data transfer service that simplifies, automates, and accelerates moving **data** between on-premises storage systems and **AWS Storage services**, as well as between AWS Storage services.

**AWS Migration Hub** helps plan your migrations by allowing you to group related servers and resources that should be migrated together.

**AWS Server Migration Service (SMS)** is an agentless service which makes it easier and faster for you to migrate thousands of on-premises **workloads** to AWS.

**The AWS Transfer Family** provides fully managed support for file transfers directly into and out of **Amazon S3 or Amazon EFS**. With support for **Secure File Transfer Protocol (SFTP), File Transfer Protocol over SSL (FTPS), and File Transfer Protocol (FTP)**


**Networking and Content Delivery:**

**AWS Global Accelerator** combines advanced networking features with the dedicated AWS Global Network to improve your application network performance by up to 60%. When the internet is congested, AWS Global Accelerator optimizes the path to your application to keep packet loss, jitter, and latency consistently low.

**AWS Transit Gateway** connects **VPCs and on-premises networks** through a central hub. This simplifies your network and puts an end to complex peering relationships. It acts as a cloud router – each new connection is only made once.

**Security, Identity, and Compliance:**

**AWS Directory Service** provides multiple ways to set up and run Microsoft Active Directory with other AWS services such as Amazon EC2, Amazon RDS for SQL

**AWS Certificate Manager (ACM)** handles the complexity of creating, storing, and renewing public and private SSL/TLS X.509 certificates and keys that protect your AWS websites and applications.

**AWS Secrets Manager** helps you protect secrets needed to access your applications, services, and IT resources.

**AWS Shield** is a managed **Distributed Denial of Service (DDoS)** protection service that safeguards applications running on AWS.


**Amazon Macie** is a fully managed data security and data privacy service that uses machine learning and pattern matching to discover and protect your sensitive data in AWS.

**Storage:**

**Amazon S3 Glacier** is a secure, durable, and extremely low-cost Amazon S3 storage class for data archiving and long-term backup.
Archive Retrieval Options
You can specify one of the following when initiating a job to retrieve an archive based on your access time and cost requirements. For information about retrieval pricing, see the S3 Glacier Pricing.

Expedited — Expedited retrievals allow you to quickly access your data when occasional urgent requests for a subset of archives are required. For all but the largest archives (250 MB+), data accessed using Expedited retrievals are typically made available within 1–5 minutes. Provisioned Capacity ensures that retrieval capacity for Expedited retrievals is available when you need it. For more information, see Provisioned Capacity.

Standard — Standard retrievals allow you to access any of your archives   within 3–5 hours. This is the default option for retrieval requests that do not specify the retrieval option.

Bulk — Bulk retrievals are S3 Glacier’s lowest-cost retrieval option, which you can use to retrieve large amounts, even petabytes, of data inexpensively in a day. Bulk retrievals typically complete within 5–12 hours.

**Amazon FSx** makes it easy and cost effective to launch, run, and scale feature-rich, high-performance file systems in the cloud.


AWS SERVICES THAT ENABLE HIGH AVAILABILITY

Amazon Regions and Availability Zones
Amazon Virtual Private Cloud (VPC)
Amazon Elastic Load Balancing (ELB)
Amazon Simple Queue Service (SQS)
Amazon Elastic Cloud Compute (EC2)
Amazon Elastic IP Addresses (EIP)
Amazon Route53
Amazon CloudWatch
Amazon Auto Scaling



DR -Disaster recovery options in the cloud
![](assets/images/saa/dr.png)
