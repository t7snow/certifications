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
+ 1 Subtle keyword or phrase that points to the exact question - read like ur searching for all the details. one keyword is "there on purpose" 

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
corrective - fire extinfuisher 
directive - do something processes (authorized personnel only)


### cia triad

1. Confidentiality
+ prevent disclosure of info to unauthorized individuals
2. Integrity
+ messages cant be modified without detection
+ hashing
+ certs
+ non-repudiation - proof of integrity
3. Availability
+ keep shit up
+ 

### sep
1. non-repudiation
+ verify data does not change
+ hash
- fingerprint 
- doesnt associate data with an individual
+ proof of origin


### AAA

+ Auth 
- password or other auth facrotrs
+ Authorization
- based on identity and auth what do you have access to?
+ Accounting
- resources used: login time? 
+ triple A server (holds credentials)

+ CA 
- manages all the certs in the environment

### gap 

+ where you are vs where you want to be
+ baseline, NIST 800-171 PRotecting CUI in nonfed systems
+ ISO/IEC 27001
+ baseline of employees
+ compare existing systems
+ analysis report on access control, etc, gap aanalysis
+ need a path to get to where we want to be

### zero trust

+ authenticate everytime you want to get to another resource
+ nothing is trusted, everything is using some type of security check 
+ split network into *functional planes*
- data plane proceess frames packets and network data
- control plane: ploicies and ruels, determine how packets should be forwarded, routing tables
+ adapive identity: examine identity based on IP, type of connection, clicks, etc
+ threat scope reduction
+ *Policy Driven Access Control* : set of rules
+ Security zones: where you from where you going
- create each vpn for each zone
- untrusted -> trusted. trusted -> internal could be impolicit trust
+ **Policy Enforcement Point** : all traffic on network goes through this
- could be multiple devices
+ **Policy Decision Point**: PEP gives data to PDP and PDP makes decision. 
- Policy Engine
- Policy Administrator: gvenereates access tokens or creds, tells PEP to allow or disallow

### physical security

+ barricade / bollard
+ access control vestibules
+ fence
+ secufity cameras
+ id 
+ lighting 
+ infared 
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
a. fix doesnt fix anything, breaks something else, data corruption, etc. 
b. sandbox testing environment
3. technical change management:
a. allow list deny list.
b. downtime 
c. primary and secondary system
d. documentation goes out of date without doc process - include in change management rpocess

### pub key infrastructure

+ PKI: the CA binds keys
+ **symmetric key encryption** : a single shared key, encrypt with key, decrypt with key. if it get sout ur fucked. doesnt scale well
+ **asymmetric**: private - one device has. pub key is available to everytone
- you cant derive the private key from the public key


### encrypt data

+ only encrypt certain columns data
+ transport encryption
- encrypting in HTTPS, everything is encrypted
+ VPN - encrypted tunnel. client based VPN using SSL/TLS
+ both sides must use same encryption algorithm
+ longer the key the better

### key exchange

+ out of bound symmetric key
- dont use the network, some other method (suitcase) 
- telephone et
+ inband key exchange 
- additional encryption
- asymmewtric encryption to send a key over 

### encryptiuon tech

+ TPM
- cryptiographic processor
- unique keys during manufacturing
+ HSM
- Hardware security module 
- store all of the encryption keys 
- plugin card for cryptiographic functions
+ key mangement system


### obfuscation

+ hide shit within the imaage - covertext
+ embed messages in tcp packets
+ tokenization 

### hashing

+ integrity
+ can be a digital signiture - nonrepud, auth, integrity
+ sha256 - 256 bit hex characters
+ collision - MD5 had a collisison problem in 1996
+ verify document is the original - integrity
+ salt - random data added to a password when hashing. every user gets their own random salt ? 
+ rainbow tables - every possible hash associated with inputs
+ digitial signature - prove the message was not changed - integrity
+ prove source - auth
+ signature isnt fake - notn repudiation
+ sign with private jkey verify with pub

### blockchain

+ distributed ledger - everyone has a copy


### certs

