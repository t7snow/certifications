# Maarek SAA Notes

27 hours of video  
5 practice tests  
Targeted Anki review

Starting: April 29, 2026  
Ideal test date: June 1, 2026

## Section 1: Introduction

### Regions

- A Region is a cluster of data centers in a specific geographic area.
- Most AWS services are Region-scoped.
- Choosing a Region depends on:
  - Compliance, data governance, and legal requirements.
  - Proximity to customers.
  - Available services, because not every service exists in every Region.
  - Pricing.

### Availability Zones

- Each Region has multiple Availability Zones, usually at least 3.
- Example: `ap-southeast-2a`, `ap-southeast-2b`, and `ap-southeast-2c`.
- Each Availability Zone is one or more discrete data centers with redundant power, networking, and connectivity.
- Availability Zones are isolated from each other so failures should not cascade.
- Availability Zones are connected with high-bandwidth, ultra-low-latency networking.

### Points of Presence

- AWS has a large global edge network of Points of Presence.
- Points of Presence are used by services such as CloudFront and Route 53 to serve users closer to where they are.

### AWS Console Tour

- Route 53: DNS and domain routing.
- EC2: Virtual servers.

## IAM: Identity and Access Management

IAM is a global service.

- The root account is created by default and should not be used for day-to-day work or shared.
- A user represents one person or workload identity.
- Users can be placed into groups.
- Groups contain users only. There are no nested groups.
- A user can belong to multiple groups.
- Users and groups receive permissions through JSON policy documents.
- Tags give metadata to AWS resources.
- Permissions are easier to manage when inherited through groups.
- "Add session" lets you sign into multiple AWS accounts in the same browser.

### Policies in Depth

- Policy inheritance works the way you would expect: user permissions can come from attached user policies and group policies.
- A policy is a JSON document with elements such as:
  - `Version`: policy language version.
  - `Id`: optional policy identifier.
  - `Statement`: one or more permission statements.
  - `Sid`: optional statement identifier.
  - `Effect`: `Allow` or `Deny`.
  - `Principal`: who the policy applies to; mainly used in resource-based policies.
  - `Action`: API calls that are allowed or denied.
  - `Resource`: resources the actions apply to.
  - `Condition`: optional rules for when the statement applies.

### Password Policy and MFA

- Password policies can control password length, complexity, reuse, expiration, and whether users can change their own passwords.
- MFA means something you know, like a password, plus something you own, like a security device.
- MFA options include:
  - Virtual MFA devices, such as Authy or Google Authenticator.
  - U2F or FIDO security keys, such as YubiKey.
  - Hardware key fobs.
  - AWS GovCloud-compatible options such as SurePassID.

### Ways to Access AWS

- AWS Management Console: browser-based access.
- AWS CLI: command-line access using access keys.
- AWS SDKs: AWS API access from application code.
- Access keys are generated through the AWS console.
- Users manage their own access keys where allowed.
- Protect access keys like passwords.

### IAM Roles

- Some AWS services need to perform actions on your behalf.
- IAM roles give AWS services permissions without hardcoding credentials.
- Example: an EC2 instance can use an IAM role to call AWS APIs.
- Do not put IAM user access keys on EC2 instances. Attach an IAM role instead.
- Example flow:
  - Create an IAM role for EC2.
  - Attach a policy, such as read-only permissions.
  - Attach that role to the EC2 instance.
  - The instance can now call allowed AWS APIs.

### IAM Reports and Advisor

- IAM credential report: account-level report showing user credential details, such as password and access key status.
- IAM Access Advisor: shows when services were last accessed. Useful for permission audits.
- These help figure out which users, passwords, keys, and permissions need attention.

### IAM Best Practices

- Do not use the root account except for AWS account setup or rare root-only tasks.
- One physical person equals one IAM user or federated identity.
- Assign users to groups.
- Enforce MFA.
- Create and use roles for AWS service permissions.
- Use access keys only for programmatic access.
- Audit permissions regularly.
- Never share credentials.

## EC2 Fundamentals

- EC2 is one of the core AWS services.
- Elastic Compute Cloud is Infrastructure as a Service.
- EC2 lets you:
  - Rent virtual machines, called EC2 instances.
  - Store data on EBS volumes, which are virtual drives.
  - Distribute load with Elastic Load Balancing.
  - Scale using Auto Scaling Groups.
