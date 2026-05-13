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
+ 
