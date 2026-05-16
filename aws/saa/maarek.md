# stuff

27 Hours of Video
5 Practice Tests
Targeted Anki Review

Starting: April 29th 2026
Ideal test date: June 01. 
# section 1 - introduction

+ regions
- us-east-1 -> cluster of datacenters. most services are region scoped. 
- where to do it? -> it depends: compliance with data governance and legal requirements, proximity to customers, available services (not all have all), pricing,
+ availability zone
- each region has many zones, min 3 max 6, 
- ap-southeast-2: 2a,2b,2c each zone is one or more discrete datacenters with redundant power, networking, and connectivity. each zone is isolated and wont have cascading disasters. connected with highbandidth ultra low latency. 
+ points of prescence:
- 400+ POP in 90+ cities and 40+ countries

+ tour of aws console
- route 53? 
- EC2? 

## IAM - Identity and Access Managment, GLOBAL SERVICE
+ Root account created by default, shouldnt be used or shared. 
+ user = one perosn. can be grouped.
+ groups only have users, no recursive groups.
+ user can belong to multiple groups. 
+ users or groups are assigned a json documents called policies
+ tags -> give metadata to resources
+ easier to manage permissions with inherited perms
+ add session allows for two different accounts on two different browser windows - think this stops the private browser thing from being needed.
+ 

### Policies Indepth
+ inheritance how you would expect
+ json document - Version number, ID, Statement: [Sid, Effect, Principlal, ASctiopn, Resource]
++ sid: identifier (optional)
++ effect: if it allows or denies certian things
++ principl;e - who it applies to, which groups, etc. 
++ action: list of api calls denied or allowed
++ resources: list of resources shits applied to 
++ condition: when it should be put in effect (optional)

### Password Policy
+ change, reuse, expiration, etc. 
+ MFA - password  you know+ security device you own. 
+ virtual MFA device, authy, U2F - universal 2nd factor : YubiKey, Hardware Key Fob , AWS GovCLoud SurePassID

### how to access
+ aws managemnt console 
+ CLI - access keys protect it.
+ SDK - for code , api from aws from within your application code. 
+ access keys are gneerated through the aws console. users manage your access keys. 
### Roles
+ some aws actions perform actions on our behalf, need some kind of permissions to AWS Services = IAM Role
+ IAM Role for agents? / services
+ EC2 Instance -> virtual server. perform functions on aws IAM Role.A
+ IAM Cred Report
+ AM ADvisor - 
+ Credentials report: you can download a cred report about a bunch of shit
+ figure out when people change passwords, account, etc. which deserve attention
+ iam advisor last access which services were accessed last. 
+ Best PRactices : Do not use root account except for aws accoutn setup. one physical user= one aws user.
+ assign users to groups and enforce MFA. 
+ create and use roles for giving permissions to aws. 
+ use access keys for programmatic ascess. Audit permissions, never sare.


## EC2 Fundamentals

+ EC2 - most popular 
+ Elastic Compute Cloud = Infrastructure as a Service: 
+ Renting Virtual Machines (EC2 Instances) 
+ Storing on EBS ( Virtual Drives)
+ Distributing Load across machines (ELB)
+ Scaling using autoscaling group (ASG)
+ EC2 - Linux, Windows, MacOs 
+ How much compute and cores 
+ How much Random Access Memory
+ How much storage space - Network Attached or hardware attached
+ Network Card
+ Firewall Rules
+ Bootstrap script ( EC2 USer Data) 
+ automate updates, comon files, etc. 
+ Run with the root user
### EC2 Instance Types
+ General Purpose
+ Compute Optimized 
+ Memory Optimized
+ Accelerated Comuting
+ Storage Computing
+ m5.2xlarge - m: instance class, 5: generation, 2xlarge: size within the instance class
+ Genereal Purpose: WEb servers or code repositories, good balance between compute memory networking. t2micro general prupose. 
+ Compute Optimized - batch processm,ing, media, HPC, machine learnign, etc. 