- EC2 supports Linux, Windows, and macOS.
- Main choices when launching an instance:
  - Compute and CPU cores.
  - RAM.
  - Storage: network-attached or hardware-attached.
  - Network card.
  - Firewall rules through security groups.
  - Bootstrap script through EC2 user data.
- EC2 user data is used to automate boot tasks such as installing updates and common files.
- EC2 user data runs as the root user.

### EC2 Instance Types

- General purpose.
- Compute optimized.
- Memory optimized.
- Accelerated computing.
- Storage optimized.
- Example: `m5.2xlarge`
  - `m`: instance family.
  - `5`: generation.
  - `2xlarge`: size within the family.
- General purpose instances are good for web servers, small databases, code repositories, and balanced workloads.
- `t2.micro` and similar burstable instances are general purpose.
- Compute optimized instances are good for batch processing, media transcoding, high-performance computing, machine learning inference, and CPU-heavy workloads.

### Security Groups

- Security groups are virtual firewalls around EC2 instances.
- Security groups only contain allow rules.
- Rules can reference IP ranges or other security groups.
- Each rule includes protocol, port, and source or destination.
- SSH should usually have a dedicated security group.
- By default:
  - All inbound traffic is blocked.
  - All outbound traffic is allowed.
- If an EC2 connection times out, check security group inbound rules first.

### Important Ports

- FTP: 21.
- SSH: 22.
- SFTP: 22, because it runs over SSH.
- HTTP: 80.
- HTTPS: 443.
- RDP for Windows instances: 3389.

## SSH and EC2 Instance Connect

- EC2 Instance Connect gives browser-based SSH access.
- It uploads a temporary SSH key and opens a browser CLI.
- EC2 Instance Connect commonly uses the default username for the AMI, such as `ec2-user` on Amazon Linux.
- Again: do not put IAM access keys on EC2 instances. Use IAM roles.

## EC2 Purchasing Options

- On-Demand Instances: short workloads with predictable pricing and no long-term commitment.
- Reserved Instances: long-running steady workloads. Can be standard or convertible.
- Savings Plans: commitment to a certain amount of usage over time.
- Spot Instances: short, fault-tolerant workloads. You can lose capacity if the Spot price or capacity situation changes.
- Dedicated Hosts: physical servers dedicated to you.
- Dedicated Instances: instances run on hardware dedicated to you, but you do not control the host placement the same way as Dedicated Hosts.
- Capacity Reservations: reserve On-Demand capacity in a specific Availability Zone.

### On-Demand

- Billing is per second after the first minute for many instance types.
- Highest cost, but no upfront payment and no commitment.
- Good when you need flexibility.

### Reserved Instances and Savings Plans

- Reserved Instances can give large discounts for steady-state usage.
- Reserved Instances are defined by attributes such as instance type, Region, operating system, tenancy, term, payment option, and scope.
- Convertible Reserved Instances let you change instance family, operating system, scope, or tenancy and still keep a discount.
- EC2 Instance Savings Plans discount usage based on a long-term hourly spend commitment.
- Savings Plans are more flexible than classic Reserved Instances, depending on the plan type.

### Spot Instances and Spot Fleets

- Spot Instances can save up to 90% compared with On-Demand.
- You can use Spot while capacity is available and your maximum price is compatible.
- If AWS interrupts your Spot Instance, you get a two-minute interruption notice.
- Good for batch jobs, data analysis, image processing, distributed workloads, and anything resilient to failure.
- Not good for critical databases or workloads that cannot tolerate interruption.
- A Spot request can be:
  - One-time: launches when available and then finishes.
  - Persistent: keeps trying to maintain the requested capacity.
- Spot Fleet is a set of Spot Instances, and optionally On-Demand Instances.
- A launch pool is a combination of instance type, operating system, Availability Zone, and other launch details.
- Spot allocation strategies include:
  - Lowest price.
  - Diversified.
  - Capacity optimized.
  - Price capacity optimized, which is commonly recommended.
- Spot Fleet can automatically request Spot capacity from the best pools based on your strategy.

### Dedicated Hosts and Capacity Reservations

