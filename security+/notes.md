# Security + Course / Notes

## plan

### videos
121 Videos
7.5m average
2x speed

30 videos per day 2x speed (2 hours?)


### techniques

+ examcompass.com - take every practice test
+ cybercraft - Security+ PBQ Playlist
+ Security Controls - on there a lot 
+ Active Recall
+ 1 subtle keyword or phrase that points to the exact question - read like you're searching for all the details. one keyword is "there on purpose"

## notes


2026.02.09
### control categories
1. technical controls
+ antivirus
2. managerial controls
+ standard operating procedures
3. operational controls
+ security guards
4. physical controls

each control category has a different example for each type

deterrent - warning signs etc (splash screen) 
detective control - alarm motion detector
corrective - fire extinguisher
directive - do something processes (authorized personnel only)


### cia triad

1. Confidentiality
+ prevent disclosure of info to unauthorized individuals
2. Integrity
+ messages can't be modified without detection
+ hashing
+ certs
+ non-repudiation - proof of integrity
3. Availability
+ keep systems up
+ 

### sep
1. non-repudiation
+ verify data does not change
+ hash
- fingerprint 
- doesn't associate data with an individual
+ proof of origin


### AAA

+ Auth 
- password or other auth factors
+ Authorization
- based on identity and auth what do you have access to?
+ Accounting
- resources used: login time? 
+ triple A server (holds credentials)

+ CA 
- manages all the certs in the environment

### gap 

+ where you are vs where you want to be
+ baseline, NIST 800-171 Protecting CUI in nonfed systems
+ ISO/IEC 27001
+ baseline of employees
+ compare existing systems
+ analysis report on access control, etc, gap analysis
+ need a path to get to where we want to be

### zero trust

+ authenticate every time you want to get to another resource
+ nothing is trusted, everything is using some type of security check 
+ split network into *functional planes*
- data plane processes frames, packets, and network data
- control plane: policies and rules, determine how packets should be forwarded, routing tables
+ adaptive identity: examine identity based on IP, type of connection, clicks, etc
+ threat scope reduction
+ *Policy Driven Access Control* : set of rules
+ Security zones: where you from where you going
- create each vpn for each zone
- untrusted -> trusted. trusted -> internal could be impolicit trust
+ **Policy Enforcement Point** : all traffic on network goes through this
- could be multiple devices
+ **Policy Decision Point**: PEP gives data to PDP and PDP makes decision. 
- Policy Engine
- Policy Administrator: generates access tokens or creds, tells PEP to allow or disallow

### physical security

+ barricade / bollard
+ access control vestibules
+ fence
+ security cameras
+ id 
+ lighting 
+ infrared
+ pressure, microwave, ultrasonic sensors

### deception and disruption

+ honeypot: attract and keep them in the system. 
- a virtual world: spend time in virtual world
- honeynets
- alert if someone access a file
- honeytoken, api credentials (if someone uses them)

### change management

1. formal change process form
a. scope, schedule, systems affected, analyze risk, stakeholders
2. impact analysis 
a. fix doesn't fix anything, breaks something else, data corruption, etc.
b. sandbox testing environment
3. technical change management:
a. allow list deny list.
b. downtime 
c. primary and secondary system
d. documentation goes out of date without doc process - include in change management rpocess

### pub key infrastructure

+ PKI: the CA binds keys
+ **symmetric key encryption** : a single shared key, encrypt with key, decrypt with key. if it gets out you're in trouble. doesn't scale well
+ **asymmetric**: private - one device has it. pub key is available to everyone
- you can't derive the private key from the public key


### encrypt data

+ only encrypt certain columns data
+ transport encryption
- encrypting in HTTPS, everything is encrypted
+ VPN - encrypted tunnel. client based VPN using SSL/TLS
+ both sides must use same encryption algorithm
+ longer the key the better

### key exchange

+ out of bound symmetric key
- don't use the network, some other method (suitcase)
- telephone et
+ inband key exchange 
- additional encryption
- asymmetric encryption to send a key over

### encryption tech

+ TPM
- cryptographic processor
- unique keys during manufacturing
+ HSM
- Hardware security module 
- store all of the encryption keys 
- plugin card for cryptographic functions
+ key management system


### obfuscation

+ hide data within the image - covertext
+ embed messages in tcp packets
+ tokenization 

### hashing

+ integrity
+ can be a digital signature - nonrepud, auth, integrity
+ sha256 - 256 bit hex characters
+ collision - MD5 had a collision problem in 1996
+ verify document is the original - integrity
+ salt - random data added to a password when hashing. every user gets their own random salt ? 
+ rainbow tables - every possible hash associated with inputs
+ digital signature - prove the message was not changed - integrity
+ prove source - auth
+ signature isn't fake - non-repudiation
+ sign with private key verify with pub