+ public key and digitial signature
+ dig certificate - CA signs and trusts
+ Web of Trust - multiple individuals sign cert
+ X.509 standard format
+ serial num, version, sig algo, issuer, cert holder etc
+ root of trust - 3rd party trusts them we can too. HSM, enclave, CA, etc. 
+ **CA** 
- trust the CA therefore trust the website
- CSR -> CA 
- you can be your own CA - seems fun
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
- Recconnaissance
+ Open port for TCP/ UDP

### phisihing

+ typosquatting
+ pretexting, lying story shit
+ Smishing, Vishing

### watering hole attack

+ gain access to one website where everyone visits
+ Defense-In-Depth - multiple layers of security


### memory injections

+ DLLs - dynamic link libraries, thread,s buffers, malware run own process or inject into process. 

### buffer overflow

+ additional memory flows into another application. 
+ takes time to avoid fcrashing things or make it do what you want. hard
+ repeatable overflow


### race conditiion

+ TOCTOU - time o check to time of use account. in between these two do shit

### operating system vulnerabilities

+ patch tuesday 

### sql injection

+ structures query language
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
+ EOL -> this doesnt mean its done updating, but no longer selling the product
+ EOSL 

### virtualization vulnerabilties

+ local privelige escalation
+ commandinjection
+ information disclosure 
+ VM Escape -> getting to another vm on same hypervisor
+ Data can be inadvertently shared between VMs. RAM is shared


### cloud specific vulnerabilities

+ Denail of Service (DOS) DDoS 
+ Directory Traversal - bad
+ Remote code execution
+ Need to make sure all applications hav ebeen properly patched


### misconfiguration vulnerabilities

+ open permissions
+ unsecured admin accounts
+ unencrypted protocols: TELNET, FTP, SMTP, IMAP
+ Packetcapture to view if packet is encrypted or not. 
- SSh SFTP, is encrypted.
+ looks for devices with Mirai botenet
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
+ fileless ooperates in memory - never detected when it is not in exe format
+ adds autostart to get going again
+ worm runs without any user intervention 
+ worm replicates itself - worst 


### spyware

+ keylogger
+ bloatware - popular apps 
+ sponsored and games 


### other malware types

+ keylogger
+ logic bomb -> dormant until a specific event occurrs
+ rootkit -> hides within the kernel of the operating system, part of the OS

### physical attacks

+ environmental attack - turn off power type thing

### Denial of Service

+ force a service to fail 
++ overload service
+ competitive advantage - often  a smokescreen 
+ friendly DoS
+ NTP, DNS, IMCP, gives more information than we send -> each request sends back more characters. send these non stop to somoene


### DNS attack

+ dns posining - modify DNS server
+ modify host files send fake response to  a valid DNS request
+ MIM attack 
+ Domain Hijacking - take control of domain registration -> send users somewhere. 
+ typosquatting - brandjacking
+ typing error

### wireless attacks

+ 802.11 management frames
+ RF jamming 

### on-path attacks

+ sit inbetween two devices and read all data (MAN IN THE MIDDLE ATTACK)
+ redirects your traffic - invisible for victims
+ arp posining - on local subnet - arp no security
+ arp posoning - arp request asking for mac address, laptop caches mac address (dont want to arp reqeuest everytime), attacker 
+ on path browser attack 

### replay attack 

+ arp poining, malware, network tap, replay to server posing as the computer. 
+ not an MIM attack 
+ attacker captures the stuff by being in the middle - replay the username and hashed password acting as the client. 
+ header manipulation 


### malicious code 

### application attakck

+ code injection, buffer overflow
+ replay attack - replaying password hash or usser id - two different attacks used together 
+ Horizontal _ USER A -> USER B
+ Cross Site Requests -> loads texxt from server, video, instagram, etc.  
+ cross site request forgery - XSRF, CSRF (sea surf) 
+ browser makes requests on your behalf onto your facebook or someshit. 

### cryptographic attacks

+ birthday attack - two students sharing a birthday. has collision. brute force . hash value same for two different plaintexts. 
+ downgrade attack - use a weaker . ssl stripping - on path attack. strips away the S from http. attacker sends https after 
+ hash passowrds

