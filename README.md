[comment]: # "Auto-generated SOAR connector documentation"
# DomainTools

Publisher: Phantom  
Connector Version: 1\.0\.47  
Product Vendor: DomainTools  
Product Name: DomainTools  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 3\.5\.210  

Use DomainTools to query various current and historical data regarding domain names, domain registration and IPs

[comment]: # " File: readme.md"
[comment]: # "  Copyright (c) 2016-2018 Splunk Inc."
[comment]: # ""
[comment]: # "  Licensed under Apache 2.0 (https://www.apache.org/licenses/LICENSE-2.0.txt)"
[comment]: # ""



### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a DomainTools asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**username** |  required  | string | User Name
**key** |  required  | password | API Key

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity  
[domain reputation](#action-domain-reputation) - Evaluates the risk of a given domain  
[recent domains](#action-recent-domains) - Search for new domains containing a word  
[reverse domain](#action-reverse-domain) - Find IPs that point to this domain and other domain names that share the same IP  
[reverse ip](#action-reverse-ip) - Find domain names that share an IP  
[reverse email](#action-reverse-email) - Find domains with an email in their Whois record  
[hosting history](#action-hosting-history) - Obtain changes to registrar, IP, etc  
[whois history](#action-whois-history) - Obtain historic whois records for a domain name  
[whois ip](#action-whois-ip) - Execute whois lookup on the given IP address  
[whois domain](#action-whois-domain) - Execute whois lookup on the given domain  

## action: 'test connectivity'
Validate the asset configuration for connectivity

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'domain reputation'
Evaluates the risk of a given domain

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**domain** |  required  | Domain to query | string |  `url`  `domain` 
**use\_risk\_api** |  optional  | Use Risk/Evidence API | boolean | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.domain | string |  `url`  `domain` 
action\_result\.parameter\.use\_risk\_api | boolean | 
action\_result\.data\.\*\.domain | string |  `domain` 
action\_result\.data\.\*\.risk\_score | numeric | 
action\_result\.summary\.risk\_score | numeric | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'recent domains'
Search for new domains containing a word

Type: **investigate**  
Read only: **True**

If the <b>days\_back</b> parameter is not set, the data for the current day is returned, else data of the particular day in the past is retrieved\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**query** |  required  | Word to look for in a domain name | string | 
**days\_back** |  optional  | Number of days back to search for \(1\-6\) | string | 
**status** |  optional  | Status of the domain | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.days\_back | string | 
action\_result\.parameter\.query | string |  `email` 
action\_result\.parameter\.status | string | 
action\_result\.data\.\*\.alerts\.\*\.domain | string |  `domain` 
action\_result\.data\.\*\.alerts\.\*\.status | string | 
action\_result\.data\.\*\.date | string | 
action\_result\.data\.\*\.limit | numeric | 
action\_result\.data\.\*\.new | boolean | 
action\_result\.data\.\*\.on\-hold | boolean | 
action\_result\.data\.\*\.query | string |  `email` 
action\_result\.data\.\*\.total | numeric | 
action\_result\.data\.\*\.utf8 | boolean | 
action\_result\.summary | string | 
action\_result\.summary\.total\_domains | numeric |  `domain` 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'reverse domain'
Find IPs that point to this domain and other domain names that share the same IP

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**domain** |  required  | Domain to query | string |  `host name`  `domain` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.domain | string |  `host name`  `domain` 
action\_result\.data\.\*\.ip\_addresses\.\*\.domain\_count | numeric |  `domain` 
action\_result\.data\.\*\.ip\_addresses\.\*\.domain\_names | string |  `domain` 
action\_result\.data\.\*\.ip\_addresses\.\*\.ip\_address | string |  `ip`  `ipv6` 
action\_result\.summary | string | 
action\_result\.summary\.total\_ips | numeric | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'reverse ip'
Find domain names that share an IP

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**ip** |  required  | IP address to query | string |  `ip`  `ipv6` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.ip | string |  `ip`  `ipv6` 
action\_result\.data\.\*\.ip\_addresses\.domain\_count | numeric |  `domain` 
action\_result\.data\.\*\.ip\_addresses\.domain\_names | string |  `domain` 
action\_result\.data\.\*\.ip\_addresses\.ip\_address | string |  `ip`  `ipv6` 
action\_result\.summary | string | 
action\_result\.summary\.total\_domains | numeric |  `domain` 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'reverse email'
Find domains with an email in their Whois record

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**email** |  required  | email query | string |  `email` 
**include\_history** |  optional  | Include historical whois matches | boolean | 
**count\_only** |  optional  | Only return count of matched records | boolean | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.count\_only | boolean | 
action\_result\.parameter\.email | string |  `email` 
action\_result\.parameter\.include\_history | boolean | 
action\_result\.data\.\*\.domain\_count\.current | numeric | 
action\_result\.data\.\*\.domain\_count\.historic | numeric | 
action\_result\.data\.\*\.domains | string |  `domain` 
action\_result\.data\.\*\.report\_cost\.current | numeric | 
action\_result\.data\.\*\.report\_cost\.historic | numeric | 
action\_result\.data\.\*\.report\_price\.current | numeric | 
action\_result\.data\.\*\.report\_price\.historic | numeric | 
action\_result\.summary | string | 
action\_result\.summary\.total\_domains | numeric |  `domain` 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'hosting history'
Obtain changes to registrar, IP, etc

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**domain** |  required  | Domain to query | string |  `domain` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.domain | string |  `domain` 
action\_result\.data\.\*\.domain\_name | string |  `domain` 
action\_result\.data\.\*\.ip\_history\.\*\.action | string | 
action\_result\.data\.\*\.ip\_history\.\*\.action\_in\_words | string | 
action\_result\.data\.\*\.ip\_history\.\*\.actiondate | string | 
action\_result\.data\.\*\.ip\_history\.\*\.domain | string |  `domain` 
action\_result\.data\.\*\.ip\_history\.\*\.post\_ip | string |  `ip`  `ipv6` 
action\_result\.data\.\*\.ip\_history\.\*\.pre\_ip | string |  `ip`  `ipv6` 
action\_result\.data\.\*\.nameserver\_history\.\*\.action | string | 
action\_result\.data\.\*\.nameserver\_history\.\*\.action\_in\_words | string | 
action\_result\.data\.\*\.nameserver\_history\.\*\.actiondate | string | 
action\_result\.data\.\*\.nameserver\_history\.\*\.domain | string |  `domain` 
action\_result\.data\.\*\.nameserver\_history\.\*\.post\_mns | string | 
action\_result\.data\.\*\.nameserver\_history\.\*\.pre\_mns | string | 
action\_result\.data\.\*\.registrar\_history\.\*\.date\_created | string | 
action\_result\.data\.\*\.registrar\_history\.\*\.date\_expires | string | 
action\_result\.data\.\*\.registrar\_history\.\*\.date\_lastchecked | string | 
action\_result\.data\.\*\.registrar\_history\.\*\.date\_updated | string | 
action\_result\.data\.\*\.registrar\_history\.\*\.domain | string |  `domain` 
action\_result\.data\.\*\.registrar\_history\.\*\.registrar | string | 
action\_result\.data\.\*\.registrar\_history\.\*\.registrartag | string | 
action\_result\.summary | string | 
action\_result\.summary\.ip\_history\_count | numeric | 
action\_result\.summary\.nameserver\_history\_count | numeric | 
action\_result\.summary\.registrar\_history\_count | numeric | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'whois history'
Obtain historic whois records for a domain name

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**domain** |  required  | Domain to query | string |  `domain` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.domain | string |  `domain` 
action\_result\.data\.\*\.history\.\*\.date | string | 
action\_result\.data\.\*\.history\.\*\.is\_private | numeric | 
action\_result\.data\.\*\.history\.\*\.whois\.name\_servers | string | 
action\_result\.data\.\*\.history\.\*\.whois\.record | string | 
action\_result\.data\.\*\.history\.\*\.whois\.registrant | string | 
action\_result\.data\.\*\.history\.\*\.whois\.registration\.created | string | 
action\_result\.data\.\*\.history\.\*\.whois\.registration\.expires | string | 
action\_result\.data\.\*\.history\.\*\.whois\.registration\.registrar | string | 
action\_result\.data\.\*\.history\.\*\.whois\.registration\.statuses | string | 
action\_result\.data\.\*\.history\.\*\.whois\.registration\.updated | string | 
action\_result\.data\.\*\.history\.\*\.whois\.server | string | 
action\_result\.data\.\*\.record\_count | numeric | 
action\_result\.summary | string | 
action\_result\.summary\.record\_count | numeric | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'whois ip'
Execute whois lookup on the given IP address

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**ip** |  required  | IP to query | string |  `ip`  `ipv6` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.ip | string |  `ip`  `ipv6` 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.abuse\_mailbox | string |  `email` 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.address | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.address\.0 | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.address\.1 | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.address\.2 | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.address\.3 | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.contact\_keys\.abuse | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.contact\_keys\.admin | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.contact\_keys\.noc | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.contact\_keys\.tech | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.country | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.created\_date | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.email | string |  `email` 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.fax | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.id | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.mnt\_keys\.by | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.mnt\_keys\.ref | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.name | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.other\.auth | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.phone | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.ref | string |  `url` 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.remarks | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.source | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.type | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.\*\.updated\_date | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.asn | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.contact\_keys\.abuse | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.contact\_keys\.admin | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.contact\_keys\.noc | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.contact\_keys\.org | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.contact\_keys\.tech | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.country | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.created\_date | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.customer | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.descr | string |  `url` 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.id | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.mnt\_keys\.by | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.mnt\_keys\.irt | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.mnt\_keys\.routes | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.name | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.org | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.parent | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.parent\_id | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.range\.cidr | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.range\.count | numeric | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.range\.from | string |  `ip`  `ipv6` 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.range\.to | string |  `ip`  `ipv6` 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.ref | string |  `url` 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.remarks | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.source | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.status | string | 
action\_result\.data\.\*\.parsed\_whois\.networks\.\*\.updated\_date | string | 
action\_result\.data\.\*\.parsed\_whois\.routes\.\*\.asn | string | 
action\_result\.data\.\*\.parsed\_whois\.routes\.\*\.country | string | 
action\_result\.data\.\*\.parsed\_whois\.routes\.\*\.created\_date | string | 
action\_result\.data\.\*\.parsed\_whois\.routes\.\*\.descr | string | 
action\_result\.data\.\*\.parsed\_whois\.routes\.\*\.id | string | 
action\_result\.data\.\*\.parsed\_whois\.routes\.\*\.mnt\_keys\.by | string | 
action\_result\.data\.\*\.parsed\_whois\.routes\.\*\.mnt\_keys\.lower | string | 
action\_result\.data\.\*\.parsed\_whois\.routes\.\*\.mnt\_keys\.routes | string | 
action\_result\.data\.\*\.parsed\_whois\.routes\.\*\.name | string | 
action\_result\.data\.\*\.parsed\_whois\.routes\.\*\.org | string | 
action\_result\.data\.\*\.parsed\_whois\.routes\.\*\.ref | string | 
action\_result\.data\.\*\.parsed\_whois\.routes\.\*\.source | string | 
action\_result\.data\.\*\.parsed\_whois\.routes\.\*\.status | string | 
action\_result\.data\.\*\.parsed\_whois\.routes\.\*\.updated\_date | string | 
action\_result\.data\.\*\.record\_source | string |  `ip`  `ipv6` 
action\_result\.data\.\*\.registrant | string | 
action\_result\.data\.\*\.source | string | 
action\_result\.data\.\*\.whois\.date | string | 
action\_result\.data\.\*\.whois\.record | string | 
action\_result\.summary\.city | string | 
action\_result\.summary\.country | string | 
action\_result\.summary\.organization | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'whois domain'
Execute whois lookup on the given domain

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**domain** |  required  | Domain to query | string |  `domain` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.domain | string |  `domain` 
action\_result\.data\.\*\.name\_servers | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.admin\.city | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.admin\.country | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.admin\.email | string |  `email` 
action\_result\.data\.\*\.parsed\_whois\.contacts\.admin\.fax | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.admin\.name | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.admin\.org | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.admin\.phone | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.admin\.postal | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.admin\.state | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.admin\.street | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.billing\.city | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.billing\.country | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.billing\.email | string |  `email` 
action\_result\.data\.\*\.parsed\_whois\.contacts\.billing\.fax | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.billing\.name | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.billing\.org | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.billing\.phone | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.billing\.postal | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.billing\.state | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.registrant\.city | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.registrant\.country | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.registrant\.email | string |  `email` 
action\_result\.data\.\*\.parsed\_whois\.contacts\.registrant\.fax | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.registrant\.name | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.registrant\.org | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.registrant\.phone | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.registrant\.postal | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.registrant\.state | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.registrant\.street | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.tech\.city | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.tech\.country | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.tech\.email | string |  `email` 
action\_result\.data\.\*\.parsed\_whois\.contacts\.tech\.fax | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.tech\.name | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.tech\.org | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.tech\.phone | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.tech\.postal | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.tech\.state | string | 
action\_result\.data\.\*\.parsed\_whois\.contacts\.tech\.street | string | 
action\_result\.data\.\*\.parsed\_whois\.created\_date | string | 
action\_result\.data\.\*\.parsed\_whois\.domain | string |  `domain` 
action\_result\.data\.\*\.parsed\_whois\.expired\_date | string | 
action\_result\.data\.\*\.parsed\_whois\.name\_servers | string | 
action\_result\.data\.\*\.parsed\_whois\.other\_properties\.dnssec | string | 
action\_result\.data\.\*\.parsed\_whois\.other\_properties\.domain\_domain\_status | string |  `domain` 
action\_result\.data\.\*\.parsed\_whois\.other\_properties\.registry\_domain\_id | string |  `domain` 
action\_result\.data\.\*\.parsed\_whois\.registrar\.abuse\_contact\_email | string |  `email` 
action\_result\.data\.\*\.parsed\_whois\.registrar\.abuse\_contact\_phone | string | 
action\_result\.data\.\*\.parsed\_whois\.registrar\.iana\_id | string | 
action\_result\.data\.\*\.parsed\_whois\.registrar\.name | string | 
action\_result\.data\.\*\.parsed\_whois\.registrar\.url | string |  `url` 
action\_result\.data\.\*\.parsed\_whois\.registrar\.whois\_server | string |  `host name` 
action\_result\.data\.\*\.parsed\_whois\.statuses | string | 
action\_result\.data\.\*\.parsed\_whois\.updated\_date | string | 
action\_result\.data\.\*\.record\_source | string | 
action\_result\.data\.\*\.registrant | string | 
action\_result\.data\.\*\.registration\.created | string | 
action\_result\.data\.\*\.registration\.expires | string | 
action\_result\.data\.\*\.registration\.registrar | string | 
action\_result\.data\.\*\.registration\.statuses | string | 
action\_result\.data\.\*\.registration\.updated | string | 
action\_result\.data\.\*\.whois\.date | string | 
action\_result\.data\.\*\.whois\.record | string | 
action\_result\.summary | string | 
action\_result\.summary\.city | string | 
action\_result\.summary\.country | string | 
action\_result\.summary\.organization | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric | 