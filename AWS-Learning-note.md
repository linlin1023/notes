# Tech part
* compute: EC2, Lambda, Elastic Beanstalk;
* storeage: S3, EBS, EFS, FSx, Storage Gateway
* databases: RDS, DynamoDB, Redshit
* Networking: VPCs, Direct Connect, Route 53, API Gateway,  AWS Global Accelerator

## Blocks of AWS
* A region is a physical location in the world that consist of 2 or more Availability Zones
* An Availability Zone is one or more discrete data centers --- each with redundant power, networking, and connnectivity-- housedin separate facilities
* Edge locations are endpoints for AWS that are used for caching content. Typically, this consist of CloudFront, Amazon's CDN.
## Compute

## Storage
image Disk on the cloud
* S3
* EBS
* EFS
* FSx
* Storage Gateway

### S3
automatically scaling with demand. ()
host static website,

bucket name is universal unique
bucket policy
object ACLs

exam tips: any basic senario question about static website, instantly associate static website with S3

versioning of S3: 
 * allversions
 * backup, when versioning is enabled, you cannot stop it, you can only suspend
 * lifecycle rules, 
 * supports MFA

eventhough the object in the bucket is all public and bucket is public, this does not apply to previous version.

* S3 Standard (default one is you create S3)  99.99% avail  11 9's
  * high availability durability: data is stored redundantly across multiple devices in multiple facilites ( an object is stored in at least 3 AZs >= 3AZs)
* S3 Standard - Infrequent Access   99.9%  avail  11 9's
  * Rapid access,
  * pay to access data, low per-GB storage price, and a per-GB retrieval fee
  * user cases: Great for long-term storage, backups, and as a data store for disaster recovery files.
* S3 One Zone - Infrequent Access   99.5% avail  11 9's
  * like S3 standard-IA,
  * data is stored redundantly within a single AZ
  * costs 20% less than regular S3 standard-IA
  * long-live,  infreguqently acccessed, non-critical data
  * a few times per year
* S3 Glacier   99.99%  11 9's
  * 1 minuts to 12 hours
  * pay each time you access your data
  * cheap storage
  * archiving data only
* S3 Glacier deep archive   99.99%  11 9's
  * 12 hours default retriving time
  * once or twice a year
* S3 Intelligent tier 99.9%  11 9's
  * machine learning algorithm
  * optimizes cost   monthly fee of zzzzzzzz40.0025 per 1000 objs
  
#### Object lock  WORM
  * Governance Mode
       In governance mode, users can not overwrite or delete an object version or alter its locking settings unless they have special permissions. With governance mode, you protect objects against being delted by most users, but you can still grant some users permission to alter the retention settings or delete the object if necessary
  * 

## Databases

* RDS
* DynamoDB
* Redshift
* 

## Migration & Transfer


## Network and Content Delivery

* VPCs
* Direct Connect 
* Route 53 ,  DNS
* API Gateway
* AWS Global Accelarator

### Amazon CloudFront
It is a content delivery network(CDN) 
1. fast, low latency, high transfer speed
2. secure: seamlessly integrated with AWS Shield, AWS Web Application Firewall and Amazon Route 53 to protect against multiple types of attackes includign network and applicatio nlayer DDoS attacks. These services co-reside at edge networking locations, - globally scaled and connected via the AWS network backbone
3. programmable : CloudFront works seamlessly with any AWS origin, such as Amazon S3, Amazon EC2, Elastic Load Balancing, or with any custome HTTP origin,  you can customize your content delivery through CloudFront using the secure and programmable edge computing features CloudFront Functions and AWS Labda@Edge

### Edge location

Definition: edge locations is AWS CloudFront and Route 53 services being hosted on a distributed network of proxy servers throughout the world.

Using global Amazon network of edge locations for application delivery and DNS service plays an important role in building a comprehensive defense against the DDoS attacks for your dynamic web applications.

edge locations are endpoints for AWS that are used for caching content.
1. typically, this consists of CloudFront,Amazon;s content delivery network(CDN).
2. there are many more edge locations than Regsions.
3. over 215 edge locations


## Management & Governance


## Analytics

## Security, Identity & Compliance

### DDoS
All AWS customers can benefit from the automatic protections of AWS Shield Standard at no additional charge. AWS Shield Standard defends against the most common and frequently occurring network and transport layer DDoS attacks that target your website or applications. This protection is always on, pre-configured, static, and provides no reporting or analytics. It is offered on all AWS services and in every AWS Region. In AWS Regions, DDoS attacks are detected and the Shield Standard system automatically baselines traffic, identifies anomalies, and, as necessary, creates mitigations.You can use AWS Shield Standard as part of a DDoS-resilient architecture to protect both web and non-web applications.

You can also utilize AWS services that operate from edge locations, such as Amazon CloudFront, Global Accelerator, and Route 53 to build comprehensive availability protection against all known infrastructure layer attacks. These services are part of the AWS Global Edge Network and can improve the DDoS resilience of your application when serving any type of application traffic from edge locations distributed around the world. You can run your application in any AWS Region and use these services to protect your application availability and optimize the performance of your application for legitimate end users.

Benefits of using Amazon CloudFront, Global Accelerator, and Amazon Route 53 include:

Access to internet and DDoS mitigation capacity across the AWS Global Edge Network. This is useful in mitigating larger volumetric attacks, which can reach terabit scale.

AWS Shield DDoS mitigation systems are integrated with AWS edge services, reducing time-to-mitigate from minutes to sub second.

Stateless SYN Flood mitigation techniques proxy and verify incoming connections before passing them to the protected service. This ensures that only valid connections reach your application while protecting your legitimate end users against false positives drops.

Automatic traffic engineering systems that disperse or isolate the impact of large volumetric DDoS attacks. All of these services isolate attacks at the source before they reach your origin, which means less impact on systems protected by these services.

Application layer defense when combined with AWS WAF that does not require changing current application architecture (for example, in an AWS Region or on-premises datacenter).

There is no charge for inbound data transfer on AWS and you do not pay for DDoS attack traffic that is mitigated by AWS Shield. The following architecture diagram includes AWS Global Edge Network services.

## Application Integration


## AWS Cost Management


## Containers




### Region

Scope AWS services
Depending on the AWS service you use, your resources are either deployed at the AZ, Region, or Global level. Each service is different, so you must understand how the scope of a service might affect your application architecture.

When you operate a Region-scoped service, you only need to select the Region you want to use. If you are not asked to specify an individual AZ to deploy the service in, this is an indicator that the service operates on a Region-scope level. For Region-scoped services, AWS automatically performs actions to increase data durability and availability.

On the other hand, some services ask you to specify an AZ. With these services, you are often responsible for increasing the data durability and high availability of these resources.


  
### Security group Inbound Rules
When you create a security group, it has no inbound rules. No inbound traffic originating from another host to your instance is allowed until you add inbound rules to the security group.

### Security group Outbound Rules
By default, a security group includes an outbound rule that allows all outbound traffic. We recommend that you remove this default rule and add outbound rules that allow specific outbound traffic only.