### pasword attaacks

### indicators of comprimise

### hardening

+ EFS - Encrypting file system
+ FDE - Encrypt everything on the device
+ Encrypt all network - using a VPN  - https
+ EDR - Endpoint detection and response
+ detect threadts with machine learning , investigate the threat  - root cause analysis
+ repond to threat, isolate systen, roll back to older config, API driven
+ Host based firewall - allow or disallow
+ Host Based iNtrusion Prevention System HIPS - built into endpoint protection software
+ uses heuristics, behavioral, buffer overflow writing files to the window foler
+ NGFW - Next Gneeration Fire Wall 
+ change default configuration

### cloud infrastructure

+ IaaS, PaaS, SaaS
+ Matrix of responsibilites
+ IaC - configuration and defining servers network and applications
+ FaaS - Function as a Service  - accessing individual functions from an application
+ OS doesnt matter, justusing the functions- evenbt triggered and ephemeral
+ Microservice - APIs - API is the flue for the pmicroservices


### network infrastructure concepts

+ physical isolation - dont talk to eachother. 
+ VLAN - serpated logically canot communicate between a vlan without a layer 3 device
+ SDN - Software Defnied Networking - planes of operations
+ Data Plane, Control Plane, Management PLane
+ Split the functions int logoical unit

+ Data PLane - process network frames and packets, forwarding, trunking
+ Control Plane - routing tabels, session tables, NAT tables, dynamic routing protocol updates
+ Applicaiton Layer - ssh browser api , configuring the device, application tells control and data wat to do  DCA


### other infrastructure concepts

+ containerization - docker containerizes each application. contains everything u need except the os
+ SCADA - Supervisory Control and Data Acquisition System / ICS Industrial Control Systems
+ PC manages quiment
+ Distributed control systems
+ Segmented from the outside
+ RTOS - Real Time Operating System - brake will be the number one important thing
+ Nondetemrinistic operating system? 
+ HA = High Availibity

### infrastruicture considerations

+ availability - uptime
+ resilience - MTTR - mean time to repair
+ Cost - important
+ elasticity - scalablity 
+ computer - the compute engine - multiple thjings

### secure infrastructures

+ zones- firewall between different zones
+ secure network cabling
+ application level encryption 
+ 

### intrustion prevention

+ IPS - intrustion prevention system 
+ checking for vulnerabilites that are moving around the network
+ IDS - intrusion detection - jsut detects doesnt prevent
+ SPAN - switch port analyzer
+ copies traffic to IPS and place its going - just an IDS


