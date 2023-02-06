# Understanding AWS Accounts, AWS Organisations and Service Control Policies

In our previous [post](https://hashnode.com/post/clclv46rf000708l82verd3ym), we discussed some of the best practices for AWS Identities. As organisational structures become more complex, it also gets trickier to manage multiple AWS accounts and this cannot by any means be taken for granted.

AWS Accounts, AWS Organisations and Service Control Policies (SCP) are three important components that work together to provide secure and efficient cloud management of access to resources on multiple AWS accounts.

An AWS account is a unique identifier that gives you access to AWS services and resources. It allows you to create and manage your resources, such as Amazon Elastic Compute Cloud (EC2) instances, Amazon Simple Storage Service (S3) buckets, and more. You can create multiple AWS accounts for different purposes, such as development, testing, staging, and production environments.

AWS Organizations is a feature that allows users to centralise the management of multiple AWS accounts within a single organisation. It allows you to create a hierarchy of accounts, called an organisational structure, and apply policies that span across all accounts in the organisation. This is especially useful for businesses with multiple teams or departments that need to have their AWS accounts, as it allows them to manage access and permissions across all accounts easily.

One key aspect of AWS Organizations is the ability to use service control policies (SCPs). SCPs are used to set permissions and policies for the accounts within an organisation. They can be used to control which AWS services and resources can be accessed by users or applications within those accounts.

SCPs can be applied at the root level of an organisation or to individual accounts or organisational units within the organisation. This allows administrators to set policies at a global level, as well as granularly control access for specific accounts or teams. SCPs help you enforce security, compliance, and governance policies across your AWS environment.

SCPs are written in JSON format and use conditions and permissions to specify what actions are allowed or denied. For example, an SCP could be used to allow users in a specific account to access only certain S3 buckets or to deny access to certain EC2 instance types.

One of the key benefits of using SCPs is that you can use them to enforce the least privileged access to your AWS resources. This means that users and roles can only access the resources that they need to perform their job tasks and nothing more. This helps reduce the risk of accidental or malicious actions that could compromise the security or stability of your AWS environment. For example, an organisation may have an SCP that denies access to certain services or resources to meet compliance standards.

Another benefit of SCPs is that they can be used to enforce best practices and standards within an organisation. For example, an organisation may have an SCP that requires users to use secure protocols when accessing specific resources or that limits the number of resources that can be created in a specific account.

Overall, AWS Organizations and SCPs provide a powerful tool for managing and securing multiple AWS accounts within a single organisation. By centralising management and using SCPs to set permissions and policies, organisations can ensure compliance, enforce best practices, and effectively manage access to resources across all accounts.