- Dedicated Hosts help with compliance and server-bound software licenses.
- Dedicated Hosts can be purchased On-Demand or reserved.
- Dedicated Instances run on hardware dedicated to one customer.
- Capacity Reservations reserve On-Demand capacity in a specific Availability Zone.
- Capacity Reservations have no time commitment.
- You pay whether or not you run instances against the reservation.
- Good for short-term uninterrupted workloads where capacity must be available.

### Elastic IP

- An Elastic IP is a static public IPv4 address you keep until you release it.
- It can be moved between instances and used to mask instance failure.
- AWS accounts have a small default quota for Elastic IPs.
- Overusing Elastic IPs is usually poor architecture.
- Prefer DNS names and load balancers when possible.

## Placement Groups

Placement groups influence how EC2 instances are placed on AWS hardware.

### Cluster Placement Group

- Instances are packed close together inside a single Availability Zone.
- Great for low latency and high network throughput.
- Use case: big data job or tightly coupled compute workload.
- Risk: if the Availability Zone has an issue, the whole group is affected.

### Spread Placement Group

- Instances are spread across different hardware.
- Can span multiple Availability Zones.
- Max 7 instances per Availability Zone per group.
- Good for critical applications where each instance should be isolated.

### Partition Placement Group

- Instances are spread across partitions.
- Each partition is isolated from failures in other partitions.
- Each partition maps to separate racks of hardware.
- Can scale to hundreds of EC2 instances.
- Use case: big data systems such as Hadoop, Cassandra, or Kafka.

## Elastic Network Interfaces

- An Elastic Network Interface is a virtual network card in a VPC.
- ENIs can provide:
  - Primary private IPv4 address.
  - One or more secondary private IPv4 addresses.
  - One Elastic IP per private IPv4 address.
  - One public IPv4 address.
  - One or more security groups.
  - MAC address.
- ENIs are bound to a specific Availability Zone.
- You can create ENIs independently and attach, detach, or move them between instances in the same Availability Zone.
- This is useful for failover because the network identity can move.
- ENIs are not physical network cards. They are an abstraction on top of AWS networking.

## EC2 Hibernate

- Stop: data on EBS root volume is kept until the next start.
- Terminate: root EBS volume is deleted if delete-on-termination is enabled.
- Hibernate: RAM state is preserved to the encrypted EBS root volume.
- On hibernate, the OS is paused instead of fully stopped.
- Good for:
  - Long-running processes.
  - Preserving RAM state.
  - Services that take time to initialize.
- Requirements and notes:
  - Root volume must be EBS and encrypted.
  - Root volume must have enough space to store RAM contents.
  - Not supported for bare metal instances.
  - Instance RAM size limit applies.
  - Hibernate duration has a maximum supported period.

## EC2 Instance Storage

### EBS Volumes

- EBS means Elastic Block Store.
- An EBS volume is a network drive attached to EC2 instances.
- It can persist data after instance termination, depending on delete-on-termination settings.
- Most EBS volumes attach to one EC2 instance at a time.
- EBS volumes are bound to a specific Availability Zone.
- Think of EBS as a network USB drive.
- Because it is network-attached, there is some latency.
- You provision capacity, IOPS, and throughput depending on volume type.
- Volumes can be detached and reattached on demand.

### Delete on Termination

- Root EBS volumes are deleted by default when the instance is terminated.
- Additional attached EBS volumes are not deleted by default.
- You can change delete-on-termination behavior.
- This matters if you need to preserve the root volume after terminating an instance.

### EBS Snapshots

- An EBS snapshot is a backup of an EBS volume.
- Snapshots can be copied across Availability Zones through volume restore, and across Regions through snapshot copy.
- You can recreate a volume from a snapshot.
- Snapshot Archive is cheaper storage for snapshots, but restore takes much longer.
- Recycle Bin for EBS snapshots helps protect against accidental deletion.
- Fast Snapshot Restore removes first-use latency, but it is expensive.

## AMI

- AMI means Amazon Machine Image.
- An AMI is a customized image for launching EC2 instances.
- AMIs are built for a specific Region, but can be copied across Regions.
- AMI sources:
  - AWS-provided AMIs.
  - Your own custom AMIs.
  - AWS Marketplace AMIs.
- Common flow:
  - Launch instance.
  - Customize it.
  - Stop it.
  - Build AMI, which creates EBS snapshots.
  - Launch new instances from the AMI.

