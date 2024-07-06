---
title: "Threat Modeling - Understanding your system's security posture"
datePublished: Sat Jul 06 2024 13:13:39 GMT+0000 (Coordinated Universal Time)
cuid: clya5b0ki000709l860er6wrg
slug: threat-modeling-understanding-your-systems-security-posture
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720257631558/3a7b8fb1-2393-4345-ab9b-356e1925f2a9.png
tags: aws, security, iam, stride

---

Software systems are designed to withstand attacks, which can only be achieved by a proper knowledge of the breadth and length of your system's attack surface area. When building on a cloud platform like AWS, there are guidelines and best practices in the security pillar of the [Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc) which teams can leverage to build secure systems. However, after the system is completed, we need a living document that gives the security team an overview of the system architecture and the potential security risks an attacker can exploit to wreak havoc on your system alongside mitigations. This is what Threat Modelling provides. In this article, we look to explain what threat modelling is and also understand how we can mitigate vulnerabilities identified in our systems using AWS services.

A threat model is a structured approach used to identify, assess, and mitigate potential security threats to a system or application. The goal is to understand and address the security risks that could negatively impact the confidentiality, integrity, and availability of the system. Threat modelling is a crucial aspect of the software development lifecycle (SDLC) and helps organizations build more secure systems by proactively identifying and addressing potential security issues before they can be exploited.

Below are the guidelines and steps involved in creating a threat model for your system:

1. **Identify Assets**: Identify what assets need to be protected. This could include data, source code, services, IaC, hardware, etc.
    
2. **Define Security Objectives**: Establish what needs to be achieved in terms of security. This includes ensuring data confidentiality, integrity, and availability.
    
3. **Identify Potential Threats**: Enumerate possible threats to the system. This could include external threats like hackers or internal threats like disgruntled employees.
    
4. **Identify Vulnerabilities**: Identify weaknesses in the system that could be exploited by threats. This might include software bugs, weak passwords, or unpatched systems.
    
5. **Assess Threat Impact**: Evaluate the potential impact of each threat if it were to be realized. This helps prioritize the threats based on the damage they could cause.
    
6. **Determine Likelihood**: Estimate the likelihood of each threat occurring. This often involves considering the motivation and capabilities of potential attackers.
    
7. **Mitigation Strategies**: Develop and implement strategies to mitigate the identified threats. This could involve applying patches, improving access controls, or enhancing monitoring and detection capabilities.
    
8. **Documentation and Review**: Document the threat model and review it regularly to ensure it remains up-to-date with the evolving threat landscape and changes in the system.
    

There are several methodologies and frameworks for threat modeling, let us briefly point out some of them:

* **STRIDE**: Focuses on Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, and Elevation of Privilege.
    
* **DREAD**: Assesses risk based on Damage potential, Reproducibility, Exploitability, Affected users, and Discoverability.
    
* **PASTA**: Process for Attack Simulation and Threat Analysis, which is a risk-centric methodology.
    
* **Attack Trees**: Visual representations of the paths an attacker can take to achieve a specific objective.
    

Now we will dive deeper into the STRIDE methodology and how we can leverage AWS security-specific services for mitigations. STRIDE was developed by Microsoft to help identify and classify potential security threats.

The acronym STRIDE stands for six categories of security threats: Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, and Elevation of Privilege.

**1\. Spoofing**

**Description**: Spoofing threats involve an attacker impersonating another user or entity to gain unauthorized access to a system.

**Examples**:

* Using stolen credentials to log into a system.
    
* IP spoofing to disguise the origin of network traffic.
    

**Mitigations:**

