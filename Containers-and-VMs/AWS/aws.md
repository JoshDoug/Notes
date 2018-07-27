# Amazon Web Services

* [AWS News Blog](https://aws.amazon.com/blogs/aws/)

## Data

### EBS

EBS (Elastic Block Storage) is long term storage, whereas local storage lasts the length of a running instance. EBS volumes are attached to EC2 instances and can be used like any other block device.

There are two types of EBS volumes: standard volumes and provisioned IOPS volumes.

* Each volume can be up to 1TB and multiple volumes can be attached to an EC2 instance
* IOPS volumes can be used to specify I/O performance
* EBS volumes are stored on S3

### S3 (Simple Storage Service)

* [Amazon S3 Website](https://aws.amazon.com/s3/)

### RDS (Amazon Relational Data Service)

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

### AMI

An AMI (Amazon Machine Image) is a base image, used to launch instances or clone environments from. Similar to a Docker Image (although for a VM instead of a container)?