## EC2 Instance Store

- Instance store is storage physically attached to the host server.
- It provides very high performance.
- It is ephemeral: data is lost if the instance stops, terminates, or the underlying disk fails.
- Good for cache, buffer, scratch data, and temporary content.
- Not a long-term storage place.

## EBS Volume Types

- `gp2` and `gp3`: general purpose SSD.
- `io1` and `io2`: provisioned IOPS SSD for low latency and high performance.
- `st1`: throughput optimized HDD.
- `sc1`: cold HDD.
- SSD-backed volumes are for IOPS-heavy workloads.
- HDD-backed volumes are for throughput-heavy workloads.
- Only SSD-backed EBS volumes are typically used as boot volumes.

### General Purpose SSD

- Good for cost-effective storage, virtual desktops, development environments, and many general workloads.
- `gp3` separates IOPS and throughput from volume size.
- `gp3` has baseline performance included, with optional provisioned IOPS and throughput.
- `gp2` performance is tied to volume size.

### Provisioned IOPS SSD

- Good for database workloads that need consistent high performance.
- `io1` and `io2` support EBS Multi-Attach.
- `io2` is newer and has better durability and performance options.

### HDD Volumes

- `st1` is good for big data, data warehouses, and log processing.
- `sc1` is for cold data that is accessed less frequently.
- HDD volumes cannot be boot volumes.

### EBS Multi-Attach

- Multi-Attach allows the same EBS volume to attach to multiple EC2 instances in the same Availability Zone.
- Only supported on `io1` and `io2`.
- Gives full read/write access from multiple instances.
- The application must manage concurrent writes correctly.
- Limit is up to 16 EC2 instances at a time.
- **Exam:** Multi-Attach does not magically make a normal file system safe for concurrent writes.

### EBS Encryption

- EBS encryption protects:
  - Data at rest.
  - Snapshots.
  - Volumes created from snapshots.
  - Data in flight between the instance and the volume.
- Encryption is handled transparently.
- Uses AWS KMS and AES-256.
- Minimal latency impact.
- You can encrypt an unencrypted volume by creating a snapshot, copying it as encrypted, creating a new encrypted volume, and attaching it.

## EFS

- EFS means Elastic File System.
- It is a managed network file system.
- It can be mounted by many EC2 instances across multiple Availability Zones.
- It is more expensive than EBS, but you pay for usage.
- Uses NFSv4.1 and supports POSIX-style file system behavior.
- Works with Linux clients.
- Can scale to many concurrent NFS clients.
- Performance modes and throughput options include bursting, provisioned, and elastic throughput.
- Storage classes include:
  - EFS Standard.
  - EFS Standard-Infrequent Access.
  - EFS One Zone.
  - EFS Archive.
- Lifecycle policies can move files between storage classes after a number of days.

### EFS vs. EBS

- EBS is usually attached to one instance at a time and locked to one Availability Zone.
- EBS can be moved by snapshotting and restoring in another Availability Zone.
- `gp2` performance increases with volume size.
- `gp3` performance can be increased independently.
- EFS can mount to hundreds or thousands of instances across Availability Zones.
- EFS is good for shared website files, such as WordPress content.

## High Availability and Scalability: ELB and ASG

- Vertical scaling means increasing the size of an instance.
- Horizontal scaling means adding more instances.
- Elasticity means the system can scale out and in based on demand.

### Load Balancing

- A load balancer forwards traffic to downstream targets such as EC2 instances.
- It gives users a single DNS endpoint.
- It helps handle failures, distribute load, terminate SSL/TLS, and spread traffic across Availability Zones.
- AWS manages the load balancer service.
- Health checks verify that targets are working, often by hitting a path such as `/health`.

### Load Balancer Types

- Classic Load Balancer: older generation.
- Application Load Balancer: HTTP, HTTPS, and WebSocket. Layer 7.
- Network Load Balancer: TCP, UDP, and TLS. Layer 4.
- Gateway Load Balancer: network appliances. Layer 3.

### Application Load Balancer

- ALB operates at Layer 7.
- Supports HTTP, HTTPS, and WebSocket.
- Can route to multiple HTTP applications.
- Supports path-based and host-based routing.
- Routes to target groups.
- Target groups can include:
  - EC2 instances.
  - ECS tasks.
  - Lambda functions.
  - Private IP addresses.
