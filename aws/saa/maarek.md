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
+ 


