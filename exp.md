data cached in redis in mainly two ways, one is cache it when query and later query from cache again
and when any update happend to the data clear redis cache,  those data, we require them to be 
accurrate

antoher type of data, we do not have the accuracy requirement, we will set the expire time
for cache.



experience in microservice, NodeJs Microservice
experience in AWS,



how important is the could and cloud computing.
design, deploy, and manage applications in cloud computing.
3-  12 certifications that cover both foundational and specialty cloud computing topics

cloud projects


 public cloud, cloud computing has moved from a nice-to-have to a core competency in the enterprise


# AWS
in Kiwiplan we use AWS to create AMIs which are those machine images that contain different licences and data base setup, to help developers to easily setup customer software environment and to invetigate the issue in production evironment

Could I think up more good usefull points for Kiwiplan form aspects that storage, computing, network, load balance, big data that can help Kiwiplan to move on cloud 


AWS:echo intelligence voice 

### who is using AWS?
>1. NASA/JPL: amazon cloudfront service -> Mars explorer ->
requirement:  process high resolution pics from satelite, and calculation for location
and movement of robot. it used hundrends EC2 points, and SQS merged the resource, it spent 
2 hours to finished processing pictures which normally needs 15 days
>2. musical.ly  --> app

### AWS Resource

>1. google academic  ---> AWS essay
>2. [website to study aws](http://awseducate.com)
>3. [Practise and free try](https://run.qwiklabs.com/)


>region ->  available zone (faul tolerant)  --> sites universal deploy
#### how to access AWS, 
>   1. RESTfull API interface -infrastructure and code, 0101001 the mathine always know
>   2. SDK development tool
>   3. command line interface
>   4. management console 

> JAVA JavaScript Python PHP .NET Ruby, Node.js ... etc all have the coding to access aws

> AWS core service: calculation, web, mysql, storage, IAM (identity access management)


### when do a big concurrent web site, things need to think about is 
1. how to deal with static resources
2. service machine
3. customer quantity 
4. manage resources scalably

### 1. S3   ---(simple storage service)
* in AWS S3 we put static resource: image, video,pure HTML, javascript, CSS, logging file (which is big amount)
* save your disk, and reduce loss when disk crush happen which would happen eventually as a disk would not live forever. reduce service network pressure, save broadband. And do not have to pay for the storage that you do not use
* yulp app uses S3, it can deal with good amount of logging file like 1.2 TB, every day there has 250 EMR job process 30 TB data video create image of user.
* version management, if you delete something by mistake, you could roll back to any version,
* reliable, 
* store data as objects, and those objects are stored in folders which called as buckets or segments
* bucket is container of objects, you could have more than one
* you could set ceate, delete, query permissions for every bucket, 
* create bucket is free, you would only be charged for storing data in the bucket
* 
  
### 2. EC2   --- elastic compute
* for the dynamic thing we need a web service to process it, when the access amount is super big, we need calculate scalably. instance, the cloud visual service, it can chagne the size base on access amount

### 3. ELB  ---elastic load balancing load balancing
* despatch  http, tcp and https requests to instances of EC2 
* it will expost a uniform API to outside,
* health check of EC2s and replace down one with good one
* dynamic expand

### 4. Why we need AWS EC2
* modile app : (not necessary EC2)
  * html5
  * static content on S3
  * on time 
  * kinesis

### 5. EC2 Container

### 6. EBS ----elastic block store, 
* like a vitual disk  volumn, EC2 service can use it
* can separate  your data and computer instance
* one EBS can only connect to one EC2,
* one EC2 can connect to manay EBS
* you could attach lots of volumn and divide them by data type, and improve input and output performance
*  it is good for I/O intense application,

### 7. Cloud Front
### 8. RDBs
### 9. AWS DynamoDB 
* no SQL
* only pay the storage you used and I/O
### 10. Elastic Cache
* help to improve performatce of app with lots of read
* AWS Elastic cache is a web service, it  automize time consuming tasks
* the app that need to deliver information quickly 
* it was used to built app that need instances collecting data and deliver to mobile app
* social media,  gaming, media,  analysis app developer
* often use it to implement cache and imrove performance 
* elastic cache support two open source cache engine, like Redis, Memcached
* application has data structure will find Redis will be more useful
* memcache is liked by itssimplicity 
* Elastic cache has function for auto detach the failure and recover from failure
* pay the resource you consumed by hour

### 11. EMR  ----   Elastic MapReduce
* cluster

### 12. Lambda
region specific
1- code
2- console
3- AWS cli
4- node js, serverless deploy -v, sls deploy -v, sls deploy -f functionname


### 13. IAM  idendity Access Management
* it is a web service that enable Amazon Web Service customers to manage users and user permissions in AWS. With IAM, you can centrally manage users,security, credentials, such as access keys, and permissions that control which AWS resources users can access

* IAM users and groups
* IAM policies 
* real-world scenario, add users to groups with specific capabilities enabled
* locating and using the IAM signin URL
* Experimenting with the effects of policies on service accesss
  
1. Manage IAM Users and their accesss:
   1. you can create users and assign them individual secutiry credentials (access keys, passwords, and multi-factor authenticaton devices). you can manage permissions to control which operations a User an perform
2. Mnaage IAM Roles and their permissions: 
   1. An IAM ROlr is similar to a User, in that it is an AWS identity with permission policies that determine what identity can and cannot do in AWS. However instrad of being uniquely associated wtth one person, a Role is intendede to be assumable by anyone who needs it.
3. Manage federated users and their permissions: 
   1. You can enable identity federation to allow existing users in yo uenterprise to access the AWS Manangement Console, to call AWSS APIs and to access resources, without the nees to cerare an IAM User for each identity
   




aws configurer



  
---
### task 2:

 #### AWS VPC(virtual private cloud),S3, EC2, RDS
* AWS Service Catalog portfolio
* each product is backed by an AWS CloudFormation template
* VPC environment for end user development purposes.That VPC will be the destination you build your other products into.
* EC2 linux instance
* RDS MySQL 
* S3 product is restricted by IAM user and IP address range of your VPC
* 

#### AWS introduction to AWS Identity and Access Management (IAM)
* 

#### AWS lambda lab
1. explorer the Users and Groups that have alreadt been created for you in IAM


----
every day task, I have to do one and learn some thing that really improve my skills and capability
### 1. AWS certifications
### 2. https://run.qwiklabs.com/
### 3. side project
### 4. checkout master degree
### 5. running or excercise
### 6. algorithm





________________
# Nodejs

1. server
2. js core
3. os / process / fs / net, 
4. no browser object which react vue angular doing
   
API from offical web
https://nodejs.org/dist/latest-v10.x/docs/api


run/debug/modulize => build the thing you want









