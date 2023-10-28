# Serverless Web Application on AWS

## Description:

In this project, we will build a dynamic serverless web application using [AWS Lambda] (https://aws.amazon.com/es/lambda/), [Amazon DynamoDB] (https://aws.amazon.com/es/dynamodb/), [Amazon S3] (https://aws.amazon.com/es/s3/), and [Amazon CloudFront] (https://aws.amazon.com/es/cloudfront/). The application will allow users to create, read, update, and delete (CRUD) items from a DynamoDB table.

## Step by Step:

### 1° Phase - Create an S3 bucket to host the website

- Using Amazon S3, we will host and compile all the files related to the web site such as HTML, CSS or JavaScript formats.
- Use the bucket name you like (I'll use serverless-web-application-on-aws-project) and choose the region you need (in my case eu-central-1 Frankfurt).
- You can leave the rest as default settings.
- Upload the static files within the bucket.

### 2° Phase - Create the CloudFront distribution

- To get lot-latency of the website, we are going to settle CloudFront related to our bucket.
- Select our S3 bucket as the origin domain.
- Select the option 'Origin access control settings (recommended)' since we did not make our S3 bucket as public.
- Set the Origin access control creating a new one.
- Leave everything as default.
- After this, we need to copy our S3 bucket policy in order to attach to our bucket.
- Under 'Origins', select the origin name that we've created, click on 'Edit', and copy the policy.
- Now go to your S3 bucket and select 'Permissions'. We are going to add the policy within the bucket.
- The last part of this is select our index.html as the Default root object within the settings of the CloudFront distribution that we've created.

### 3° Phase - 

- 


* Create a DynamoDB table to store the items.
* Build a Lambda function to handle the CRUD operations on the DynamoDB table.
* Use S3 to store and host the web application's static files within a bucket (HTML, CSS, and JavaScript).
* Create a CloudFront distribution to serve the S3-hosted static files with low latency.



### 4° Phase - 

### 5° Phase - 

### 6° Phase - 


## Expected Outcome:

Upon completing the project, you will have a working serverless web application hosted on AWS.
You will have hands-on experience building a serverless application using AWS Lambda, DynamoDB, S3, CloudFront.
Additionally, you will have experience working with AWS services and integrating them to create a complete solution.

This project will help you improve your skills in cloud computing, serverless architecture, and AWS services.









CHEQUEAR ESTO 

This workshop shows you how to build a dynamic, serverless web application. You'll learn how to host static web resources with Amazon S3, how to use Amazon Cognito to manage users and authentication, and how to build a RESTful API for backend processing using Amazon API Gateway, AWS Lambda and Amazon DynamoDB.

In this project, we went through how to build a dynamic, serverless web application. In detail, we will host static web resources with Amazon S3, how to use Amazon Cognito to manage users and authentication, and how to build a RESTful API for backend processing using Amazon API Gateway, AWS Lambda and Amazon DynamoDB.




create an AWS Lambda function that will persist data to an Amazon DynamoDB table.


