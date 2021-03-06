# Amazon Web Services

* [AWS Documentation](https://aws.amazon.com/documentation/)
* [AWS News Blog](https://aws.amazon.com/blogs/aws/)
* [AWS Simple Monthyl Calculator](https://calculator.s3.amazonaws.com/index.html)
* [AWS Free Tier Signup](https://aws.amazon.com/free/)

## Temp, AWS Service List

* AWS Elastic Beanstalk
* AWS OpsWorks
* AWS CloudFormation
* AWS CodeDeploy

## Data Storage

### EBS

EBS (Elastic Block Storage) is long term storage, whereas local storage lasts the length of a running instance. EBS volumes are attached to EC2 instances and can be used like any other block device.

There are two types of EBS volumes: standard volumes and provisioned IOPS volumes.

* Each volume can be up to 1TB and multiple volumes can be attached to an EC2 instance
* IOPS volumes can be used to specify I/O performance
* EBS volumes are stored on S3

### EFS

File storage.

### S3 (Simple Storage Service)

* [Amazon S3 Website](https://aws.amazon.com/s3/)

S3 has no defined limit, it can scale and grow with the storage needs of an organisation, but each object is limited to 5TB.

Object storage. Objects are stored in a flat organisation, referred to as buckets in S3 and retrieved by a unique ID (key). The flat hierarchy allows for greater scalability and faster retrieval than a normal file hierachy.

RRS - Reduced Redundancy Storage, this comes at a reduced cost and can be used for easily reproduced data.

S3 works on an eventual consistency model, so the objects are highly available and highly durable, but the data consistency is only achieved eventually. It takes time to propagate the changes to all the replicas.

### Glacier

Object storage used for archiving data, data retrieval time is several hours and should only be used for very infrequently accessed data. High durability is guaranteed and Glacier has a much lower cost than S3 (which it is built on).

### RDS (Amazon Relational Data Service)

Supports MySQL, Postgres, Aurora, MariaDB, Oracle, SQL Server

### Amazon DynamoDB

NoSQL, non-relational, schema-less. Data is stored on SSDs and auto replicated across multiple availability zones, data speed is very fast.

## Networking

* Elastic IPs - static but not instance specific, instead they are created at the account level and easily mapped and remapped to instances. This allows for simple failovers between servers to easily reroute traffic, this also works great for rolling out  application update.

### ELB

The ELB (Elastic Load Balancer) is an AWS service for balancing network traffic across multiple EC2 instances within multiple availability zones. ELB can handling routing of HTTP, HTTPS, and TCP traffic (hmm?). ELB also;

* Supports health check configuration.
* Auto scales based on demands placed on it
* Single CNAME for DNS configuration

## Regions

AWS has locations in several geographic regions, and each region has availability zones. Multiple availability zones and even regions can be utilised incase of disasters.

## EC2

* [EC2 Getting Started Guide](https://docs.aws.amazon.com/console/ec2/EC2_GetStarted.html)\
* [EC2 Getting Started with Windows Instances](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/EC2_GetStarted.html)
* [Using EC2 through the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-using-ec2.html)
* [EC2 Console](http://console.aws.amazon.com/ec2)
* [Install a LAMP Stack on Amazon Linux 2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-lamp-amazon-linux-2.html)

### Generating a Key Pair

Under network and security > Key Pairs.

### AMI

An AMI (Amazon Machine Image) is a base image, used to launch instances or clone environments from. Similar to a Docker Image (although for a VM instead of a container)?

## Amazon Services

### Elastic Beanstalk

Most convenient, least control. Fully managed service, just upload the application, supported platforms include:

* Apache Tomcat
* Apache HTTPD Server for PHP and Python applications
* NGINX or HTTPD for Node.js applications
* Passenger or Puma for Ruby applications
* Microsoft IIS 7.5, 8.0, and 8.5 for .NET apps
* Java SE
* Docker
* Go

Beanstalk can also automatically pushing application & server logs to S3.

Config files can be written in YAML or JSON.

### OpsWorks

OpsWorks balances convenience and control and has two offerings, AWS OpsWorks for Chef Automate, and AWS OpsWorks Stacks.

Chef is used for configuration. OpsWorks provides two primary parts to the OpsWorks service, the OpsWorks provisioning enginge, and the OpsWorks agent.

#### Stacks

Organised into Layers and Stacks. A stack contains several layers such as a Web Server, App Server, and Database, multiple Stacks of these might include test, staging, and production environments.

#### Chef Automate

### CloudFormation

Cloudfoundation and Cloudformer(?).

#### CloudFormer

CloudFormer helps to create a CloudFormation template from an existing stack. CloudFormer is itself a CloudFormation stack.

### CodeDeploy

* Component service
* Coordinates deployments across EC2 instances
* Not framework, language, or stack dependent
* Scalableh

### Simple Message Queue Service (SQS)

Reliable, highly scalable, distributed system for passing messegaes between application components.
Allows for decoupling and improved failure tolerance. These queues allow components to communicate asynchronously, to support concurrency and remain highly available, and to better hanlde load spikes.

Basically, SQS provides a buffer for messages sent between components.

### Simple Workflow Service (SWF)

Not really sure what this does.

### Simple Notification Service (SNS)

Similar to an observer pattern, but application instead of class level. Can be used to monitor the health of an application.

### AWS CloudSearch

A search engine, providing fast, reliable, relevant, and quality results to a query.

### Amazon API Gateway

A fully managed service.

### AWS Lambda

Lambda is a serverless architecture.

### Identity and Access Management (IAM)

Don't use the master account to access or manage resources, create seperate users, groups, roles, and permissions in IAM and only allow access where necessary and only to the specific resources that are needed.

### Virtual Private Cloud (VPC)

## Caching

### AWS Elasticache

Supports two popular caching engines, Memcached and Redis.

### AWS CloudFront

CloudFront is a CDN service with regional caching.

### AWS Bastion Hosts

* [AWS Bastion Docs](https://docs.aws.amazon.com/quickstart/latest/linux-bastion/architecture.html)