### Security GHroups
+ only contain allow rules - ip or groups 
+ www -> ec2 : security around ec2. rules arund ec2. 
+ protocol, port, ep, etc. 
+ ssh should have its own security group
+ outside the ec2, all inbound is blocked, all outbound is allowed, by default. 

### misc
+ 22 - ssh, 21 - ftp, 22 - sftp, 80 http, 443 - https, 3389 - remote desktop protocol (windows instances) 
+ timeout => always a EC2 security rule most likely. 
+ outbound rules: 

## ssh 
+ EC2 Instance Connect - web browser good for all. only works for amazon linux 2. 
+ EC2 Instance COnnect: username. connect to instance. uploads a temp ssh key. gives a web browser cli. 
+ dont iam keys into ec2 instance. create iam roles
+ attach certain iamroels into the instance. this allows you to list users. added IAM Read Only Access to a certain EC2 Instance Role. ? confused on this.
+ attached a policy to a iam role that corresponds to EC2 role. 
## EC2 again
+ ondemand instances - short workload predicable pricing
+ reserved - long workloads with flexible instances are convertible reserved instances
+ savings plan - commitment to amount of usage, long workload. 
_ spot instances - short workload. can lose these though? 
+ dedicated - physical server, instance = hardweare
+ ONDEMAND - billing per second after the first minute - highest cost but no upgront payment, no commitment. 
+ RESERVED - HIGH DISCOUNT - instance attribute, region, os etc., reservation period, upfront or no, scope of region or zone, steady state usage applications. buy and sell in marketplace. convertible reserved instances - change the EC2 instance type. 66% discount. EC2 savings plan. discount based on long term usage commit to a certain type of usage. locked to a region or instance family. intsance size is flexible/ os/ tenance . E
+ EC2 SPOT- u can lose if your max price is les than the current spot price. workloads that are resilient to failure are for these. - not goof for anything secure or needed
+ EC2 Dedicated hosts - address compliance requiremens and existing serverbound software licences.e Reserve or on demand. Reserving a phyusical server. Useful for software that have compliance - good for compliance.
+ EC2 Dedicated Instances - instances run on hardware that dedicated to you.own hwardare, host - physical server. 
+ EC2 Capacity Reservation - On-Demand instances capacity in specific AZ? for any direction. No time commitment, just trying to reserve. charged at on-demad rate whether or not you run.  good for short term uninterupted workload. 

### spot instances and spot fleet
+ discount of up to 90%. define max spot price, while current < max then you have it. hourly rate varies based on supply demand. teminate or stop based on the 2  minute grace period. used for batch jobs, analysis, workloads failure. NO DATABASES. AZ = Availability Zone
+ terminate spot instance - one time or persistent. one time u requrest create then goeas away. persistent it keeps requesting until ends. 
+ fleet- picks the best launch pool ( instance type, os az) 
+ multiple launch pools - lowestPrice, diversified (distributed across pools), spot fleet = set of spot instances + on demand instanfces, capcityOptimized, priceCapacityOptimized (recomennded). 
+ spot fleet allow us to atuimatically request spot instances with the lowest price. 

### EC2 hands on 
+ spot request. 
+ elastic ip is one you own until u delete it. can mask failure of software. you can only have 5 elastic IP in your account - poor architectural IP. IP and register a DNS name to it. Use a load balance and dont use a public IP at all .

### Placement Groups
+ placement strategy ? - Cluster (low latency group in a  single AZ), Spread (spread across hardware, max 7 per AZ, crit applications). Partition - spread across many different set of racks within an AZ, scales to 100s of EC2 insstances per group. Cluster - great network but if AZ fails ur fucked.
+ Cluster Use: Big data job needed fast, low latency and high network throughput, 
+ Spread use; all instances on different hardware. Can span across AZ zones. Reduced Risk. 
+ Partition Group - 7 parities per az, each partition has multiple instances. not sure hwy its differnet. each parition is a rack - so you can have your own rack? , 100s of ec2 instances. ok so the instances in each parittion is its own hardware rack. "rack" is metaphorical i think, doesnt share ports maybe. Use case is big data applications.