### network applicents
+ jump server - jump server ssh to webserver - access secure network zones
+ proxy - sits in the middle in between and sends out to internet - a megaphone basically - checks shit caching content scanning etc
+ explicit or transparent proxy - uysers dont know about 
+ NAT - internal and external ip address translate
+ HTTP is a proxy?
+ internal proxy  - forward proxy -> users make requests to proxy in network then sends to user
+ reverse proxy is the other way around
+ load balance - large scal implementations 
+ fault tolderance - split the load among remaining servers
+ active/active load balance - configurable load - tcp offload - one single tcp connection between all servers - ssl offload. load balancer does the encryption and decryption - a proxy. caching  - Content Ssitching - QoS .
+ active/passing if an actrive server fails passive takes its place
+ port security - EAP - Extensible Autentication P{rotocol - many differntways to authentatice with RFC Stands

+ 802.1X - you dont get access to network without authentication 
+ RAIDUS, LDAP, TACASA+
+ Supplicant, authenticator, auth server - 

### network layers

1. Physical Layer - transmits raw bit stram over physical medium - cables
2. Data Link Lyaer - Defines the format of data on network = ethernet, wifi, mac addessses
3. NEtwork Layer- which physical path it will take = ip and routesrs
4. Transport Layer - using TCP / UDP trasmit data = tcp and udp
5. Session Layer  - maintains conncections and repsonsible for ports and sessions = NEtBIOS / RPC keeping u logged in
6. Presentation Layer - ensurs data is usable and data encryption  occurs = SSL / TLS JPEG/PNG
7. Application layer -  =Discord
### data types

+ Regulated - managed by third party
+ trade Secret 
+ Intellectual Property

### states of data

+ data at rest - should encrypt
+ data in transit - not much protection as it travels FIREWALL or IPS - Intrusion Prevention System
+ TLS _ Transport Layer Security
+ IPSec - internet protocol securituy
+ data in use is decryupted - target corp
+ GDPR -- General Data pRocection Regulation - any data about EU citizens must be stored in EU 


### protecting data

+ what subnet they are on in ip 
+ confusion encrypted different than plaintext
+ hasing - integrity

### resiliency 

+ High availibity - HA - always on always available
+ Server Clustering - multiple servers work as one big server - identicial operating systems
+ loads balancer adds or rmeoves devices
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
+ Table-TOp exerciese, go through all the steps with a group of peopleoer a table
+ talk through a disaster
+ Failover -bakcups
+ Simulated attacks

### backups

### power resiliency

+ line-interactive ups - brownouts
+ doubleconversion/online - always using ups
+ ramp up for generator - ups covers that itme

### security baselines

+ bascially the list of detailed security things
+ active directory, MDM (?)
+ automation is the key
+ most rarely change 


### hardening

+ hardening checkllists are from nauactuerrs
+ segment for company data and user data
+ MDM - Mobile Device Mnaager 
+ SCADA - Supervisory Control and Data Acquisiition System
+ ICS - 
+ RTOS - Deterministic - individual applications have to run ASAP 
+ isolate RTOS from network, minimum services running, secure communication
+ IoT devices - weak defaults
+ deploy updates quickly
+ degmentation
+

### securing wireless and mobile

+ COPE - Corporate owned persoanlly enabled
+ laptops and phones 
+ CYOD - Choose your own device
+ Seperate land into cells
+ PAN - Personal Area Network

### wireless security settings

+ MIC - Message Integrt Check
+ WPA2 - capture the hash during the handsheck - brute force gpu based processing
+ once u have the PSK
+ WPA3 - GCMP - block cipher mode 
+ GCMP - MIC, GMAC - Galois Message Auth Code
+ SAE - no more 4 way handsheck - Simultaneous Authenetiation of Equals - Diffie Hellman derived key exchange
+ IEEE Standards - dragon fly handshake
+ shared password/ PSK  - Pre Shared Key
+ Centralized Authenetiation (802.1x) 
+ sperate creds for everyone
+ WPA3 personal - PreSharedKey
+ WPA3 Enterprize - username and apswword
+ AAA Server
+ Identification - username
+ Autheneticaiton - password 
+ Authorization - what resources do you have access ot
+ Accounting - logging what you do 
+ RADIUS  - an AAA protocol - Remote Auth Dial-In User Service) 
+ username and password checked against a RADIUS Server
+ IEEE 802.1X - NAC - Network Access Control
+ Used in conjunction with RADIUS, LDAP, TACACS+ 
+ EAP - Exentsible AUthentication Protocol - an autheneticator, the atuthenetication server

### application security

+ QA - Quality Assurance 
+ SAST - Static Application Security Testing
+ Sandboxing 

### asset management

+ acquisition / procurement process
+ Assignment / Accounting - classificaiton ownership etc
+ degauss - electromagnetic deletion of shit


### vuln scanning

+ port scanning- what ar eopen and what are closed - what possible vulnerabilites
+ identify systems
+ lots of false positivess
+ SAST - Static application security testing
+ doesnt understand how shit is implmeented in the code jus tht eline 
+ fuzzing - dynamic analaysis - fault injecting, negative testing, syntax testing, appliction crash, exception
+ some applications are distributed as a package
+ confirm package is legit

### threat intelligence

+ stay up to date
+ OSINT - Open Source Intelligence
+ disucssion groups, social media, etc
+ Cyber Thraet Alliance - score submissions based oin threat, open source
+ dark web intelligence - intrnet for transport but need specialized software
+ pentesting - 

### pen testing

+ rules of engagment
+ type of testing, hours, etc. 
+ what is in and out of scope
+ try to break into the system - be cafeul can cause a ddos
+ laterla movement once ur in the network - try to create a persistent backdoor