### blockchain

+ distributed ledger - everyone has a copy


### certs

+ public key and digital signature
+ dig certificate - CA signs and trusts
+ Web of Trust - multiple individuals sign cert
+ X.509 standard format
+ serial num, version, sig algo, issuer, cert holder etc
+ root of trust - 3rd party trusts them we can too. HSM, enclave, CA, etc. 
+ **CA** 
- trust the CA therefore trust the website
- CSR -> CA 
- you can be your own CA - seems useful for labs
-- openCA
+ *SAN* subject alt name - wildcard certificate . any device that has the domain name in SAN. lots of \*.x.live
+ CRL - list of all certs that have been revoked. 
+ April 2014 - heartbleed - openssl patched. make new certs
+ OCSP Stapling - status of certs on web server itself. OCSP status is stapled into SSL/TLS handshake. Signed by CA 
+ OCSP does most -> 3rd party server can do it. 


### threat actor

+ APT - Advanced persistent Threat


### threat vector

+ message based 
- email links, sms (short message service), 
+ SVG - Scalable vector graphic 
- image described in XML 
- html injection
+ war dialing - unpublished phone numbers?
+ Wireless
- WEP, WPA, WPA2 all outdated
+ Wired
- No 802.1X
+ Bluetooth 
- reconnaissance
+ Open port for TCP/ UDP

### phishing

+ typosquatting
+ pretexting, made-up story
+ Smishing, Vishing

### watering hole attack

+ gain access to one website where everyone visits
+ Defense-In-Depth - multiple layers of security


### memory injections

+ DLLs - dynamic link libraries, thread,s buffers, malware run own process or inject into process. 

### buffer overflow

+ additional memory flows into another application. 
+ takes time to avoid crashing things or make it do what you want. hard
+ repeatable overflow


### race condition

+ TOCTOU - time of check to time of use. in between those two, do something

### operating system vulnerabilities

+ patch tuesday 

### sql injection

+ structured query language
+ can control all data in database

### cross-site-scripting XSS

+ CSS - Cascading Style Sheets
+ Uses Javascript
+ at -> sends a link with malicious script to user -> user visits site
+ Non-Persistent -> web site allows script to run in user input
+ script embedded in url executes in browser
+ persistent now runs the javascript run in the browser

### hardware vulnerabilities

+ IoT  devices are vulnerable
+ EOL -> this doesn't mean it's done updating, but no longer selling the product
+ EOSL 

### virtualization vulnerabilities

+ local privilege escalation
+ command injection
+ information disclosure 
+ VM Escape -> getting to another vm on same hypervisor
+ Data can be inadvertently shared between VMs. RAM is shared


### cloud specific vulnerabilities

+ Denial of Service (DoS) DDoS
+ Directory Traversal - bad
+ Remote code execution
+ Need to make sure all applications have been properly patched


### misconfiguration vulnerabilities

+ open permissions
+ unsecured admin accounts
+ unencrypted protocols: TELNET, FTP, SMTP, IMAP
+ packet capture to view if packet is encrypted or not.
- SSH, SFTP is encrypted
+ looks for devices with Mirai botnet
+ Services will open ports 
- a little bit of access into a section of your server
+ firewall 

### mobile device vulnerabilities

+ Mobile Device Manager - MDM
+ Sideloading - installing applications off of software. Usually a jailbreak can do this


### Zero Day Vulnerabilities

+ Zero day attack 

### Overview of malware

+ viruses, worms, ransomware, trojan horse, rootkit, keylogger, spyware, logic bomb, etc.
+ ransomware - lock computer out
+ backup offline
- gap 


### viruses and worms

+ virus replicates itself
+ reproduces through file system or network - may not cause any issue until way spread out 
+ fileless operates in memory - never detected when it is not in exe format
+ adds autostart to get going again
+ worm runs without any user intervention 
+ worm replicates itself - worst 


### spyware

+ keylogger
+ bloatware - popular apps 
+ sponsored and games 


### other malware types

+ keylogger
+ logic bomb -> dormant until a specific event occurs
+ rootkit -> hides within the kernel of the operating system, part of the OS

### physical attacks

+ environmental attack - turn off power type thing

### Denial of Service

+ force a service to fail 
++ overload service
+ competitive advantage - often  a smokescreen 
+ friendly DoS
+ NTP, DNS, ICMP, gives more information than we send -> each request sends back more characters. send these nonstop to someone


### DNS attack

+ dns poisoning - modify DNS server
+ modify host files send fake response to  a valid DNS request
+ MIM attack 
+ Domain Hijacking - take control of domain registration -> send users somewhere. 
+ typosquatting - brandjacking
+ typing error

### wireless attacks

+ 802.11 management frames
+ RF jamming 

### on-path attacks