### elastic network interfaces (ENI)
+ VPC? cirtual network card. provides ip and shit.
+ CENI: Primary Private IPv4, one or more secondary ips. 
+ One elastic IP per IPV4.
One or more security groups. One public IPV4, a mac address. You can create independently or move on the fly. Bound to a specific AZ. 
+ move ips between instances. - good for failover purposes.
+ So ENIs arent the actualy physical network cardsm, an abstraction on top of that that can be moved instance to instance. 

### EC2 Hibernate 
+ stop - data on disk is kept intact until next start. 
+ terminate - any ebs volume root also set upto be descryed is lost.
+ HIBERNATE: RAM state is pereserved, os is not stopped or restarted it is paused. RAM state -> EBS VOLUME ENCRYPTED. 
+ long running process, saving ram state, services that take time to initialzie. 
+ Good to know - support hella families, instance ram size < 150GB . not supported for baremetal. 
+ root volume must be EBS - on demand, reserved, spot. < 60 days. 
+ root volume must have enough storage / memor? 
+ 

## EC2 Instance Storage
+ EBS Volume - Elastic Block Store Voluem - network drive you can attach to your instances when they run. persist data after termination.  CCP - one ebs oen ec2 instance at a time. bound to a specific AZ zone. "NETWORK USB STICK" -> can attach to several instances
+ Network Drive. SOme latency. Detached from one to another. locked to a specific AZZ.  have a provisioned cpaacity , size in GBS and IOPS. EBS volumes can be unatached, attached on demand. 
+ Delete on termination attribute. Second to last column. Ticked for EBS behavior . by defualt the root EBS volume is delted. By default any other EBS volume is not deleted. preserve root volume when instance is terminated. 
+ EBS Snapshot - make a snapshot then can copy it across AZ or regions
+ EBS Snapshot Archive -> move to archive which is 75% cheaper. 72 hours to restore, not immediate. Recycle bin for snapshots helps. Retnetion 1 day to 12 year. FSR -> full intialization of snapshot to have no latency on the first use (expensive) 5:30AM
+ Copy snapshot to any region. 
+ Recreate volume from snapshot. EBS volume. 

### AMI 
+ Amazon MAchine IMage -> Customization of an EC2 INstance
+ prepacked AMI -> built for a specific region copied across them. Can launch EC2 instances from ami. can create your own ami, make and maintain yourself. aws marketplace ami
+ start -> stop -> build AMI (creates Ebs snapshots) -> launch . 

### EC2 Instance Store
+ Hard drive attached to physical storver. High performance hardware disk. if you terminate instances the storage is lost. EPHEMERAL storage. Not a long term place.
+ Good for cache, buffer, scratch data, etc. 
+ Risk of data loss if hardware fails. 

### EBS Volume Types
+ gp2 / gp3 (ssd) genereal purpose ssd -> medium
+ io1io2 SSD volume for low latency
st1 -> low cost, sc1 -> lowest cost.
+ Size throughput IOPS (I/O Ops Per Sec)
+ only gp2/io are boot volumes
+ Genereal Purpose: cost effective storage, 1-16tb, virtual desktops, gp3 - 3000 IOPS and throuput of 125, up to 16l and 1k. gp2 -> max is 16k, size of vcolume and iops are linked
+ gp3 through and iops are not linked
+ provisioned iops -> database workload (storage consisitency) io1 -> 64k iops for Nitro, 32k others. io2 -> 256k iops IOPS 1000:1.
+ EBS multiattach
+ st1/sc1 -> 16tb big data, log processing, IOPS 500, Cold HDD -> SC1, IOPS 250
+ multi attach - same volume to multiple EC2 instancces in the same AZ. ONLY FOR IO1 and IO2. Full read and write perms to high performance voluem. managaes concurrent write operations -> not too sure what this means -> only 16EC2 instances at a time **EXAM**
+ EBS Encryption : data at rest is encrypted, snapshots, volumes, data in flight. handled transparently. minimal impact on latency. KMS - AES-256**EXAM** 
+ copy funtion encrypts, create new, atatach. 
+ EFS - Elastic File System - Managed Network File System -> mounted on many EC2 in multi AZ. EXPENSIVE. Pay per use. POSIX, NFSv4.1, pay per gb. 
+ EFS Scale 1000s of concurrent NFS clients. Performance , Bursting, Provisioned. 
+ Storage Tiers move files after N days. Standard, EFS-IA -> Cost to retrieve cheap to store. Archive -> raely accessed 50% cheaper. IMplement lifecycle policies to move files between storage tiers. 
+ Bursting, Elastic, Provisioned. 
+ EFS vs EBS: EBS attached to one at a time, locked at AZ level. gp2: io increases if disks size does, gp3: increate io indepenetned. EBS moved with snapshot
+ EFS vs EBS: EFS mounting 100s of instances across AZ. Sharewebsite files (wordpress) only for linux. 