### analyzing vulnerabilities

+ false negatives , positives
+ NVD - CVSS - 0-10 scoring differing scoring for 2.0, 3.0 etc
+ CVE - what CVE is associated with a given vulnerabilites cve.mitre.org
+ exposure factor - how risky it is having a vulnerability on a device. based on its aviliability


### vulnerability remidaition

+ patching 
+ cyber security insurance policy


### security monitoring

+ authentiation, server monitoring, etc
+ SIEM or SEM - Security Information and Event manager
+ consolidates all of the information, firwalls, cvpns, san, etc
+ centralized reporting
+ correlation between diverse systems
+ takes an average of 9 months to detect a breach
+ SOC - Security Operation Center

### security tools
+ NGFW - Next generation firewalls
+ IPS intrusion prevention system
+ SCAP Security content automation protocol
+ NIST National institude of standards and tech
+ SCAP is the language for security vulnerabilities
+ pass onto other people. patching can be automated
+ agentless runs without a formall install
+ check to see if device is in compliance, agent stays on agentless leaves after checking compliance
+ SIEM - Security information and event management - consolidate log types
+ log aggregation and data correlation
+ DLP - Data Loss Prevention - block out certain security and shit
+ data leakage is found
+ SNMP - simple network management protocol
+ MIB mangement information base
OID - object identifiers
+ udp/161 - poll devices
+ SNMP collect statiics
+ SNMP expect a poll, snmp traps can be configured on the monitored devices over *udp/162*
+ CRC? 
+ NetFlow - standard collection method. 
+ probe and collector. included in switch or router or in a seperate network probe. sometimes a tap on network sending itto a networkcollector
+ solarwinds
+ 


### firewalls

+ vpn between points
+ firewalls can be layer 3 device - NAT
+ NGFW - layer 7 firewall. ? 
+ application layer gateway - deeppacket inspection . 
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
+ - anomaly based - baseline of whats normal then scan
+ - list of vulnerabilites and decide if its allowed or disallowed
+ 

### content blocking

+ group urls
+ agent based - user decides it then agent manages control of content 
+ proxy makes request on behalf of user
+ - can url filter, cache, etc
+ - explicit proxies - need to know how to use it
+ - forward proxy , internal network
+ block based on specific url
+ DNS filtering - dns doesnt allow user to go that website


### operating system security

+ active directory
+ a database of everyhting on the network - on one central database - use username in the AD database
+ permissions inside the AD and groups are in there
+ group policy on certain computer / devices on manager
+ QoS - network configuration
+ Comprehensive control for the entier network 
+ SELinux - discretionary acccess control DAC 
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

+ FIM file integryity monitoring 
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
+ acces scontrol - limites access to acertain data
+ Posture assessment - what is or isnt up to date 
+ persistent agents can monitor files and shit on the system 
+ dissolvable agents  - no installic is required on startup 
+ agentless nac - integrated with active directy-  done on login and logodd
+ EDR - endpoint detection and response
+ EDR oios macihine learning and shit
+ root cause analysis is done by EDR
+ automated response
+ XDR is the smarter version of EDR
+ multiple agents - multiple devices - all correlated together
+ XDR multiple sources and correlateing data together. 


### identity
+ IAM - identity and acces smanagement
+ identitfyt licecycle management 
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
+ interoperability - use of shit with other shit


### access control

+ MAC - mandatort acess control 
+ - CUI shit
+ - administrator designs who has access to what
+ DAC - used in most operating systems. 
+ - who has access to what designed by the owner of the data
+ - weaker
+ RBAC - job function


### passwords

+ at least 8 characters 15 dats 
+ just in time - elevate rights at certain point 


### security incidents 

+ NISTSP800-61
+ network diagarms, hashes of files, mitigation software - os image


### incident planning

+ exercise 
+ tabletop exercise - everyone logistically stepping through the SOP, not actually doing it


### digital foresics

+ RFC 3227
+ extensive notes
+ legal hold: legal technique to preserve relevant informatrion - hold notificaitons
+ ESI - electronically stored information 
+ chain of custody - maintain integrity 
+ everyone who contacts evidence uses their digital signature to avoid tampering