+ sit in between two devices and read all data (man-in-the-middle attack)
+ redirects your traffic - invisible for victims
+ arp poisoning - on local subnet - arp has no security
+ arp poisoning - arp request asking for mac address, laptop caches mac address (don't want to arp request every time), attacker
+ on path browser attack 

### replay attack 

+ arp poining, malware, network tap, replay to server posing as the computer. 
+ not an MIM attack 
+ attacker captures the stuff by being in the middle - replay the username and hashed password acting as the client. 
+ header manipulation 


### malicious code 

### application attack

+ code injection, buffer overflow
+ replay attack - replaying password hash or user id - two different attacks used together
+ Horizontal _ USER A -> USER B
+ Cross Site Requests -> loads text from server, video, instagram, etc.
+ cross site request forgery - XSRF, CSRF (sea surf) 
+ browser makes requests on your behalf onto your Facebook or something.

### cryptographic attacks

+ birthday attack - two students sharing a birthday. has collision. brute force . hash value same for two different plaintexts. 
+ downgrade attack - use a weaker . ssl stripping - on path attack. strips away the S from http. attacker sends https after 
+ hash passwords

### password attacks

### indicators of compromise

### hardening

+ EFS - Encrypting file system
+ FDE - Encrypt everything on the device
+ Encrypt all network - using a VPN  - https
+ EDR - Endpoint detection and response
+ detect threats with machine learning, investigate the threat - root cause analysis
+ respond to threat, isolate system, roll back to older config, API driven
+ Host based firewall - allow or disallow
+ Host Based iNtrusion Prevention System HIPS - built into endpoint protection software
+ uses heuristics, behavioral, buffer overflow, writing files to the Windows folder
+ NGFW - Next Generation Firewall
+ change default configuration

### cloud infrastructure

+ IaaS, PaaS, SaaS
+ Matrix of responsibilities
+ IaC - configuration and defining servers network and applications
+ FaaS - Function as a Service  - accessing individual functions from an application
+ OS doesn't matter, just using the functions - event triggered and ephemeral
+ Microservice - APIs - API is the glue for the microservices


### network infrastructure concepts

+ physical isolation - don't talk to each other
+ VLAN - separated logically, cannot communicate between a VLAN without a layer 3 device
+ SDN - Software Defined Networking - planes of operations
+ Data Plane, Control Plane, Management PLane
+ Split the functions into logical units

+ Data PLane - process network frames and packets, forwarding, trunking
+ Control Plane - routing tables, session tables, NAT tables, dynamic routing protocol updates
+ Application Layer - ssh browser api, configuring the device, application tells control and data what to do  DCA


### other infrastructure concepts

+ containerization - docker containerizes each application. contains everything you need except the os
+ SCADA - Supervisory Control and Data Acquisition System / ICS Industrial Control Systems
+ PC manages equipment
+ Distributed control systems
+ Segmented from the outside
+ RTOS - Real Time Operating System - brake will be the number one important thing
+ nondeterministic operating system?
+ HA = High Availability

### infrastructure considerations

+ availability - uptime
+ resilience - MTTR - mean time to repair
+ Cost - important
+ elasticity - scalability
+ compute - the compute engine - multiple things

### secure infrastructures

+ zones- firewall between different zones
+ secure network cabling
+ application level encryption 
+ 

### intrusion prevention

+ IPS - intrusion prevention system
+ checking for vulnerabilities that are moving around the network
+ IDS - intrusion detection - just detects, doesn't prevent
+ SPAN - switch port analyzer
+ copies traffic to IPS and place its going - just an IDS


### network appliances
+ jump server - jump server ssh to webserver - access secure network zones
+ proxy - sits in the middle and sends out to internet - a megaphone basically - checks content, caching, scanning, etc.
+ explicit or transparent proxy - users don't know about it
+ NAT - internal and external ip address translate
+ HTTP is a proxy?
+ internal proxy  - forward proxy -> users make requests to proxy in network then sends to user
+ reverse proxy is the other way around
+ load balance - large scale implementations
+ fault tolerance - split the load among remaining servers
+ active/active load balance - configurable load - tcp offload - one single tcp connection between all servers - ssl offload. load balancer does the encryption and decryption - a proxy. caching - content switching - QoS.
+ active/passive if an active server fails passive takes its place
+ port security - EAP - Extensible Authentication Protocol - many different ways to authenticate with RFC standards

+ 802.1X - you don't get access to network without authentication
+ RADIUS, LDAP, TACACS+
+ Supplicant, authenticator, auth server - 

### network layers

1. Physical Layer - transmits raw bit stream over physical medium - cables
2. Data Link Layer - Defines the format of data on network = ethernet, wifi, mac addresses
3. Network Layer - which physical path it will take = IP and routers
4. Transport Layer - using TCP / UDP to transmit data = tcp and udp
5. Session Layer - maintains connections and responsible for ports and sessions = NetBIOS / RPC keeping you logged in
6. Presentation Layer - ensures data is usable and data encryption occurs = SSL / TLS JPEG/PNG
7. Application layer -  =Discord
### data types

+ Regulated - managed by third party
+ trade Secret 
+ Intellectual Property

### states of data

+ data at rest - should encrypt
+ data in transit - not much protection as it travels FIREWALL or IPS - Intrusion Prevention System
+ TLS - Transport Layer Security
+ IPSec - internet protocol security
+ data in use is decrypted - target corp
+ GDPR -- General Data Protection Regulation - any data about EU citizens must be stored in the EU


### protecting data

+ what subnet they are on in ip 
+ confusion encrypted different than plaintext
+ hashing - integrity

### resiliency 

+ High availability - HA - always on, always available
+ Server Clustering - multiple servers work as one big server - identical operating systems
+ load balancer adds or removes devices
+ site resiliency 
+ hot site - exact replica of data center 
+ cold site, no hardware, empty building
+ warm site, some equipment on site
+ geographic dispersion 
+ platform diversity
+ multicloud system

### capacity planning

### recovery testing

+  test yourselves before an actual event
+ Tabletop exercise, go through all the steps with a group of people around a table
+ talk through a disaster
+ Failover - backups
+ Simulated attacks

### backups

### power resiliency

+ line-interactive ups - brownouts
+ doubleconversion/online - always using ups
+ ramp up for generator - ups covers that itme

### security baselines

+ basically the list of detailed security things
+ active directory, MDM (?)
+ automation is the key
+ most rarely change 


### hardening

+ hardening checklists are from manufacturers
+ segment for company data and user data
+ MDM - Mobile Device Manager
+ SCADA - Supervisory Control and Data Acquisition System
+ ICS - 
+ RTOS - Deterministic - individual applications have to run ASAP 
+ isolate RTOS from network, minimum services running, secure communication
+ IoT devices - weak defaults
+ deploy updates quickly
+ segmentation
+

### securing wireless and mobile

+ COPE - Corporate owned personally enabled
+ laptops and phones 
+ CYOD - Choose your own device
+ Separate land into cells
+ PAN - Personal Area Network

### wireless security settings

+ MIC - Message Integrity Check
+ WPA2 - capture the hash during the handshake - brute force gpu based processing
+ once you have the PSK
+ WPA3 - GCMP - block cipher mode 
+ GCMP - MIC, GMAC - Galois Message Auth Code
+ SAE - no more 4 way handshake - Simultaneous Authentication of Equals - Diffie Hellman derived key exchange
+ IEEE Standards - dragon fly handshake
+ shared password/ PSK  - Pre Shared Key
+ Centralized Authentication (802.1x)
+ separate creds for everyone
+ WPA3 personal - PreSharedKey
+ WPA3 Enterprise - username and password
+ AAA Server
+ Identification - username
+ Authentication - password
+ Authorization - what resources do you have access to
+ Accounting - logging what you do 
+ RADIUS  - an AAA protocol - Remote Auth Dial-In User Service) 
+ username and password checked against a RADIUS Server
+ IEEE 802.1X - NAC - Network Access Control
+ Used in conjunction with RADIUS, LDAP, TACACS+ 
+ EAP - Extensible Authentication Protocol - an authenticator, the authentication server