## High Availability and Scalability: ELB & ASG
+ Vertical , Horizontal (elasticity) 
+ Vert: increasing the size of the instance. Horizontal scaling is just adding one other operator, adding instances. 
+ Load Balanceing: Server that fowards traffice to downstream EC2 Instances
+ SIngle point of DNS 
+ handle failuter, SSL termination (HTTPS) high AZ, spearate traffic
+ AWS handles it
+ health checks - pinging and shit to amke sure it works properly. /health 
+ CLB - Classic Load Balancer old
+ Application Load Balancer ALB - HTTP HTTPS WebSocket
+ Network Load Balancer - TCP TLS
+ Gateway - Network level? 


### APplication Load 
+ Layer 7 HTTP
_ Multiple HTTP applications 
+ routing tables to different target groups. 
+ Target Groups: Instances, Tasks, Lambda, Private IP, 
+ Create a target group, use that as the listener on http port 80 for the laod balancer. 

### NEtworkl Load Balancer
+ Layer 4, TCP and UDP
+ millions of requests per second
+ ultra low latency - ONE STATIC IP PER AZ. Assign elastic IP per AZ. 
+ you can have an NLB -> ALB. NLB -> TG(IP) NLB -> TG(EC2 Instances)
+ HEALTH CHECKS SUpport the TCP, HTTP, HTTPS **EXAM** 
+ 

### Gateway Load Balancer
+ 3rd partyy network appliances in AWS
+ All go through iDS, firewall, etc. at the network level 
+ user -> GLB -> Target Group (check if all good) drop or send -> GLB -> Foward to applicaiton. to application it looks like nothing
+ operates at layer 3, network layer, IP packets. Transparent network gatesway -> single entry exit. load balancer as well. 
+ GENEVE PROTOCOL 6081 **EXAM**
+ EC, PRIV IP,


### misc
+ Sticky Session - client is always redirected to the same isntance . one client ends up at same instance always. quicker to get their data and shit. 
+ Cookie Names -Appication Based COokies - genereated by the targe. certain names you cant use. Duration Cookies - generated by load balancer, not target. 
+ Cross Zone Load Balanzcing - doesnt matter what az, alb distributes evenly no matter what. 
+ No charges for inter AZ data. enabled by default. 
NLB and GLB then we do pay for inter AZ. 
+ CLB - Ignore
+ SSL Certificates - in flight encryption - SSL Secure Sockets Layer
+ TLS newer version of SSL, SSL basically, CA - Certificate Authorities. ACM - AWS Certicate Manager
+ HTTPS listener - certs, SNI Server Name indication. 
+ **SNI** multiple ssl cedrts onto web server - indicate the hostname in the handshale. ONL Y WORKS WITH ALB AND NLB. Not CLB. 
+ ALB (2 CERTS) (2 TARGETS) -> Client -> ALB -> give me name and send right cert and shit to place
+ Connection Draining -> CLB . Deregistration Delay -> ALB NLB
+ Time to complete inflight requests 
+ Draining period to complete requests. ELB sends people to NONDRAINING EC2 Instances
+ 1-3600 seconds. default 5m
+ low value good for short
+ Autoscaling group -> load changes over time. free  - onyl pay for what it does for you
+ ELB -> ASG -> health check from ELB can use the help wahtever
+ launch template -> how to launch EC2 instancers ithin the ASG. 
+ can have any metric that causes an alarm 
+ Dynamic Scaling - avereage cpu %? 
+ Simple step scaling - add how many units
+ known usage pattern schedule scaling.
+ Predictive sacaling - forecast load and schedule based on that


