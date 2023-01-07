# AWS Accounts and Identity Management Best Practises

From a security perspective, AWS Accounts and Identity Management is one of the things to get right when working on the AWS cloud platform. Keeping in mind best practices and ensuring that the proper permissions and privileges are granted appropriately to accounts and identities is one of the core decisions that can make developing on the cloud a smooth sail or a terrible nightmare. Imagine waking up to the news that a compromised team member's account raked up millions of pounds in cloud bills simply because they had too much privilege than was required for them to perform their duties successfully. Properly configured accounts and identities are required to reduce the blast radius for situations like this.

So let’s get started by describing what an AWS account is. The best way to describe an AWS account is to look at it as a container for different AWS resources and identities/users. In other words, they give you access to the world of AWS. To create one, you need to provide a few details, such as a name, a unique email address and a payment method. This creates an account root user with complete control and unrestricted access to AWS resources within the account. Also, billing on AWS is pay-as-you-go, meaning you’re only billed for what you use at the end of the month.

AWS (Amazon Web Services) is a cloud computing platform that provides a wide range of services to businesses and organizations around the world. One of the key features of AWS is its ability to manage accounts and identities for users, enabling organizations to effectively control access to their resources and data.

However, managing accounts and identities can be a complex and time-consuming process, especially for large organizations with many users. To ensure that your organization is taking full advantage of the benefits of AWS while also maintaining the highest level of security and compliance, it is important to follow best practices for AWS account and identity management.

Here are some tips for managing accounts and identities on AWS:

1. Create separate AWS accounts for different departments or teams: Rather than having all of your users access the same AWS account, it is a good idea to create separate accounts for different departments or teams. This helps to ensure that users only have access to the resources and data that they need and reduces the risk of unauthorised access to sensitive information.
    
2. Use IAM (Identity and Access Management) policies: IAM policies enable you to control who has access to your AWS resources and what actions they can perform. It is essential to carefully define and maintain these policies to ensure that only authorised users have access to your resources.
    
3. Use multi-factor authentication: MFA (multi-factor authentication) adds an extra layer of security to your AWS accounts by requiring users to provide a second form of authentication (such as a one-time code sent to their phone) in addition to their username and password. This helps to prevent unauthorised access to your accounts.
    
4. Rotate access keys regularly: Access keys are used to access AWS resources programmatically (e.g., through the AWS API). Rotating these keys regularly is a good practice to reduce the risk of unauthorised access.
    
5. Monitor activity in your AWS accounts: AWS provides tools such as CloudTrail and AWS Config that enable you to monitor activity in your accounts. It is essential to regularly review these logs to ensure that only authorised users are accessing your resources and to detect any suspicious activity.
    

By following these best practices for an AWS account and identity management, you can ensure that your organisation is taking full advantage of the benefits of AWS while also maintaining the highest level of security and compliance.