### application security

+ QA - Quality Assurance 
+ SAST - Static Application Security Testing
+ Sandboxing 

### asset management

+ acquisition / procurement process
+ Assignment / Accounting - classification ownership etc
+ degauss - electromagnetic deletion of data


### vuln scanning

+ port scanning - what are open and what are closed - what possible vulnerabilities
+ identify systems
+ lots of false positives
+ SAST - Static application security testing
+ doesn't understand how stuff is implemented in the code, just the line
+ fuzzing - dynamic analysis - fault injecting, negative testing, syntax testing, application crash, exception
+ some applications are distributed as a package
+ confirm package is legit

### threat intelligence

+ stay up to date
+ OSINT - Open Source Intelligence
+ discussion groups, social media, etc
+ Cyber Threat Alliance - score submissions based on threat, open source
+ dark web intelligence - internet for transport but need specialized software
+ pentesting - 

### pen testing

+ rules of engagement
+ type of testing, hours, etc. 
+ what is in and out of scope
+ try to break into the system - be careful, can cause a DDoS
+ lateral movement once you're in the network - try to create a persistent backdoor

### analyzing vulnerabilities

+ false negatives , positives
+ NVD - CVSS - 0-10 scoring differing scoring for 2.0, 3.0 etc
+ CVE - what CVE is associated with a given vulnerability cve.mitre.org
+ exposure factor - how risky it is having a vulnerability on a device, based on its availability


### vulnerability remediation