## AWS Fundamentals RDS + Aurora + ElastiCache

### RDS
+ Relational Database Se4rrvice - SQL managed db service. managed by AWS. PostGres, Mysql, auraua, oracle, etc. *REMEMBER*
+ Managed service , os patching, continuous backups, you cannot ssh into your instances
+ RDS Storage Auto Scaling - rds will autoscale. avoid manually scalling. set a massive storage threshold. 
+ read replicas - scale reads. create read replicas across, within or cross region.async replication. eventually consistent. can be promoted to their own database and add writes at some point
+ create a reporting application
+ network cost; data cost from one AZ to another -> NO FEE IF IN THE SAME REGION BUT DIFFERENT AZ. CROSS REGION DOES COST A FEE. 
+ Multi AZ - disaster recovery. one dns name - automatic app failover to standby. 
+ zero downtime from singl to multi az. 
+ RDS Custom: Oracle, MS SQL Server - access to os and database customization.  - configure settings, patches, and the EC2 instances underneath the RDS. 
+ Amazon Aurora: compatibile with mysql and postgres. cloud optimized. 5x performance improvements. automatically grows in increments of 10GB -> 256TB. 15 read replicas. Faster. Failover is instantanerous. 20% more. but better. High Availability. 6 copies of your data across 3AZ. 4 for writes, 3 for reads. self healing. storage is striped across 100s of volumes. only one instance takes writre -> master up to 15 read replicas. one masters, multiple replicas. Cluster? Master only writes, writer endopint is DNS name pointing to the right instance incase failover. read replicas autoscaling. **READEWR ENDPOINT** Connection load balancing. connects to correct read replicas. ROutine maintenance, backtrack, patching, scaling, compliance, etc. 
+ Amazon Aurora Advannced: Autoscaling: can have a custom endpoint. many custom endpoints. Server less: automated database instantiation and autoscaling. good for infrequent unpredicatbale workloads. Global Aurora: 1 primary region for read write, 10 secondary are readonly, up to 16 read replicas per region. **TYPICAL COROSS REGION TAKES LESS THAN 1 SECOND** ML based predictions for you applications. SageMaker, Comprehend. predicts idea. predictions based on the aurora database sql. Baeblfish: understand commands for mssql server. BabelFish allows you to T-SQL -> babelsish. Aurora works with it now. AWS SCT and DMS to migrate. RDS Backups: automated abcksup -> daily full backup during window. 5 minute transaction logs are backed up. ub a stiooed RDS database will not pay for storage. **EXAM TRICK**: In a stopped RDS database, you will still pay for storage. If yhou plan on stoppiung for a long time, snapshot and restore instead.  Automated backsup 1-> 35 days. POint in time recovery anywahere in that frame. Aurora database cloning: create a new cluster from an exiign one. 
+ RDS & AURRORA. At-restencryption with KMS. read replicas cant be necrypted if master not. db -> restore to encrypt. Inflight encrypted by default. AWSTLS root certs. IAM Auth, IAM ROLES to connect. Security groups. NO SSH since its managed service. Audit logs sint to cloud watch logs for retention

