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

### [Users in AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_identity-management.html)

Only service control policies (SCPs) in organizations can restrict the permissions that are granted to the root user.

#### [IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_identity-management.html#intro-identity-users)

IAM users are users within the AWS account. Each user can have a password to access the AWS Console, and/or an access key to make programmatic requests. Users can also be applications, an IAM user doesn't have to be a person. E.g. you might create a user for an on-premise application that needs AWS access.

#### [Permissions and policies in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_access-management.html)

TODO

#### [What is ABAC](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_attribute-based-access-control.html)

Attribute-based access control is an authorisation strategy that defines permissions based on attributes....

TODO