* [**AWS Identity and Access Management**](https://aws.amazon.com/iam/)**(IAM)**: Manage user identities and access policies securely.
    
* [**AWS Multi-Factor Authentication**](https://aws.amazon.com/iam/features/mfa/)**(MFA)**: Add an extra layer of security to user logins.
    
* [**AWS Cognito**](https://aws.amazon.com/cognito/): Provide user sign-up, sign-in, and access control to web and mobile apps.
    
* [**AWS Certificate Manager**](https://aws.amazon.com/certificate-manager/)**(ACM)**: Provision, manage, and deploy SSL/TLS certificates.
    

**2\. Tampering**

**Description**: Tampering threats involve unauthorized modifications of data or code. **Examples**:

* Altering data in a database.
    
* Modifying software binaries or configuration files.
    

**Mitigations**:

* [**AWS Key Management Service**](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)**(KMS)**: Create and control encryption keys used to encrypt your data.
    
* [**AWS CloudTrail**](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html): Log and monitor account activity to ensure data integrity.
    
* [**Amazon S3 Object Lock**](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html): Store objects using a write-once-read-many (WORM) model to prevent tampering.
    
* [**AWS CodePipeline**](https://aws.amazon.com/codepipeline/): Automate the release process and ensure only validated code is deployed.
    

**3\. Repudiation**

**Description**: Repudiation threats occur when a user denies performing an action without a way to prove otherwise. **Examples**:

* A user denies making a transaction.
    
* Lack of logs to verify actions taken by users.
    

**Mitigations**:

* **AWS CloudTrail**: Provides a history of AWS API calls for your account, including API calls made via the AWS Management Console, AWS SDKs, command-line tools, and other AWS services.
    
* [**AWS CloudWatch Logs**](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html): Collect and monitor log files, allowing you to track user actions.
    
* [**AWS Config**](https://aws.amazon.com/config/): Provides detailed inventory, configuration history, and configuration change notifications.
    

**4\. Information Disclosure**

**Description**: Information disclosure threats involve the exposure of information to unauthorized individuals.

**Examples**:

* Sensitive data sent over an unencrypted connection.
    
* Inadvertent leakage of data through error messages or debug information.
    

**Mitigations**:

* [**AWS Shield and AWS WAF**](https://docs.aws.amazon.com/waf/latest/developerguide/what-is-aws-waf.html): Protect your applications from DDoS attacks and web exploits.
    
* [**Amazon GuardDuty**](https://aws.amazon.com/guardduty/): Continuous security monitoring service to detect threats.
    
* [**AWS Secrets Manager**](https://aws.amazon.com/secrets-manager/): Protect and manage access to secrets (e.g., database credentials, API keys).
    
* [**AWS Key Management Service**](https://aws.amazon.com/kms/)**(KMS)**: Encrypt data at rest and in transit.
    
* **Amazon S3 Server-Side Encryption (SSE)**: Automatically encrypt data at rest in S3.
    

**5\. Denial of Service (DoS)**

**Description**: Denial of Service threats aim to make a system or service unavailable to legitimate users.

**Examples**:

* Overloading a server with traffic (DDoS attack).
    
* Exploiting a vulnerability to crash a system.
    

**Mitigations**:

* [**AWS Shield**:](https://aws.amazon.com/shield/) Managed DDoS protection service.
    
* **AWS WAF**: Web application firewall to protect against common web exploits.
    
* [**Elastic Load Balancing (ELB)**](https://aws.amazon.com/elasticloadbalancing/): Automatically distribute incoming application traffic across multiple targets.
    
* [**Amazon CloudFront**](https://aws.amazon.com/cloudfront/): Content delivery network (CDN) to distribute content with low latency and high transfer speeds, also provides DDoS protection.
    
* **Auto Scaling**: Ensure you have the right number of Amazon EC2 instances available to handle the load for your application.
    

**6\. Elevation of Privilege**

**Description**: Elevation of privilege threats occurs when an attacker gains higher access levels than they are authorized for.

**Examples**:

* Exploiting a vulnerability to gain administrative access.
    
* Using a low-privilege account to execute commands with higher privileges.
    

**Mitigations**:

* **AWS Identity and Access Management (IAM)**: Enforce the least privilege by assigning minimal required permissions to users and roles.
    
* [**AWS Organizations**](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_introduction.html): Centrally manage and govern your environment as you grow and scale your AWS resources.
    
* [**AWS Trusted Advisor**](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/): Provide real-time guidance to help you provision your resources following AWS best practices.
    
* [**Amazon Inspector**](https://aws.amazon.com/inspector/): Automated security assessment service to help improve the security and compliance of applications deployed on AWS.
    

**SUMMARY**

It is increasingly critical that teams are more aware of the implications of their architectural decisions. Security incidents can cost organisations millions of pounds and prevention they say is better than cure. Periodic review of every system’s threat model is essential in ensuring that vulnerabilities in the system are not exploited by bad actors. By leveraging specific services provided by cloud platforms and other third parties, you can effectively mitigate the security threats identified through the STRIDE threat modelling process, ensuring a robust security posture for your applications and data.