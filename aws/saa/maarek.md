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
