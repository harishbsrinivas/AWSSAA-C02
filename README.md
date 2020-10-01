# AWS SAA-C02

## AWS SAA-C02

${toc}

# Introduction
The exam validates the following abilities for an examinee
* Define a solution using architectural design principles based on customer requirements.
* Provide implementation guidance based on best practices to an organization throughout the lifecycle of a
project.

The exam contains 
the examination sores are reported as a score from 100-1,000, with a minimum passing score of 720.
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

Object based storage where objects can be 0 bytes to 5TB. S3 objects has the following attributes

1.  Key(name of the object)
2.  Value (the data/contents of the object)
3.  Version ID (contains the current version ID)

Files are stored in buckets. Name given to S3 buckets must be globally unique. Bucket names are based on DNS which is a global namespace.

Upon creation buckets are private by default and will need to be made public explicitly. This is by design so as to avoid inadvertent disclosure of data.

## S3 data consistency
|operation|consistency|Retrieval type| time | 
|---------|-----------|------------|-------|
|PUTS|Read-After-Write| GET, HEAD | After creation |
|PUTS|Eventual | GET, HEAD | before creation |
|Overwrite PUTS|Eventual | GET, HEAD | After overwrite|
|DELETE |Eventual | GET, HEAD | After Deletion|

Updates to a single key are atomic. For example, if you PUT to an existing key, a subsequent read might return the old data or the updated data, but it never returns corrupted or partial data.


## S3 SLA

99.99% availability for S3 platform

- Amazon guarantees 99.9% availability
- Amazon guarantees 99.999999999% durability fo S3 information (11x9s)

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

- Charged for storage
- Requests
- Storage management pricing
- Data Transfer Pricing
- Transfer acceleration
- Cross region Replication Pricing

## S3 security

### S3 access control

Bucket policies - control access at bucket level 
ACL - control access at  at object level 


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

## S3 Cheatsheet
* See a very comprehensive S3 cheatsheet [here](https://tutorialsdojo.com/amazon-s3/)

## Resources

[https://github.com/keenanromain/AWS-SAA-C02-Study-Guide](https://github.com/keenanromain/AWS-SAA-C02-Study-Guide)