- Typical flow:
  - Create a target group.
  - Create an ALB.
  - Configure an HTTP or HTTPS listener.
  - Listener forwards traffic to the target group.

### Network Load Balancer

- NLB operates at Layer 4.
- Supports TCP, UDP, and TLS.
- Can handle millions of requests per second.
- Ultra-low latency.
- Has one static IP per Availability Zone.
- You can assign an Elastic IP per Availability Zone.
- NLB can route to EC2 instances, IP addresses, and Application Load Balancers.
- Health checks support TCP, HTTP, and HTTPS.
- **Exam:** NLB is the static IP and extreme performance load balancer.

### Gateway Load Balancer

- GWLB is used for third-party virtual network appliances in AWS.
- Examples: firewalls, intrusion detection systems, and packet inspection appliances.
- Traffic flow:
  - User traffic enters GWLB.
  - GWLB sends traffic to the appliance target group.
  - Appliance allows or drops traffic.
  - GWLB forwards allowed traffic to the application.
- It operates at Layer 3, the network layer.
- Uses the GENEVE protocol on port 6081.
- Acts as both a transparent network gateway and a load balancer.

### Sticky Sessions and Cookies

- Sticky sessions keep a client routed to the same target.
- Useful when session data is stored locally on the target.
- Application-based cookies are generated by the target.
- Duration-based cookies are generated by the load balancer.
- Some cookie names are reserved and cannot be used.

### Cross-Zone Load Balancing

- ALB has cross-zone load balancing always enabled.
- NLB and GWLB have cross-zone load balancing disabled by default, but it can be enabled.
- Cross-zone load balancing distributes traffic across registered targets in enabled Availability Zones.

### SSL/TLS and SNI

- SSL/TLS provides in-flight encryption.
- TLS is the newer protocol; people still often say SSL casually.
- Certificates come from certificate authorities.
- ACM means AWS Certificate Manager.
- HTTPS listeners use certificates.
- SNI means Server Name Indication.
- SNI lets a load balancer serve multiple certificates on the same listener by using the hostname from the TLS handshake.
- SNI works with ALB and NLB, not Classic Load Balancer.

### Connection Draining

- Classic Load Balancer calls it connection draining.
- ALB and NLB call it deregistration delay.
- It gives in-flight requests time to complete before a target is removed.
- Range is 1 to 3600 seconds.
- Default is 300 seconds.
- Lower values are good for short requests.

### Auto Scaling Groups

- An Auto Scaling Group changes capacity as load changes.
- ASG itself is free; you pay for the resources it launches.
- ASG can use ELB health checks in addition to EC2 health checks.
- A launch template defines how EC2 instances are launched.
- Scaling can be based on CloudWatch metrics and alarms.
- Dynamic scaling options:
  - Target tracking, such as average CPU percentage.
  - Simple scaling.
  - Step scaling.
- Scheduled scaling works for known usage patterns.
- Predictive scaling forecasts load and schedules capacity.

## AWS Database Fundamentals: RDS, Aurora, and ElastiCache

## RDS

- RDS means Relational Database Service.
- It is a managed SQL database service.
- Engines include PostgreSQL, MySQL, MariaDB, Oracle, Microsoft SQL Server, and Amazon Aurora.
- AWS manages OS patching, backups, and much of the operational overhead.
- You cannot SSH into standard RDS database instances.

### RDS Storage Auto Scaling

- RDS can automatically increase storage when needed.
- This helps avoid manual scaling.
- Set a maximum storage threshold so it has room to grow.

### Read Replicas

- Read replicas scale read workloads.
- Replication is asynchronous.
- Read replicas are eventually consistent.
- Read replicas can be in the same Availability Zone, across Availability Zones, or cross-Region depending on engine support.
- A read replica can be promoted to its own standalone database.
- Good use case: reporting application.
- Network cost note:
  - Same Region and cross-AZ replication for RDS read replicas generally does not charge replication data transfer.
  - Cross-Region replication does have data transfer costs.

### Multi-AZ

- Multi-AZ is for disaster recovery and high availability.
- Uses one DNS name with automatic failover to the standby.
- Not for scaling reads, unless using newer Multi-AZ DB cluster patterns.
- You can usually convert single-AZ to Multi-AZ without downtime.

