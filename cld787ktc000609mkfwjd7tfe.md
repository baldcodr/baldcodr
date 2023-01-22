# Deploying a React Application using GitHub, AWS Amplify and S3

A few years ago, I built a front-end web app with React and deployed it to AWS Amplify. I thought it would be nice to document my process for deploying the application and to show how easy it is to deploy your apps in a matter of minutes using AWS Amplify. Amplify allows you to connect your frontend project hosted on a code repository like GitHub and handles the build process for your web app. The video on the homepage and image files are hosted on Amazon S3.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674382359080/d9110dd4-af0e-4671-af57-874a1087a77a.jpeg align="center")

What is AWS Amplify?

AWS Amplify is a set of tools and services provided by Amazon Web Services (AWS) that allows developers to easily create, deploy, and manage web and mobile applications. It includes a variety of features such as authentication, storage, hosting, and analytics, as well as a command line interface (CLI) and a JavaScript library for building user interfaces. Amplify also integrates with other AWS services such as AWS AppSync, AWS Lambda, and AWS Cognito, making it a powerful tool for building scalable and secure applications.

Steps to deploy a React web application to AWS Amplify:

1. Log in to the AWS Management Console and navigate to the Amplify console.
    
2. Click on the "Get Started" button to create a new web app.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674380776846/e5c1ed7d-68f8-4a83-bbbb-656e462ea789.png align="center")
    
3. Select "GitHub" as the source provider and authorize the connection to your GitHub repository.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674380814097/88864db6-4368-4451-b147-62304dc1f91a.png align="center")
    
4. Select the repository that contains your React application and configure the build settings, such as the build command and output directory.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674380932481/ea494ee9-1d29-4457-b40a-52b9ef217d18.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674381040556/c5f1a526-7444-4ab8-9638-c97cbbe0a31a.png align="center")
    
5. Click on the "Save and Deploy" button to start the build and deployment process.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674381100207/ca1d6337-ba11-454c-ac67-02bfd1fe180f.png align="center")
    
6. Once the deployment is complete, you will see the URL of your deployed application in the Amplify console.
    
7. You can also set up a custom domain for your application by clicking on the "Domain" tab in the Amplify console.
    
8. To test the application, visit the URL or custom domain in a web browser.
    
9. To make changes to your application, simply push updates to your GitHub repository and Amplify will automatically build and deploy the changes.
    

Here is the final result of the web application we have deployed with interesting web and mobile views [https://master.d2rh789rxw04r.amplifyapp.com/](https://master.d2rh789rxw04r.amplifyapp.com/)

NB: Best viewed on a desktop/large screen.