#### RDS Proxy
+ allows apps to pool and share db connections established with teh database. improving efficieny. multiple AZ. reduces failover by 66%. no code changesm just change where you connect. NEVER publicly accessible. only over VPC. Lambda functions -> execute pieces of codes. multiply many times. pools together lamda functions for db instance to go easier. it is overloaded on purpose.
### Elasticache Overview
+ managed redis or memched - reduce load off of databases for read intensive worklodds - stateless. managed al os everything. heavy application code changes. 
+ Redis multi az AOF persistednce (what is that). supoprts sets and sorted sets. memchached - mul nodes for partitioned. not high avialability. non ersistent. backup and restore for servless only. replication vs sharding. 
+ IAM Auth for Redis. AWS API level security. 
+ REDIS auth password/token 
+ Memchae - SASL Based authentication. 
+ Lazy Loading - all read data iscached data can become stale
+ write through adds or updaate data in the cache when written to a db
+ session store temporary data in a cache 
+ REDIS: gaming leaderboards are computationally complex. redis sorted sets guarantee both uniqueness and element ordering. each tie an element is added its ranking in real time. 
+ Important ports:

    FTP: 21

    SSH: 22

    SFTP: 22 (same as SSH)

    HTTP: 80

    HTTPS: 443 

vs RDS Databases ports:

    PostgreSQL: 5432

    MySQL: 3306

    Oracle RDS: 1521

    MSSQL Server: 1433

    MariaDB: 3306 (same as MySQL)

    Aurora: 5432 (if PostgreSQL compatible) or 3306 (if MySQL compatible)

## Route 53
### DNS
+ Fomain Name System - human friendly hostnames into machine ip adress. .com -> example.com -> www.example.com -> ...
+ Registrar - GoDaddy, DNS Records, Zone FIle, Name Server, Top Level Domain, Second Level Domain, 
+ FQDN Fully qualified domain name
### Route 53 Overview
+ scalable managed ADNS
+ Authroitative -. customer can update the dns records. 
+ 53 = port
+ Records -> how route traffic to domain
+ Record: DOmain, type, value , routing policy, ttl (time cached), A / AAAA/ CNAME/ NS
+ A -> Maps hostname to IPv4; AAAA maps hostname to IPv6, CNAME -> Hostname to hostnamde.cname record for the top node of a dns namespace. NS -> Name server for the hosted zone
+ Hosted zone. Public, private. VPC is private. 
+ .50 cents per hosted zone. public hosted zone: private hosted zone. 
+ Handson: 
+ TTL -> high ttl is less traffic. ttl is to make sure it caches the result people dont request often . higher slower lower more monay
+ CNAME vs Alias - CNAME -> points a hostname to another hostname. ONLY FOR NON ROOT DOMAIN . Alias -> hostname to an aws resource. wroks for root domain and non root domain. free! native heatlh ceheck 
+ alisas maps hostname to aws. an extension to dns functionality. automatically recognzie changes in resource Ip address.A/AAAA. no set TTL. ELB, CloudFront, API , Elastic, S3 websites, Route 53 record. Cannot set an alias for a EC2 hostname. asias lets you use blog.tucknow.com. 
#### routing 
+ route traffic to a single resource, like client. ??
+ specify only one aws resource. cant be associated with health checks. 
+ weighted: control the % of requests that go to each specfic resource. 0 and 255. 
+ LAtency based- redirect to the lowest latency. closest region. can be associated with health checks. 
+ Health Checks - are only for public resources. route 53 make: dns records -> if one region down create health checks on both ALBs in regions. automated dns failover. integrated into CW
+ Health check. monitor an endpoint -> health cehcks from all around the world to check if it gets a 200 code. 15 global. threshold, interval, HTTP/S, TCP. > 18% healthy good to go. seems low. 
+ calculate health checks - combine a bunch into one health check large thing.encapsulation kinda. private hosted zone - CloudWatch Metric. alarm EC2 instance then create a health checker on the cloud watch alarm. ? why is the alarm not in the VPC? 
+ Failover. Primary with a health check, if unhealthy failover the second EC2 instances. route 53 automatically respons with right dns. 
+ Geolocation. default record if no match on location. health checks. how is this different than latency?
+ geoproximity. is this not the same? bias is a weighted value spand more traffic to resource, less trafifc to resource. AWS or non AWS resources. you can use route 53 to use. 
+ ip based reouting. based on client ip address. CIDRS? optimize perofmance or network costs. route end users from a specific isp to a specific endpoint. CIDR locations -> blocks. Records -> EC2 instances. 
+ MultiValue: return only values for healhty recourses. 8 health records. client side load balancing. return a bunch of records client picks one. 