### RDS Custom

- RDS Custom is available for Oracle and Microsoft SQL Server.
- It gives access to the OS and database environment for customization.
- You can configure settings, patches, and the underlying EC2 instances more directly.

## Amazon Aurora

- Aurora is compatible with MySQL and PostgreSQL.
- It is cloud-optimized and can provide major performance improvements over standard MySQL/PostgreSQL on RDS.
- Storage automatically grows in increments as needed, up to very large cluster limits.
- Aurora supports up to 15 read replicas.
- Failover is fast.
- Usually costs more than standard RDS, but gives better performance and availability.
- Aurora stores 6 copies of data across 3 Availability Zones.
- Writes require a quorum; reads can tolerate more failures.
- Storage is self-healing and distributed across many volumes.
- One instance is the writer.
- Multiple instances can be readers.
- The writer endpoint points to the current writer instance.
- Reader endpoint load balances connections across read replicas.
- Aurora handles routine maintenance, backups, patching, scaling, and compliance features.

### Aurora Advanced Features

- Aurora Auto Scaling can add or remove read replicas.
- Custom endpoints can target specific groups of DB instances.
- Aurora Serverless automatically starts, stops, and scales database capacity.
- Good for infrequent, intermittent, or unpredictable workloads.
- Aurora Global Database:
  - One primary Region for reads and writes.
  - Secondary Regions are read-only.
  - Designed for low-latency global reads and disaster recovery.
- Aurora can integrate with AWS ML services such as SageMaker and Comprehend.
- Babelfish for Aurora PostgreSQL helps applications that use SQL Server T-SQL communicate with Aurora PostgreSQL.
- AWS SCT and AWS DMS help with database migration.

### RDS Backups

- Automated backups include daily full backups during the backup window.
- Transaction logs are backed up frequently for point-in-time recovery.
- Automated backup retention is 1 to 35 days.
- Point-in-time recovery can restore to a specific time inside the retention window.
- Manual snapshots are retained until deleted.
- **Exam trick:** If an RDS database is stopped, you still pay for storage.
- If stopping for a long time, consider snapshotting and restoring later instead.
- Aurora database cloning creates a new cluster from an existing one quickly and cost-effectively.

### RDS and Aurora Security

- At-rest encryption uses KMS.
- Read replicas cannot be encrypted if the source database is not encrypted.
- To encrypt an unencrypted database, snapshot it, copy the snapshot as encrypted, and restore from the encrypted snapshot.
- In-flight encryption uses TLS.
- IAM database authentication can be used with supported engines.
- Security groups control network access.
- No SSH for standard managed RDS.
- Audit logs can be sent to CloudWatch Logs for retention.

### RDS Proxy

- RDS Proxy lets applications pool and share database connections.
- It improves efficiency and reduces pressure on the database.
- It is highly available across multiple Availability Zones.
- It can reduce failover time.
- No major code rewrite is needed; change the application connection endpoint.
- RDS Proxy is never publicly accessible. It runs inside a VPC.
- Very useful for Lambda functions because Lambda can scale out quickly and create too many direct database connections.

## ElastiCache Overview

- ElastiCache is managed Redis or Memcached.
- It reduces database load for read-heavy workloads.
- It is commonly used for caching and session stores.
- AWS manages much of the operations work.
- Applications usually need code changes to use caching well.

### Redis

- Supports Multi-AZ with automatic failover.
- Supports persistence options.
- Supports sets and sorted sets.
- Supports IAM authentication for some Redis use cases and Redis AUTH tokens.
- Great for gaming leaderboards because Redis sorted sets guarantee uniqueness and ordering.
- When a score changes, ranking can update in real time.

### Memcached

- Simple distributed cache.
- Supports multiple nodes for partitioning data.
- Not designed for high availability in the same way Redis is.
- Non-persistent.
- Supports SASL-based authentication.

### Caching Strategies

- Lazy loading: data is loaded into the cache only when requested. Cached data can become stale.
- Write-through: data is added or updated in the cache when it is written to the database.
- Session store: temporary session data lives in cache.

### Important Database Ports