+ patching 
+ cyber security insurance policy


### security monitoring

+ authentication, server monitoring, etc
+ SIEM or SEM - Security Information and Event Manager
+ consolidates all of the information, firewalls, vpns, san, etc
+ centralized reporting
+ correlation between diverse systems
+ takes an average of 9 months to detect a breach
+ SOC - Security Operation Center

### security tools
+ NGFW - Next generation firewalls
+ IPS intrusion prevention system
+ SCAP Security content automation protocol
+ NIST National Institute of Standards and Technology
+ SCAP is the language for security vulnerabilities
+ pass onto other people. patching can be automated
+ agentless runs without a formall install
+ check to see if device is in compliance, agent stays on agentless leaves after checking compliance
+ SIEM - Security information and event management - consolidate log types
+ log aggregation and data correlation
+ DLP - Data Loss Prevention - block out certain sensitive data
+ data leakage is found
+ SNMP - simple network management protocol
+ MIB management information base
OID - object identifiers
+ udp/161 - poll devices
+ SNMP collect statistics
+ SNMP expect a poll, snmp traps can be configured on the monitored devices over *udp/162*
+ CRC? 
+ NetFlow - standard collection method. 
+ probe and collector. included in switch or router or in a separate network probe. sometimes a tap on network sending it to a network collector
+ solarwinds
+ 


### firewalls

+ vpn between points
+ firewalls can be layer 3 device - NAT
+ NGFW - layer 7 firewall. ? 
+ application layer gateway - deep packet inspection
+ every packet must be analyzed or categorized
+ traditional firewalls only knew what ports were being used
+ web server - 80/443
+ ssh - 22
+ dns - 53
+ ntp - 123
+ logical path top to bottom
+ implicit deny 
+ access control list (ACL) 
+ remote ip, port, local port, protocol
+ icmp - ping
+ IPS - intrusion prevention system - part of a NGFW
+ - signature ?
+ - anomaly based - baseline of what's normal then scan
+ - list of vulnerabilities and decide if it's allowed or disallowed
+ 

### content blocking

+ group urls
+ agent based - user decides it then agent manages control of content 
+ proxy makes request on behalf of user
+ - can url filter, cache, etc
+ - explicit proxies - need to know how to use it
+ - forward proxy , internal network
+ block based on specific url
+ DNS filtering - dns doesn't allow user to go to that website


### operating system security

+ active directory
+ a database of everything on the network - one central database - use username in the AD database
+ permissions inside the AD and groups are in there
+ group policy on certain computers / devices on domain
+ QoS - network configuration
+ Comprehensive control for the entire network
+ SELinux - discretionary access control DAC
+ limit application access 

### secure protocol

+ unencrypted network data
+ telnet -> ssh 
+ imap -> imaps
+ ftp -> sftp
+ port 80 http
+ port 443 https
+ packet capture to make sure all good


### email security

+ mail gateway - gatekeeper of all mail. scrubs them before going into your inbox. - in a screened subnet
+ SPF - sender policy framework - which email servers are allowed to send. DNS txt record. check your dns server to see who is allowed to send email
+ DKIM - domain keys identified mail - added between servers transport process. not to my message? 
+ DMARC - extension of SPF and DKIM written into a dns txt record
+ research this more ****

### monitoring data

+ FIM file integrity monitoring
+ SFC - system file checker 
+ tripwire is the linux version 
+ host based IPS
+ DLP - data loss prevention - block sensitive data across the network - data leakage - realtime
+ software or network
+ DLP = data in use
+ on your network = data in motion
+ on server = data at rest
+ email is the most common DLP 


### endpoint security

+ edge vs access control. 
+ edge is done by firewall 
+ access control - limits access to certain data
+ Posture assessment - what is or isn't up to date
+ persistent agents can monitor files and activity on the system
+ dissolvable agents - no install is required on startup
+ agentless nac - integrated with active directory - done on login and logoff
+ EDR - endpoint detection and response
+ EDR uses machine learning and similar tooling
+ root cause analysis is done by EDR
+ automated response
+ XDR is the smarter version of EDR
+ multiple agents - multiple devices - all correlated together
+ XDR multiple sources and correlateing data together. 


### identity
+ IAM - identity and access management
+ identity lifecycle management
+ access control 
+ log everything they do - fulll lifecycle
+ identity proofing
+ AAA server 
+ SSO - single sign on 
+ LIMITED by time
+ LDAP - lightweight directory address protocol - X.500 - DAP directory access protocol 
+ X.500 - attribute=values
+ Tree of information 
+ leaf objects
+ SAML - security assertion markup language
+ SAML wasnt designed for mobile devices
+ saml use how do serviers comm 
+ interoperability - use of one system with another


### access control

