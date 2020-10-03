## AWS SAA-C02

${toc}

# Introduction
The exam validates the following abilities for an examinee
* Define a solution using architectural design principles based on customer requirements.
* Provide implementation guidance based on best practices to an organization throughout the lifecycle of a
project.

The examination scores are reported as a score from 100-1,000, with a minimum passing score of 720.
Your score shows how you performed on the examination as a whole and whether or not you passed. 

# Exam Blueprint
|Domain|% of examination|
|------|----------------|
|Design Resilient Architectures| 30%|
|Design High-Performing Architectures| 28%|
|Design Secure Applications and Architectures| 24%|
|Design Cost-Optimized Architectures| 18%|
|TOTAL| 100%|

# Recommended Reading (FAQs)
* [AWS Well Architected Framework](https://aws.amazon.com/architecture/well-architected/)
* [Amazon EC2](https://aws.amazon.com/ec2/faqs/)
* [Amazon S3](https://aws.amazon.com/s3/faqs/)
* [Amazon VPC](https://aws.amazon.com/vpc/faqs/)
* [Amazon Route 53](https://aws.amazon.com/route53/faqs/)
* [Amazon RDS](https://aws.amazon.com/rds/faqs/)
* [Amazon SQS](https://aws.amazon.com/sqs/faqs/)

# Exam Readiness
* Check out the exam readiness page [here](https://www.aws.training/Details/Curriculum?id=20685) 

## Design Resilient Architectures
* Design a multi-tier architecture solution
* Design highly available and/or fault-tolerant architectures
* Design decoupling mechanisms using AWS services
* Choose appropriate resilient storage

## Design High-Performing Architectures
* Identify elastic and scalable compute solutions for a workload
* Select high-performing and scalable storage solutions for a workload
* Select high-performing networking solutions for a workload
* Choose high-performing database solutions for a workload

##  Design Secure Applications and Architectures
* Design secure access to AWS resources
* Design secure application tiers
* Select appropriate data security options

## Design Cost-Optimized Architectures
* Identify cost-effective storage solutions
* Identify cost-effective compute and database services
* Design cost-optimized network architectures

# IAM

## Introduction

AWS Identity and Access Management service allows you to manage users and their levels of access to various resources within one or more AWS accounts. IAM service is global and is not tied to a particular region. Changes made in IAM are applied uniformly across all regions.

- IAM allows for centralized control and administration of access to your AWS account
- Shared access to your IAM account
- Granular permissions
- Identity federation (including active directory, social logins etc)
- Helps secure accounts via MFA
- provides temporary access to resources
- Deep integration with most AWS resources
- It is also PCI DSS compliant (passes government mandated credit card security regulations).

## IAM Entities

- Users - Individuals such as Developers, engineers etc. New users do not have any permissions when created.
- Groups - a collection of users used to manage users who need similar levels of access to AWS resources. Allows easier management of access by attaching policies and roles at the group level. Each user in the group will inherit the same set of permissions as the ones associated with the group.
You cannot nest IAM Groups. Individual IAM users can belong to multiple groups, but creating subgroups so that one IAM Group is embedded inside of another IAM Group is not possible.

- Roles - Are used by one AWS resource/user to access another AWS resource in the same or different AWS account. IAM Roles can be assigned to a service, such as an EC2 instance, prior to its first use/creation or after it is used/created. You can change permissions as many times as you need. This can all be done by using both the AWS console and the AWS command line tools.

- Policies - rule sets allowing or denying access to a resource to which the policy is attached to. Policies are written in JSON. There are several built in policies provided by AWS. Users are also able to create custom policies for their specific needs. IAM Policies can be attached to users, groups or to roles.

With IAM Policies, you can easily add tags that help define which resources are accessible by whom. These tags are then used to control access via a particular IAM policy. For example, production and development EC2 instances might be tagged as such. This would ensure that people who should only be able to access development instances cannot access production instances.

## Priority Levels in IAM
Default Deny (or Implicit Deny): IAM identities start off with no resource access. Access instead must be granted.
* Explicit Allow - Allows access to a particular resource so long as there is not an associated Explicit Deny.
* Explicit Deny - Denies access to a particular resource and this ruling cannot be overruled.


# S3

## Introduction

S3 allows storage of objects composed of a file and associated metadata about the file. The stored objects can be 0 bytes to 5TB. S3 objects has the following attributes.

1.  Key(name of the object)
2.  Value (the data/contents of the object)
3.  Version ID (contains the current version ID)

Objects are stored in buckets. The name given to S3 buckets must be globally unique. Bucket names are based on DNS which is a global namespace. During creation the S3 buckets will need to be hosted in specific regions.

Object metadata are of two type
* system metadata 
* user metadata

Metadata associated with an uploaded object cannot be modified.

Objects of up to 5GB can be stored in a single file upload. Objects greater than 5GB up to 5TB must use the multipart upload API.

## S3 bucket restrictions and limitations
If a bucket is empty, you can delete it. After a bucket is deleted, the name becomes available for reuse as long as no one else registers a bucket with the same name before you do.

Buckets cannot be nested. An S3 bucket can expand infinitely to store any amount of data.

Upon creation buckets are private by default and will need to be made public explicitly. This is by design so as to avoid inadvertent disclosure of data.

once created Bucket names cannot be changed. 

Bucket names must be between 3 and 63 characters long.

You can't migrate an existing S3 bucket into another AWS Region.

Bucket names can consist only of lowercase letters, numbers, dots (.), and hyphens (-).

Bucket names must begin and end with a letter or number.

Bucket names must not be formatted as an IP address (for example, 192.168.5.4).

Bucket names can't begin with xn-- (for buckets created after February 2020).

Bucket names must be unique within a partition. A partition is a grouping of Regions. AWS currently has three partitions: aws (Standard Regions), aws-cn (China Regions), and aws-us-gov (AWS GovCloud [US] Regions).

Buckets used with Amazon S3 Transfer Acceleration can't have dots (.) in their names. For more information about transfer acceleration, see Amazon S3 Transfer Acceleration.

## S3 Features
* Tiered storage and pricing variability
* lifecycle management to expire older content
* versioning of objects
* encryption at rest and in transit
* MFA deletes to prevent accidental or malicious removal of content
* access control lists & bucket policies to secure the data
* Deep integration with other AWS services such as Lambda, redshift, Cloudfront etc
* Static Website hosting

## S3 SLA

* 99.99% availability for S3 platform
* Amazon guarantees 99.9% availability
* Amazon guarantees 99.999999999% durability fo S3 information (11x9s)

## S3 storage classes

- S3 standard
- S3 IA
- S3 One Zone IA
- S3 intelligent tiering
- S3 Glacier
- S3 Glacier Deep Archive

## Comparison of different S3 storage classes

|     | S3 standard | S3 Intelligent Tiering | S3 Standard IA | S3 one zone IA | S3 Glacier | S3 Glacier Deep Archive |
| --- | --- | --- | --- | --- | --- | --- |
| Durability | 11x9s | 11x9s | 11x9s | 11x9s | 11x9s | 11x9s |
| Availability | 99.99% | 99.9% | 99.9% | 99.5% | N?A | n/A |
| Availability Zones | >=3 | >=3 | >=3 | 1   | >=3 | >=3 |
| Minimum Capacity charge/object | NA  | NA  | 128KB | 128KB | 40KB | 40KB |
| Minimum storage duration charge | NA  | 30 Days | 30 Days | 30 Days | 90 Days | 180 Days |
| Retrieval fee | NA  | NA  | per GB Retrieved | per GB Retrieved | per GB Retrieved | per GB Retrieved |
| First byte latency | ms  | ms  | ms  | ms  | Select minutes or Hours | Select hours |

## S3 Charges

- Charged for storage for each object.
- Charge by total number of requests
- Storage management pricing (different tiers)
- Data Transfer Pricing (in/out)
- Transfer acceleration (Speed up upload downloads via integration with cloudfront edge nodes)
- Cross region replication pricing

## S3 data consistency
|operation|consistency|Retrieval type| time | 
|---------|-----------|------------|-------|
|PUTS|Read-After-Write| GET, HEAD | After creation |
|PUTS|Eventual | GET, HEAD | before creation |
|Overwrite PUTS|Eventual | GET, HEAD | After overwrite|
|DELETE |Eventual | GET, HEAD | After Deletion|

Updates to a single key are atomic. For example, if you PUT to an existing key, a subsequent read might return the old data or the updated data, but it never returns corrupted or partial data.

## S3 security

### S3 access control

Bucket policies - control access at bucket level 
ACL - control access at  at object level 

|Access type|account Type|controlled via|
|-----------|--------------|--------------|
|Programatic access|Same account| IAM, Bucket policies|
|Programatic access| Same account | IAM, ACL, Bucket policies|
|Console & Terminal| Cross account| cross account IAM roles|


### Logging
S3 supports access logs where all access to objects are logged and can be written to another S3 bucket in the same or another account.

### encryption

encryption in transit SSL/TLS encryption at rest

- SSE
- Client side encryption

#### Client side encryption

Customer encrypts the object to be store and uploads the object to S3. The keys are never disclosed to amazon both encryption and decryption happen on the client side.

#### SSE

1.  S3 Managed keys SSE-S3
2.  AWS KMS, Managed Keys - SSE-KMS
3.  SSE with customer provided keys SSE-C

### S3 Object locks
Can add WORM locks to Standard S3 and glacier. two kinds
* S3 Object lock - WORM
* Glacier vault lock - WORM

either for specified time or indefinitely.

#### Modes

* Governance.
users cannot overwrite or delete an object version or alter it locks settings. Can however provide specific users  permissions to alter the retention settings or delete the object if necessary.

* Compliance mode
Cannot be overwritten or deleted by any users even by the root user of the account.Retention period once set cannot be shortened or changed.

Retention period specified how long the items are protected from being overwritten or deleted. once a retention period ends the objects can be overwritten or deleted unless there is also a legal hold applied to the object. Legal hold can be applied b any user who has the s3putlegalhold permissions.

very similar to the S3 Object lock but applies to glacier.


## S3 HTTP Status codes

|Error Types|Response code|
|-----------|-------------|
|NotSignedUp,InvalidSecurity,InvalidObjectState,InvalidPayer,InvalidAccessKeyId,Access denied,AccountProblem,AllAccessDisabled,CrossLocationLoggingProhibited|403|
|BucketAlreadyExists,BucketAlreadyOwnedByYou,BucketNotEmpty,InvalidBucketState,OperationAborted|409|
|InvalidRange|416|
|MethodNotAllowed| 405|
|MissingContentLength|411|
|NotImplemented|501|


## S3 Versioning

The versioning feature on S3 buckets stores all versions of an object including all writes and even if you delete an object. Once enabled it cannot be disabled only suspended. Integrates with lifecycle rules. versioning allows MFA delete capability which requires MFA authentication to delete the versioned objects in buckets. To restore a deleted file in an S3 versioned bucket you can delete the deletion marker for the file to restore the file.

If a file was initially set to public upon uploading a new version the newer version  will be made private by default. The original versions of files retain whatever permissions they were assigned. While newer version are made private by default.


## S3 Object lifecycle management
Automates the transition of objects between the different storage tiers.
Can be used in conjunction with versioning this can be applied to both current and previous versions of an object.
When setting up lifecycle rules it is important to have the prefix filter end with a "/" for e.g images/ if the filter does not have the "/" at the end or is at the beginning  this can cause the lifecycle rule to be evaluated incorrectly.

## S3 webhosting 
S3 can host static websites. this feature has to be explicitly enabled on the bucket and the objects that need to be served made public either via ACL or a bucket policy.

When serving static content both a index.html and an error.html are needed

## S3 cross region replication
* Cross region replication only work if versioning is enabled.
* When cross region replication is enabled, no pre-existing data is transferred. Only new uploads into the original bucket are replicated. All subsequent updates are replicated.
* When you replicate the contents of one bucket to another, you can actually change the ownership of the content if you want. You can also change the storage tier of the new bucket with the replicated content.
* When files are deleted in the original bucket (via a delete marker as versioning prevents true deletions), those deletes are not replicated.


## S3 Event Notifications
The Amazon S3 notification feature enables you to receive and send notifications when certain events happen in your bucket. To enable notifications, you must first configure the events you want Amazon S3 to publish (new object added, old object deleted, etc.) and the destinations where you want Amazon S3 to send the event notifications. Amazon S3 supports the following destinations where it can publish events:

Amazon Simple Notification Service (Amazon SNS) - A web service that coordinates and manages the delivery or sending of messages to subscribing endpoints or clients.

Amazon Simple Queue Service (Amazon SQS) - SQS offers reliable and scalable hosted queues for storing messages as they travel between computers.
AWS Lambda - AWS Lambda is a compute service where you can upload your code and the service can run the code on your behalf using the AWS infrastructure. You package up and upload your custom code to AWS Lambda when you create a Lambda function. The S3 event triggering the Lambda function also can serve as the code's input.

## S3 Performance Optimization
 Amazon S3 bucket can support 3,500 PUT/COPY/POST/DELETE or 5,500 GET/HEAD requests per second per partitioned prefix. To optimize S3 buckets for high request rates, consider using an object key naming pattern that distributes your objects across multiple prefixes. Each additional prefix enables the  buckets to scale to support an additional 3,500 PUT/COPY/POST/DELETE or 5,500 GET/HEAD requests per second. This can be achieved by adding semi random prefixes
 
 SSE-KMS affects the performance of Object retrieval/upload as there are limits to the KMS encrypt/decrypt operations and currently these limits are not extendable.
 
 Use multipart upload for objects bigger than 100MB
 For download split files into parts Via byte ranges
 
 ## S3 select/Glacier select
 Retrieve only the subset of data needed instead of getting a complete file. It works based on SQL. Write a query that allows you to only retrieve data you need. Can get data based on rows or columns.
 
## Amazon S3 Inventory reports
S3 Inventory reports can be used to audit and report on the replication and encryption status of your objects for business, compliance, and regulatory needs.  They can also be used to troubleshoot issues with S3 notifications by using the LIST Objects API or Amazon S3 Inventory reports to check for missed events.

## S3 Cheatsheet
* See a very comprehensive S3 cheatsheet [here](https://tutorialsdojo.com/amazon-s3/)

# AWS Organizations
Allows to consolidate and manage multiple AWS accounts from a single central organizational account. Organized as a hierarchical tree where objects called OUs are used to organize different accounts. The permissions are applied via policies. Policies are inherited by all children when applied to a parent node. Explicit deny overrides allow at child level.s

Consolidated billing is another feature provided by AWS Organizations.

Organizations can be setup by first going to the root account and then creating an organization and sending invitations to other accounts or create a new account.

Invitations once issued cannot be changed they will have to be deleted and reissued. Invitations expire after 15 days.

SCP is service control policies which allow and restrict access to AWS resource for certain organization units or individual accounts.

## Resources
[https://github.com/keenanromain/AWS-SAA-C02-Study-Guide](https://github.com/keenanromain/AWS-SAA-C02-Study-Guide)
