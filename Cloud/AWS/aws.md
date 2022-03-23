# Amazon Web Services

* [AWS Documentation](https://aws.amazon.com/documentation/)
* [AWS News Blog](https://aws.amazon.com/blogs/aws/)
* [AWS Simple Monthyl Calculator](https://calculator.s3.amazonaws.com/index.html)
* [AWS Free Tier Signup](https://aws.amazon.com/free/)
* [AWS Tools](https://aws.amazon.com/tools/)
* [AWS Getting Started](https://aws.amazon.com/getting-started/)

## [Overview of Amazon Web Services](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/introduction.html?pg=gs&sec=syj&refid=ce1f55b8-6da8-4aa2-af36-3f11e9a449ae)

Basic stuff that is obvious to anyone familiar with cloud computing.

### [Amazon Web Services Cloud](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/amazon-web-services-cloud-platform.html)

Section has a brief summary for every(?) service AWS offers.

### [AWS Documentation](https://docs.aws.amazon.com/index.html)

Sections:

## Compute

### EC2

* [EC2 Getting Started Guide](https://docs.aws.amazon.com/console/ec2/EC2_GetStarted.html)\
* [EC2 Getting Started with Windows Instances](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/EC2_GetStarted.html)
* [Using EC2 through the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-using-ec2.html)
* [EC2 Console](http://console.aws.amazon.com/ec2)
* [Install a LAMP Stack on Amazon Linux 2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-lamp-amazon-linux-2.html)

#### Generating a Key Pair

Under network and security > Key Pairs.

#### AMI

An AMI (Amazon Machine Image) is a base image, used to launch instances or clone environments from. Similar to a Docker Image (although for a VM instead of a container)?

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

## Containers

## Storage

### EBS

EBS (Elastic Block Storage) is long term storage, whereas local storage lasts the length of a running instance. EBS volumes are attached to EC2 instances and can be used like any other block device.

There are two types of EBS volumes: standard volumes and provisioned IOPS volumes.

* Each volume can be up to 1TB and multiple volumes can be attached to an EC2 instance
* IOPS volumes can be used to specify I/O performance
* EBS volumes are stored on S3

### EFS

File storage.

### S3 (Simple Storage Service)

* [S3 Notes](S3.md).

## Database

### AWS Elasticache

Supports two popular caching engines, Memcached and Redis.

## Security, Identity, & Compliance

* [IAM Notes](IAM.md)

## Cryptography & PKI

## Machine Learning

## Management & Governance

## Developer Tools

## Migration & Transfer

## Networking & Content Delivery

### AWS CloudFront

CloudFront is a CDN service with regional caching.

## Media Services

## Internet of Things (IoT)

## Front-End Web & Mobile

## End User Computing

## Analytics

## Application Integration

## Business Applications

## Customer Enablement Services

## Satellite

## Robotics

## Quantum Computing

## Blockchain

## AR & VR

## Game Development

## General Reference

## Cloud Financial Management

## AWS Management Console

## SDKs & Toolkits

## Additional Resources