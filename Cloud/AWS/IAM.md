# [AWS Identiy and Access Management](https://docs.aws.amazon.com/iam/index.html)

## [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/index.html)

### [What is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)

The root AWS account that you start with has access to all AWS services and resources in the account. It is recommended that the root account is only used to create another IAM user which then performs administrative tasks.

#### [Understanding how IAM works](https://docs.aws.amazon.com/IAM/latest/UserGuide/intro-structure.html)

##### [Terms](https://docs.aws.amazon.com/IAM/latest/UserGuide/intro-structure.html#intro-structure-terms)

IAM Resources
* The user, group, role, policy, and identity provider objects that are stored in IAM.

IAM Identities
* The IAM resource objects that are used to identify and group. You can attach a policy to an IAM identity. These include users, groups, and roles.

IAM Entites
* The IAM resource objects that AWS uses for authentication. These include IAM users and roles.

Principals
* A person or application that uses the AWS account root user, an IAM user, or an IAM role to sign in and make requests to AWS. Principals include federated users and assumed roles.