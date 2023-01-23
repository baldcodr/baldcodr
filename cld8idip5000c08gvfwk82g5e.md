# Understanding different AWS identities and their specific use cases

AWS identities are integral to Amazon Web Services (AWS) and are used to manage access to various AWS resources and services. AWS identities are designed to help organisations securely access and manage their resources while also providing a way to grant permissions to other users or groups.

The security pillar of the [AWS well-architected framework](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc) specifies a number of principles that systems built on AWS must follow to meet the specification requirements of the framework. These principles, which include implementing a strong identity foundation, enabling traceability, applying security at all layers, automating security best practices, protecting data in transit and at rest, and keeping people away from data, cannot be implemented effectively without a proper understanding of the various identities and access capabilities offered by AWS. A good understanding of their strengths and vulnerability points is critical for deploying a highly secure system on AWS.

Amazon Web Services (AWS) offers several types of identities to enable you to authenticate and authorise users and services. Some of the AWS identities and their use cases are:

* **AWS Root Account**: This is the primary identity for your AWS account. It has complete access to all resources in your AWS account and is used to manage all the other identities. It is created when you sign up for AWS.
    
* **IAM User**: This identity represents a person or application that uses AWS resources. IAM users can be granted permission to access AWS resources and perform tasks such as creating and managing other IAM users.
    
* **IAM Groups**: IAM groups are a way to manage users and permissions in AWS.
    
    You can create IAM groups and add IAM users to them. You can then apply permissions policies to the groups, which will grant the permissions defined in those policies to all the users in the group. This can make it easier to manage permissions for multiple users, as you can make changes to the group's policies rather than update the policies for each individual user.
    
* **IAM Role**: This identity is similar to an IAM user, but it is not intended to be uniquely associated with a person or application. Instead, it is intended to be assumed by other entities, such as IAM users, applications, or an AWS service.
    
    * **AWS Service Role**: This identity is associated with an AWS service and is used to grant permissions to the service to access other resources in your AWS account.
        
    * **AWS Federated User**: This identity represents a user who is authenticated by an external service, such as an external identity provider or your own corporate identity system.
        
    * **AWS Identity Provider**: This identity represents an external identity provider that is used to authenticate users for your AWS account.
        

Each type of AWS identity has its specific use cases and can be used to manage access to resources and services differently. For example, IAM users are typically used to grant access to individuals or groups within an organisation, while IAM roles are used to grant access to AWS resources. Federated users are often used to grant access to external partners or contractors, while resource-based policies can be used to grant granular access to specific resources.

Overall, AWS identities are an important tool for managing access to resources and services within AWS. By understanding the different types of identities and their specific use cases, organisations can effectively secure and manage their resources within the AWS ecosystem.