### logs

+ dns sinkhole traffic, documentation of traggic logs
+ firewall logs - hodlds lots of data
+ - source/dest ip, port, disposition
+ - NGFW - applications that are in use, url categories, suspicious data
+ IPS IDS logs - ip, port, timestamp, mesg, class 
+ correlate with other network devices 
+ switches routers AP vpn hold routing updates, auth issues, or attacks

### security poliocies

+ Confidentiality, Integrity, Availability
+ AUP acceptable use policies - what is aceptable for everyone in the org


### agreemenets

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
+ Key Excrow - Storage and management of decrypted keys by a third party
+ Journaling - writes data to a temporary journal before writing the information to a database. if power is lost system acan recover the last transaction from the journal whne power is restored
+ Backout plan - how to go back after a fuckup


## acronym list

1. APT - Advanced Persistent Threat: Long term xyber attack where they stay inside
2. ARO - Annualized Rate of Occurrence: Estimated frequency that a risk will occur
3. ASLR - Address Space Layour Randomization: Protects against buffer overflows
4. AIS - Automated Indicator Sharing: exchanging threats in real time
5. ARP - Address Resolution Protocol: MAC addres and shit
6. AAA - Authentication, Authorization, Accounting: 
7. AH - Authenticaiton Header: provides integrity and authentication for IP packets. This does NOT provide confidentiality (no encryption). Includes sequence numbers to prevent replay attacks
8. ALE - Annualized Loss Expectency: Estimate total monetary loss from risk
9. AUP - Acceptable Use Policy
10. BCP - Business Continutity Plan
11. BGP - Border Gateway Protocol: BGP looks at path attributed to decide best route across teh entire internet. 
12. BIA - Business Impact Analysis
13. BPA - business partners agreement
14. BPDU - Bridge Protocol Data Unit: messes sent by swwitches within a networkthat uses spanning tree protocol. The heartbeat messages containing brighe ID and mac addreess. Vote on who will be centra point of tree
15. CAR - Corrective Actions Report
16. CASB - Cloud Access Security Broker: the policy enforce point for the cloud
17. DMARC - Domain Based Message Authentation Reporting and Conformance - specifies the dispositino of emails. 
18. SPF - Sender Policy Framework : list of all authorized mail servers for a specific domain. legit emails from one of the servers
19. NAC - Network access control: limit network access to only authorized users
20. DKIM - DOmain Keys Identified Mail : provides a way to validate all digitally signed messages from a server. 
21. MBTF - Mean Time Between Failers: how often a repairable system will fail
22. RTO - Recovery Time Objectives : Define aset of objectives needed to restore a particular service level
23. MTTR - Mean Time to Restore : amount of time to repair a componenet
24. RPO - Recovery Point Objective: Minimum data or operational state required to categorize a system as recovered
25. MOA - Memorandum of Agreement: formal document where both sides agree to broad set of goals and objectives 
26. SLA - Service Level Agreement : VERY SPECIFIC expectations between  both parties
27. PSK - Preshared key allows everyone on network to use same passwoerd when connection to network
28. CYOD - Choose Your Own Device 
29. COPE - Corporate Owned Personally Enabled
30. SASE -Secure Access Service Edge : next generation VPN designedf to optimize process of secure comms to cloud devicers
31. RTOS - Real Time operating Systems  : OS for industrial equipment
32. CRL - Certifcate Revocation list: cert has been revoked or not
33. SCAP - Securityu Content Automation protocl : focuses on the standarfdizzation of vulnerability management across multiple srcurity tools
34. DLP - Data Loss Preventuion
35. RADIUS - Remote Authetnciation Dial-In SUer service autonetation protocol for commonly used to validate user credentials. 
36. CSP - Cloud Service Provider
37. CSR - Certificate Signing Request - a user generates a public/private key pair. CSR is sent to the CA contianing the public key, CA verifies and signs
38. CSRF- Cross Site Request Forgery - while bank session is active browser sends malicious requesty
39. CSU - Channel Service Unit - CSu/DSU - hardware device that is the interface between LAN and WAN - LIKE T1 or R3. connects the digirtal line form telecom provider to the local network. ensures signal is properly formatted. protects local network from electric interference
40. CTM - Counter Mode - block cipher mode ethat turns a block ciper into a stream cipher. GCMP is standard for WPA3, CTM is underlying method. Nonce starting value counter increments every block. Key and counter are increpted together. then XOR it. AES is used with Couinter Mode. IV / Nonce
41. CVE - Common Vulnerability Enumeration: 
42. CVSS - Common vulnerability Scoring System : 0-10 scale NVD holds all thisinforamtion 
43. CYOD - Choose Your Own Device
44. DAC - Discretionary Access Control  : owner has discretion to do whatever he wants. data owner (local privilege escalation could be an issue.) SE Linux adds mandatory access conjtrol on top of DAC
45. DBA - Database Administrator
46. DEP - Data Execution Prevention. Bascially stops executing memory in placers that are designed for data storage only. Defense against buffer overflows and memory injections. Does this by memory marking, (non-execurable regions), blocking execution, targing vulnerabilites. Hardware and Sofrtawre versions
47. DES - Digital Encryption Standard - Symmetric Key algorithm, now considered insecure (same single shared key for encryption and decryption) block ciper 56 bit key, fiestel network. Brute force vulnerability. 3DES is now better, but slkower than AES
48. FN - fiestel network : split plaintext into halves and round, xor, swap, iterate
49. DHCP - Dynamic Host Configuraiton Protocol
50. DHE - Diffie Hellman steps: both parties aagree on a large prime number, each party creates own private key, perform matematical calculation using the public parameters and the private key, send result to tother person . By combining the received value with own private key both parties arrive at the same key
51. DKIM - Domain Keys Identified Mail : asymmetric key encryption to add digital signature to the header of an email. Outgoing mail server signsmessage with a privat ekey -> receiveing server looks up senders public key in dns records, integrity check
52. SPF -Sender policy framework : just a dns record of ip address authorzed to send for your domain
53. DMARC - Domain Based Message Authentication Reporting and Conformance - policy layer for scuity (disposition, what to do with shit)
54. DNAT - Destination Network ADdress Trnaslation : Changes the destination IP address of a packetas it passes through a router or firewall
55. DPO - Data Privacy Officer
56. DLP - Data Loss Prevention: has 3 points in use, motion, rest
57. DSA - Digital Signature Algothm - Asymmetric encryption  , ubtegruty, atygebtuiatuib, non-repudiation
58. DSL - Digital Subscriber Line: lets us use internet and telephone at the same time
59. EAP - Extensible Authentiation Protocl : device to negotionate authentiaction with a server regardless of what youre using. EAP-TLS (digital certs) EAP-TTLS(only server needs cert) PEAP (pencrypted tunnetl)
60. ECV - Electronic codebook - each block is encrypted independentally with the exact same key. Can lead to identical blocks of cipher text from identical blocks of plaintext
61. ECC - Elliptic Curve Cryptography : modern approach of older RSA methods. RSA uses large prime numbers, this is complex algebric structure of elliptic cures. smsalle key sized
62. EDR - Endpoint detection and response : basically just monitoring user devices
63. ESP - Encapsulated Security Payload : (AH Partnert) provides integirty, ESP provides encryption (confidentialiyy)
64. ABAC - Attribute based access control - user roles, time of daym network location
65. RuBAC - Rule Based Access Control (firewall)(
66. SMTP - Simpl eMail Transfer Protocol (it onlu piushes mail out, IMAP or POP3  actually pull the email in). 
67. SED - Self Encrypting Device - astorage ddevice that automatically encrypts every bit of data written without needing software
68. TPM -Trusted Platform Module - a chip on the motherboard used for boot integrity
69. IRP - Incident Response Plan
70. Business Response Plan - BRP



## ports

* Port 22: The default port for ssh secure alternative to Port 23. SFTP is also here, it is the secure version of FTP and works on an encrypted tunnel here. SCP is also here  
* Port 21: FTP COTNROL - used to transfer files from host to host with TCP. Control connection
* Port 20: FTP DATA - used for the actual transfer of files in active mode. in passive mode a random high number port is used instead. 
* Port 23: Telnet. Insecure. Telnet sends all data in unencrypted plaintesxt. 
* Port 25: SMTP - Simple Mail Transfer Protocol (SMTP) provides ability to send emails over the network
* Port 53: DNS - Uses both TCP and UDP on the same port. UDP 53 (queries) connectionless and easy to spoof. TCP 53 - ZOne Trasfers. When you are sneidng the entire data base to another DNS server. Large and needs to be accurate. **DNS POisoning** (Cache Poisining) an attacker sends fake dns information to a resolvers cache. If successful, anyone using the dns server is redirected. 
* Port 69: TFTP - Trivial File Transfer Protocol. UDP Based zero authentication, no encryption, only for simple get an dput operations
* Port 80: Entry point for HTTP - Unencrypted by default. Transmitted as plaintext, no integrity, redirect it to port 443 is the modern practice
* Port 88: Kerberos - TCP & UDP. Uses Key Distribution Center. AS: Authentication service you provide your username and it gives you a Ticket TGT. TGS you then trade your ticket for a service ticket whenever you need a certain resource. Backbone of SSO - u keep your ticket. Mutual authenetication. 
* Port 110: POP3 - Post Office Protocol Version 3. Legacy and should be replaced. Used by email clients to retrieve emails from a  amil server. Uses TCP. **Unencrypted** plaintext;. 995 holds POP3S the encrypted brother to this. 
* Port 119: NNTP - Netowkr News Transfer Protocol. Usenet news articles between news servers and clients. Predates social media and forums. IT uses TCP to ensure news articles are synced. **UNENCRYPTED**
* Port 135: Mircrosft RCP Endpoint Mapper - RPC endpoint mapper is a directory service for remote procedure calls. Connects to 135 to connect to specific server on a server. Handsoff to a dynamic portt. Uses **both TCP and UDDP**. **TCP IS MORE COMMON**. Provides **attackers with a map of your server**. Famous worms take over this. 
* Port 137: NetBIOS Name Service UDP
* Port 138: NetBIOS Datagram service UDP
* Port 139: NetBIOS Session Service TCP
* Port 143: IMAP (Internet Message Access Protocol) - access and manage emails directly on a mail server, imap keeps the messages on the server but synchronizes them across ytour devices. if you deleteon you iMac it deletes on your phoen too. TCP. 143 Is **UNENCRYPTED** by default. USERNAME AND PASSWORD ARE SENT IN PLAINTEXT. 993 is its secure brother
* Port 161: SNMP (Simple Network Managemetn Protocol): UDP Listens for requests from the manager. NMS (network Manager System) to query devicdes for status information and change configurations. 161 sees if its asking for anything. 
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
2b. Access Control VEstibule
2c. Access Badge
2d. Biometric - A:  Authentication token

3.
3a. Physical
3b. Managerial
3c. Operational
3d. Ohysical
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
24. (X) Deterrant scaes you away (login banner) directive is a formal document
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
39.A - Wrong. In Discretionary Access Control the owner controls the shit. **Administreatpr **  is in MAC (mandatory access contrl). **Group** is in role based access control. System is just useless
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
60 - Wrong. Jump Server is for maitenance or adminstrative shit. NEVER for cloud prod environments. SD-WAN ( ANSWER). Software Definied Networking in a Wide Area Network. it basically routes data smart;y./ MPLS is the expensive wifi connection. Gold connection . 

Microwave sensors can detect movement across a large area
ASymmetric encryption itself does not proof of origin

Operational controls are like trainings, process of getting approval. SOPs and risk asseessments or plalnning are considered managerial controls. 

902.1X requires authentication. It is a port based network access control 

PFS - perfect forward secrecy - uniquie session key derived for each connection 



#### RADIUS

UDP (Port 1812/1813)
encrypys only the password in the access request packet not the whole payload. auth and authorization in one process. used for vpns wifi etc

#### KERBEROS
Port 88
Uses symmetric encryption. 