- PostgreSQL: 5432.
- MySQL: 3306.
- MariaDB: 3306.
- Oracle RDS: 1521.
- Microsoft SQL Server: 1433.
- Aurora PostgreSQL-compatible: 5432.
- Aurora MySQL-compatible: 3306.

## Route 53

### DNS

- DNS means Domain Name System.
- DNS translates human-friendly hostnames into machine IP addresses.
- Example hierarchy: root zone, `.com`, `example.com`, `www.example.com`.
- Registrar: where the domain is registered, such as GoDaddy or Route 53 Domains.
- DNS record: mapping or instruction for a domain name.
- Zone file: file containing DNS records.
- Name server: server that answers DNS queries for a zone.
- TLD: top-level domain, such as `.com`.
- SLD: second-level domain, such as `example` in `example.com`.
- FQDN: fully qualified domain name.

### Route 53 Overview

- Route 53 is a scalable managed DNS service.
- It is authoritative DNS, meaning customers can manage records for their domains.
- The name comes from DNS port 53.
- Records tell Route 53 how to route traffic for a domain.
- A record includes:
  - Domain name.
  - Record type.
  - Value.
  - Routing policy.
  - TTL, except alias records where TTL is managed by AWS.
- Common record types:
  - `A`: hostname to IPv4.
  - `AAAA`: hostname to IPv6.
  - `CNAME`: hostname to another hostname.
  - `NS`: name servers for the hosted zone.
- Hosted zones:
  - Public hosted zone: public DNS.
  - Private hosted zone: DNS inside one or more VPCs.

### TTL

- TTL means Time To Live.
- Higher TTL means less DNS traffic and more caching.
- Lower TTL means faster changes but more DNS queries and potentially more cost.

### CNAME vs. Alias

- CNAME points one hostname to another hostname.
- CNAME cannot be used at the zone apex, such as `example.com`.
- Alias records are Route 53 extensions that point a hostname to an AWS resource.
- Alias records work at both root and non-root domains.
- Alias records are free and integrate with AWS resources.
- Alias records automatically track some AWS resource IP changes.
- Alias targets include ELB, CloudFront, API Gateway, Elastic Beanstalk, S3 website endpoints, VPC endpoints, Global Accelerator, and other Route 53 records.
- You cannot create an alias directly to an EC2 public DNS name.

### Routing Policies

- Simple routing: route traffic to a single resource or multiple values without special routing logic.
- Weighted routing: send percentages of traffic to different resources by weight.
- Latency-based routing: route to the Region with the lowest latency for the user.
- Failover routing: active-passive failover using health checks.
- Geolocation routing: route based on user location, such as continent, country, or US state.
- Geoproximity routing: route based on resource and user location, with optional bias to shift more or less traffic.
- IP-based routing: route based on client IP CIDR ranges.
- Multivalue answer routing: return up to eight healthy records. Client-side selection does the rest.

### Health Checks

- Route 53 health checks are for public endpoints.
- Health checks can support automated DNS failover.
- Health checkers around the world check endpoints for healthy responses.
- Protocols include HTTP, HTTPS, and TCP.
- Calculated health checks combine multiple health checks.
- For private resources, use CloudWatch metrics and alarms, then base health checks on the alarm.

### Domain Registrar vs. DNS Service

- A domain registrar manages domain registration.
- A DNS service manages DNS records.
- They can be the same company, but do not have to be.
- To use Route 53 with a domain registered elsewhere:
  - Create a hosted zone in Route 53.
  - Update the domain's name servers at the registrar to the Route 53 name servers.

### Route 53 Resolver

- Route 53 Resolver automatically answers DNS queries for:
  - Local VPC domain names.
  - Records in private hosted zones.
  - Public DNS names.
- Hybrid DNS can connect AWS and on-premises DNS.
- Resolver endpoints allow DNS forwarding into or out of VPCs.
- Inbound endpoints let on-premises DNS resolve AWS private hosted zone names.
- Outbound endpoints let AWS workloads forward DNS queries to on-premises DNS over VPN or Direct Connect.

## Classic Solution Architecture Discussions

### Elastic Beanstalk

- Elastic Beanstalk is a managed service that gives one interface for deploying an application.
- Beanstalk itself is free, but you pay for the underlying AWS resources.
- Concepts:
  - Application.
  - Application version.
  - Environment.
  - Tiers, such as web tier and worker tier.
