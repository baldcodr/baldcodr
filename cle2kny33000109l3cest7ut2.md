# Deploying a fully Serverless Web Application
with Lambda, API Gateway, Amplify, DynamoDB, and Cognito on AWS

A serverless web application architecture is a software architecture in which an application is created without requiring a server or server infrastructure to run it. Instead, it uses third-party and cloud-based services to manage the infrastructure and supply the computational power needed to execute the application.

At the end of this article, there is a hands-on project for you to deploy your first serverless application. Read on to see why this is the best time to learn serverless application deployment in the cloud.

AWS offers a plethora of services for deploying serverless web applications. A serverless web architecture is made up of the following components:

1. Frontend: AWS Amplify is a service for building the frontend using HTML, CSS and Javascript. With AWS Code Commit or Guthub as your repository and linked to your amplify project, you can quickly rebuild and redeploy your web application anytime there is a new change in your code.
    
2. Authentication and authorisation using Amazon Cognito. It also offers federated authentication and access using Google, Facebook and other similar services to access AWS resources.
    
3. Database: DynamoDB is a serverless database service on AWS
    
4. Routing: API Gateway for routing requests to the backend and returning responses to the frontend. This acts as a single entry point for all requests from the frontend of the application.
    
5. AWS Lambda: serves as the backend for handling the web application logic and acts as the core of the web application.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676277888244/000da390-1732-4be1-9740-de89376472fe.jpeg align="center")

Fig 1: A Serverless Web Architecture on AWS Cloud

You might wonder, why even bother about serverless or using serverless architecture for your web application? Stay with me, in a few minutes, you will understand WHY.

The speed required to innovate is rapidly evolving, and organisations are always seeking better ways to meet the needs of their customers by outsourcing server administration and management while reducing costs.

Serverless Architecture offers this capability as highlighted below:

**Cost Savings:** One of the biggest advantages of serverless architecture is cost savings. Since the cloud provider manages the underlying infrastructure, you only pay for the resources you use, which can result in lower overall costs compared to traditional server-based infrastructure.

**Scalability:** Serverless architecture is highly scalable, meaning it can automatically handle spikes in traffic without any manual intervention. The cloud provider manages the scaling of the underlying infrastructure, so you don’t have to worry about provisioning additional servers or managing the load balancing of your application.

**Flexibility:** Serverless architecture provides a high level of flexibility, allowing you to build and deploy applications quickly and easily. You can build and deploy individual functions or microservices as needed, resulting in faster development cycles and more frequent releases.

**Ease of Deployment and Management:** Serverless architecture eliminates the need to manage servers, so you can focus on developing and deploying your application. The cloud provider handles the deployment and management of the underlying infrastructure, so you don’t have to worry about hardware or software maintenance.

Serverless architecture is becoming increasingly popular and is a good choice for many applications due to its cost savings, scalability, and ease of deployment and management.

**Hands-on lab:**

[https://aws.amazon.com/getting-started/hands-on/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/](https://aws.amazon.com/getting-started/hands-on/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/)