+ MAC - mandatory access control
+ - CUI data
+ - administrator designs who has access to what
+ DAC - used in most operating systems. 
+ - who has access to what designed by the owner of the data
+ - weaker
+ RBAC - job function


### passwords

+ at least 8 characters, 15 days
+ just in time - elevate rights at certain point 


### security incidents 

+ NISTSP800-61
+ network diagarms, hashes of files, mitigation software - os image


### incident planning

+ exercise 
+ tabletop exercise - everyone logistically stepping through the SOP, not actually doing it


### digital forensics

+ RFC 3227
+ extensive notes
+ legal hold: legal technique to preserve relevant information - hold notifications
+ ESI - electronically stored information 
+ chain of custody - maintain integrity 
+ everyone who contacts evidence uses their digital signature to avoid tampering

### logs

+ dns sinkhole traffic, documentation of traffic logs
+ firewall logs - holds lots of data
+ - source/dest ip, port, disposition
+ - NGFW - applications that are in use, url categories, suspicious data
+ IPS IDS logs - ip, port, timestamp, mesg, class 
+ correlate with other network devices 
+ switches routers AP vpn hold routing updates, auth issues, or attacks

### security policies

+ Confidentiality, Integrity, Availability
+ AUP acceptable use policies - what is acceptable for everyone in the org


### agreements

+ SLA - service level agreement
+ MOU - memorandum of understanding
+ MOA - a step above MOU
+ MSA - master service agreement
+ WO / SOW - 
+ BPA - business partner agreements
+ 


### exam review

+ Record Encryption: encrypt individual columns within the data base - some as plaintext some as encrypted text
+ Asymmetric - public and private key pair to encrypt data
+ Key Escrow - storage and management of decrypted keys by a third party
+ Journaling - writes data to a temporary journal before writing the information to a database. if power is lost system can recover the last transaction from the journal when power is restored
+ Backout plan - how to go back after a mistake


## acronym list

