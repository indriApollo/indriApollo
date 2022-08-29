
# BIO

## Education

### CEPES Jodoigne
2012 - 2014  
IT Technician

### KU Leuven Faculty of Engineering Technology - De Nayer Campus
2014 - 2017  
Bachelor's degree Embedded-ICT

# Experience

## Ubidata (https://ubidata.com)
September 2017 - Present

### Embedded Software Developer

I helped my senior develop the firmware for our new in-house telematics device in C.
Some of my contributions :
- writing drivers for sensors and IC's (magnetometer, charge regulator)
- refactor our inter-processor communication (SPI, our design has both a high and low power ARM chip)
- debug and work around hardware issues in software (faulty comm bus)
- improve the efficiency of our custom TCP/IP protocol
- improve our u-blox GNSS driver

### System Administrator

I have maintained a homelab since I'm 18.  
When the previous developer responsible for our infrastructure signaled his intention to leave, I got asked to take over.  
We brought in an MSP to assist me.

I became responsible for :
- our office infra : 
  - on-site Active Directory
  - the embedded firmware Jenkins buildserver
  - a PBX VM
  - office networking
- our colocated datacenter infra :
  - a collection of Dell servers ranging from 5 to 12 years old
  - a mix of Windows Server 2003 / 2008 / 2016
  - a couple of Debian 8 machines
  - two MySQL databases
  - 7 Mbps copper pair

We undertook a modernization effort where we :
- virtualized physical hosts
- installed a new ESXi server cluster, consolidated hosts, migrated VM's and decommissioned outdated machines (we managed to halve the amount of machines in the rack)
- upgraded the network with new HA firewalls and redundant 100Mbps fiber
- improved storage and backups
- reconfigured the databases for improved performance and resiliency (we dropped the cpu load-average by 60% and reduced the maximum replication lag peaks from 2-3 hours to ~15 secs)
- updated Windows and Linux hosts / VM's to the latest versions
- improved monitoring
- migrated our PBX to cloud ip-telephony
- set up nginx proxies with automated Let's Encrypt renewals
- set up a postfix SMTP VM with OpenDKIM and proper SPF, DMARC config

I created a small lab that would host a test environment for developers using salvaged servers :
- a test database
- a couple of Ubuntu VM's for docker development
- I introduced and set up our self-hosted Gitlab instance (and migrated the remaining SVN repo's to Git)
- I created our first Gitlab-CI Runner

### Backend Software Developer

After a while, the embedded firmware matured and a two-person team became unnecessary.  
Given my experience with our TCP/IP protocol, I moved to the .NET backend team to work on incoming data processing.  

My first big project was to write a service to communicate with third-party telematics devices.  
As the sole developer on this project, I took the liberty to explore new technologies and methods.  
I chose a microservice approach with the idea of having multiple telematics front-ends that would translate communication from and to a common abstracted data processing pipeline.  
We successfully used this approach to quickly support additional telematics devices over the years.

- the services are written in .NET core
- inter-service communication happens with Protobuf messages over Redis queues
- the services expose performance metrics over Grpc. A small worker fetches these regularly and feeds them to our Grafana
- care is taken to leverage async IO to improve throughput
- the services are dockerized and managed with docker-compose 
- this solution has been handling 1000's of messages/minute mostly trouble-free on a small 2 cpu/4Gb ram Ubuntu VM ever since :)

### Lead Developer

Eventually, a technical leadership position opened up internally and I offered to become the lead developer.  
My main focus was to improve the quality of our massive legacy codebase :
- we first agreed on stronger coding conventions
- I mandated systematic code reviews
- I introduced more widespread usage of CI/CD
- we migrated or even completely rewrote services as old as .NET Framework 2.0 to .NET core
- we standardized our library usage (ex: Dapper, NUnit, NLog)
- I promoted Docker (the previous company standard was zipped release folders over FTP)
- we broke down big legacy monoliths into smaller services (while trying to avoid falling into the picoservices trap)
- I mentored developers in better SQL usage (Use The Index, Luke became our bible for a while :)
- I reviewed and validated new software architectures
- I evangelized new technologies inside the company

One big project I led during that time was the development of our new Track And Trace V2 web API.  
We decided to develop a new API in .NET Core instead of migrating the existing .NET Framework 4.5 one.  
Starting fresh allowed us to choose a better architecture and improve our public API design.  

- the backend uses ASP.NET core 6
- we use Swashbuckle for automatic Swagger documentation
- we try to keep the API consistent and intuitive
- we use caching extensively to improve responsiveness
- we monitor request response time to catch slow DB queries
- we developed a new geocoding Grpc service using an internal Nominatim database replica
- we developed a new PDF export Grpc service encapsulating Wkhtmltopdf
- we try to follow OWASP guidelines