- Web tier:
  - Typically uses ELB, Auto Scaling, EC2, and multiple Availability Zones.
- Worker tier:
  - Uses an SQS queue instead of an ELB.
  - The queue decouples incoming work from background processing.

## S3

- S3 is object storage with extremely high durability.
- Use cases:
  - Backup and storage.
  - Disaster recovery.
  - Archive.
  - Hybrid cloud storage.
  - Static website hosting.
  - Data lakes.

### Buckets and Objects

- Buckets are created in a Region.
- Bucket names are globally unique across all AWS accounts and Regions.
- Bucket naming rules include no uppercase letters and no underscores.
- Objects are stored in buckets.
- An object key is the full path-like name.
- There are no real directories, just prefixes in object keys.
- Object values are the content/body.
- Maximum object size is 5 TB.
- Use multipart upload for large objects, especially objects over 100 MB.
- A single `PutObject` can upload up to 5 GB.
- Object metadata stores key-value information about the object.

### S3 Security

- User-based access uses IAM policies.
- Resource-based access uses bucket policies.
- Bucket policies are JSON documents attached to buckets.
- Cross-account access is commonly done with bucket policies.
- ACLs exist, but are less common now and usually avoided unless specifically needed.

### Static Website Hosting

- S3 can host static websites.
- The bucket must be configured for website hosting.
- Public access and bucket policy settings must allow access where appropriate.

### Versioning

- Versioning is enabled at the bucket level.
- Versioning keeps multiple versions of an object key.
- Best practice: enable versioning when you need protection against accidental overwrite or deletion.
- You can restore previous versions.
- Suspending versioning does not delete old versions.

### S3 Replication

- CRR means Cross-Region Replication.
- SRR means Same-Region Replication.
- Replication is asynchronous.
- Buckets can be in different AWS accounts if permissions are configured.
- CRR is good for compliance, lower latency access in another Region, and cross-Region disaster recovery.
- SRR is good for log aggregation, live replication between production and test accounts, and same-Region copies.
- After replication is enabled, only new objects are replicated by default.
- Use S3 Batch Replication to replicate existing objects.
- No chaining: if bucket 1 replicates to bucket 2, bucket 2 will not automatically replicate those replicated objects to bucket 3.

### S3 Storage Classes

- Durability means how unlikely data loss is.
- S3 Standard and most S3 storage classes are designed for 11 nines of durability.
- Availability means how often the object is accessible.
- S3 Standard is general purpose storage.
- Standard-IA is for infrequently accessed data with rapid access when needed.
- One Zone-IA stores data in one Availability Zone, so data can be lost if that AZ is destroyed.
- Glacier classes are for archive storage and have retrieval considerations.
- Intelligent-Tiering monitors access patterns and moves objects automatically between tiers. It has monitoring charges but no retrieval charges for most access tiers.

| Feature | Standard | Intelligent-Tiering | Standard-IA | One Zone-IA | Glacier Instant Retrieval | Glacier Flexible Retrieval | Glacier Deep Archive |
|---|---:|---:|---:|---:|---:|---:|---:|
| Designed durability | 99.999999999% | 99.999999999% | 99.999999999% | 99.999999999% | 99.999999999% | 99.999999999% | 99.999999999% |
| Availability | 99.99% | 99.9% | 99.9% | 99.5% | 99.9% | 99.99% | 99.99% |
| Availability SLA | 99.9% | 99% | 99% | 99% | 99% | 99.9% | 99.9% |
| Availability Zones | >= 3 | >= 3 | >= 3 | 1 | >= 3 | >= 3 | >= 3 |
| Minimum storage duration | None | None | 30 days | 30 days | 90 days | 90 days | 180 days |
| Minimum billable object size | None | None | 128 KB | 128 KB | 128 KB | 40 KB | 40 KB |
| Retrieval fee | None | None | Per GB retrieved | Per GB retrieved | Per GB retrieved | Per GB retrieved | Per GB retrieved |

### S3 Express One Zone

- S3 Express One Zone is high-performance single-AZ object storage.
- Objects are stored in a directory bucket in one Availability Zone.
- It is designed for very low-latency access and high request rates.
- Best when storage and compute are colocated in the same Availability Zone.
- Use cases include AI/ML training, analytics, and financial modeling.