1. APT - Advanced Persistent Threat: long term cyber attack where they stay inside
2. ARO - Annualized Rate of Occurrence: Estimated frequency that a risk will occur
3. ASLR - Address Space Layout Randomization: protects against buffer overflows
4. AIS - Automated Indicator Sharing: exchanging threats in real time
5. ARP - Address Resolution Protocol: MAC address and related traffic
6. AAA - Authentication, Authorization, Accounting: 
7. AH - Authentication Header: provides integrity and authentication for IP packets. This does NOT provide confidentiality (no encryption). Includes sequence numbers to prevent replay attacks
8. ALE - Annualized Loss Expectancy: Estimate total monetary loss from risk
9. AUP - Acceptable Use Policy
10. BCP - Business Continuity Plan
11. BGP - Border Gateway Protocol: BGP looks at path attributes to decide best route across the entire internet.
12. BIA - Business Impact Analysis
13. BPA - business partners agreement
14. BPDU - Bridge Protocol Data Unit: messages sent by switches within a network that uses spanning tree protocol. The heartbeat messages contain bridge ID and mac address. Vote on who will be central point of tree
15. CAR - Corrective Actions Report
16. CASB - Cloud Access Security Broker: the policy enforce point for the cloud
17. DMARC - Domain Based Message Authentication Reporting and Conformance - specifies the disposition of emails.
18. SPF - Sender Policy Framework : list of all authorized mail servers for a specific domain. legit emails from one of the servers
19. NAC - Network access control: limit network access to only authorized users
20. DKIM - Domain Keys Identified Mail: provides a way to validate all digitally signed messages from a server.
21. MTBF - Mean Time Between Failures: how often a repairable system will fail
22. RTO - Recovery Time Objective: define a set of objectives needed to restore a particular service level
23. MTTR - Mean Time to Restore: amount of time to repair a component
24. RPO - Recovery Point Objective: Minimum data or operational state required to categorize a system as recovered
25. MOA - Memorandum of Agreement: formal document where both sides agree to broad set of goals and objectives 
26. SLA - Service Level Agreement : VERY SPECIFIC expectations between  both parties
27. PSK - Pre-shared key allows everyone on network to use same password when connecting to network
28. CYOD - Choose Your Own Device 
29. COPE - Corporate Owned Personally Enabled
30. SASE - Secure Access Service Edge: next generation VPN designed to optimize process of secure comms to cloud devices
31. RTOS - Real Time operating Systems  : OS for industrial equipment
32. CRL - Certificate Revocation List: whether a cert has been revoked or not
33. SCAP - Security Content Automation Protocol: focuses on the standardization of vulnerability management across multiple security tools
34. DLP - Data Loss Prevention
35. RADIUS - Remote Authentication Dial-In User Service: authentication protocol commonly used to validate user credentials
36. CSP - Cloud Service Provider
37. CSR - Certificate Signing Request - a user generates a public/private key pair. CSR is sent to the CA containing the public key, CA verifies and signs
38. CSRF - Cross Site Request Forgery - while bank session is active browser sends malicious request
39. CSU - Channel Service Unit - CSU/DSU - hardware device that is the interface between LAN and WAN - like T1 or T3. connects the digital line from telecom provider to the local network. ensures signal is properly formatted. protects local network from electric interference
40. CTR - Counter Mode - block cipher mode that turns a block cipher into a stream cipher. GCMP is standard for WPA3, CTR is underlying method. nonce starting value counter increments every block. key and counter are encrypted together, then XOR it. AES is used with Counter Mode. IV / nonce
41. CVE - Common Vulnerability Enumeration: 
42. CVSS - Common Vulnerability Scoring System: 0-10 scale, NVD holds all this information
43. CYOD - Choose Your Own Device
44. DAC - Discretionary Access Control: owner has discretion to do whatever they want. data owner controls access (local privilege escalation could be an issue). SE Linux adds mandatory access control on top of DAC
45. DBA - Database Administrator
46. DEP - Data Execution Prevention. Basically stops executing memory in places that are designed for data storage only. Defense against buffer overflows and memory injections. Does this by memory marking, non-executable regions, blocking execution, targeting vulnerabilities. Hardware and software versions
47. DES - Data Encryption Standard - symmetric key algorithm, now considered insecure (same single shared key for encryption and decryption) block cipher 56 bit key, Feistel network. Brute force vulnerability. 3DES is better, but slower than AES
48. FN - Feistel network: split plaintext into halves and round, xor, swap, iterate
49. DHCP - Dynamic Host Configuration Protocol
50. DHE - Diffie Hellman steps: both parties agree on a large prime number, each party creates own private key, perform mathematical calculation using the public parameters and the private key, send result to other person. By combining the received value with own private key both parties arrive at the same key
51. DKIM - Domain Keys Identified Mail: asymmetric key encryption to add digital signature to the header of an email. outgoing mail server signs message with a private key -> receiving server looks up sender's public key in dns records, integrity check
52. SPF - Sender Policy Framework: just a dns record of IP address authorized to send for your domain
53. DMARC - Domain Based Message Authentication Reporting and Conformance - policy layer for security (disposition, what to do with messages)
54. DNAT - Destination Network Address Translation: changes the destination IP address of a packet as it passes through a router or firewall
55. DPO - Data Privacy Officer
56. DLP - Data Loss Prevention: has 3 points in use, motion, rest
57. DSA - Digital Signature Algorithm - asymmetric encryption, integrity, authentication, non-repudiation
58. DSL - Digital Subscriber Line: lets us use internet and telephone at the same time
59. EAP - Extensible Authentication Protocol: way to negotiate authentication with a server regardless of what you're using. EAP-TLS (digital certs) EAP-TTLS (only server needs cert) PEAP (encrypted tunnel)
60. ECB - Electronic Codebook - each block is encrypted independently with the exact same key. can lead to identical blocks of ciphertext from identical blocks of plaintext
61. ECC - Elliptic Curve Cryptography: modern approach compared to older RSA methods. RSA uses large prime numbers, this uses complex algebraic structure of elliptic curves. smaller key sizes
62. EDR - Endpoint detection and response : basically just monitoring user devices
63. ESP - Encapsulated Security Payload: AH partner, provides encryption and confidentiality
64. ABAC - Attribute based access control - user roles, time of day, network location
65. RuBAC - Rule Based Access Control (firewall)(
66. SMTP - Simple Mail Transfer Protocol (it only pushes mail out, IMAP or POP3 actually pull the email in).
67. SED - Self Encrypting Device - a storage device that automatically encrypts every bit of data written without needing software
68. TPM - Trusted Platform Module - a chip on the motherboard used for boot integrity
69. IRP - Incident Response Plan
70. Business Response Plan - BRP



## ports

* Port 22: The default port for SSH, secure alternative to Port 23. SFTP is also here, it is the secure version of FTP and works over an encrypted tunnel. SCP is also here
* Port 21: FTP CONTROL - used to transfer files from host to host with TCP. control connection
* Port 20: FTP DATA - used for the actual transfer of files in active mode. in passive mode a random high number port is used instead.
* Port 23: Telnet. Insecure. Telnet sends all data in unencrypted plaintext.
* Port 25: SMTP - Simple Mail Transfer Protocol (SMTP) provides ability to send emails over the network
* Port 53: DNS - uses both TCP and UDP on the same port. UDP 53 (queries) connectionless and easy to spoof. TCP 53 - zone transfers. when you are sending the entire database to another DNS server. large and needs to be accurate. **DNS Poisoning** (Cache Poisoning) an attacker sends fake dns information to a resolver's cache. if successful, anyone using the dns server is redirected.
* Port 69: TFTP - Trivial File Transfer Protocol. UDP based, zero authentication, no encryption, only for simple get and put operations
* Port 80: Entry point for HTTP - Unencrypted by default. Transmitted as plaintext, no integrity, redirect it to port 443 is the modern practice
* Port 88: Kerberos - TCP & UDP. uses Key Distribution Center. AS: Authentication service, you provide your username and it gives you a ticket TGT. TGS: you then trade your ticket for a service ticket whenever you need a certain resource. backbone of SSO - you keep your ticket. mutual authentication.
* Port 110: POP3 - Post Office Protocol Version 3. legacy and should be replaced. used by email clients to retrieve emails from a mail server. uses TCP. **Unencrypted** plaintext. 995 holds POP3S, the encrypted version of this.
* Port 119: NNTP - Network News Transfer Protocol. Usenet news articles between news servers and clients. predates social media and forums. it uses TCP to ensure news articles are synced. **UNENCRYPTED**
* Port 135: Microsoft RPC Endpoint Mapper - RPC endpoint mapper is a directory service for remote procedure calls. connects to 135 to connect to a specific service on a server. hands off to a dynamic port. uses **both TCP and UDP**. **TCP IS MORE COMMON**. provides **attackers with a map of your server**. famous worms target this.
* Port 137: NetBIOS Name Service UDP
* Port 138: NetBIOS Datagram service UDP
* Port 139: NetBIOS Session Service TCP
* Port 143: IMAP (Internet Message Access Protocol) - access and manage emails directly on a mail server, IMAP keeps the messages on the server but synchronizes them across your devices. if you delete on your iMac it deletes on your phone too. TCP. 143 is **UNENCRYPTED** by default. USERNAME AND PASSWORD ARE SENT IN PLAINTEXT. 993 is its secure counterpart
* Port 161: SNMP (Simple Network Management Protocol): UDP listens for requests from the manager. NMS (network management system) queries devices for status information and configuration changes. 161 sees if it's asking for anything.
* Port 162: SNMP UDP SNMP Traps

## Professor Messor Practice Exams:

### PRactice Exam A

1. 
1a. Vishing
1b. Injection
1c. Onpath
1d. DDoS
1e. Keylogger

2. 
2a. Security Guard
2b. Access Control Vestibule
2c. Access Badge
2d. Biometric - A:  Authentication token

3.
3a. Physical
3b. Managerial
3c. Operational
3d. Physical
3e. Technical

4. 
4a. Something you have
4b. Something you know
4c. Something you are?
4d. Somewher you are

5.

6. Passive Reconnaissance
7. DMARC (X)
8. Organized Crime
9. Root-Cause analysis
10. System Availability
11. Automation?
12. A
13. Regulated
14. G, A, E 
15. B
16. D
17. D
18. B (X)
19. A
20. SLA /A (X)
21. C
22. C
23. B, D
24. (X) Deterrent scares you away (login banner) directive is a formal document
25. C
26. B
27. A (X)
28. (X)
29. (X)
30. D
31. (X) 
32. (X)
33. B
40.(X) i



### practice exam 2

## practice exam 3



D
B
D
C
D
A
B
D
D
B
D
D
A
C
A
B - Wrong Orchestration is real
C
24.A
C
A
C
B
C
B
A
32.A Wrong
D
D
D
C
37.B - Wrong. Playbook is an actual thing just a playbook, easy enough
B
39.A - Wrong. In Discretionary Access Control the owner controls access. **Administrator** is in MAC (mandatory access control). **Group** is in role based access control. System is just not the answer
B 
A - An MOU is an informal letter of intent (not a signed contract)
B
D
A - Wrong OCSP Stapling (Online Certificate Status Protocol) stapling allows certificate holder to verify their own certificate status. OCSP status is "stapled" onto the SSL/TLS handshake process. CRL is held by the CA
B
D
B
C
B
C
A
A
53B - WRONG LDAP is a (Lightweight Directory Access Protocol)( common standard for authentication. SIEM is a service that consolidates log files from different systems and can create reports based on this. Not part of the auth process
60 - Wrong. Jump Server is for maintenance or administrative access. NEVER for cloud prod environments. SD-WAN (ANSWER). Software Defined Networking in a Wide Area Network. it basically routes data smartly. MPLS is the expensive premium connection.

Microwave sensors can detect movement across a large area
Asymmetric encryption itself does not provide proof of origin

Operational controls are like trainings, process of getting approval. SOPs and risk assessments or planning are considered managerial controls.

802.1X requires authentication. It is a port based network access control

PFS - perfect forward secrecy - unique session key derived for each connection



#### RADIUS

UDP (Port 1812/1813)
encrypts only the password in the access request packet, not the whole payload. auth and authorization in one process. used for vpns, wifi, etc

#### KERBEROS
Port 88
Uses symmetric encryption. 
