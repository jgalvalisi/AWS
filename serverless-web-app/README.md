# Serverless Web Application on AWS

## Description:

In this project, we will build a dynamic serverless web application integrating [AWS Lambda](https://aws.amazon.com/es/lambda/), [Amazon DynamoDB](https://aws.amazon.com/es/dynamodb/), [Amazon S3](https://aws.amazon.com/es/s3/), [Amazon CloudFront](https://aws.amazon.com/es/cloudfront/), and [Amazon Route53](https://aws.amazon.com/es/route53/). The application will allow users to create, read, update, and delete (CRUD) items from a DynamoDB table. What we want to accomplish at the end is to count the number of viewers our new website has and check if it works or not using a DynamoDB table.

## Step by Step:


### 1° Phase - Create an S3 bucket to host the website

- Using Amazon S3, we will host and compile all the files related to the web site such as HTML, CSS or JavaScript formats.
- Use the bucket name you like (I'll use serverless-web-application-on-aws-project/doingwithservicecloudproviders.free.nf) and choose the region you need (in my case eu-central-1 Frankfurt).
- You can leave the rest as default settings.
- Upload the static files within the bucket.


### 2° Phase - Create the CloudFront distribution

- To get low-latency of the website, we are going to settle CloudFront connected to our bucket.
- Select our S3 bucket as the origin domain.
- Select the option 'Origin access control settings (recommended)' since we did not make our S3 bucket as public.
- Set the Origin access control creating a new one.
- Leave everything as default.
- After this, we need to copy our S3 bucket policy in order to attach to our bucket.
- Under 'Origins', select the origin name that we've created, click on 'Edit', and copy the policy.
- Now go to your S3 bucket and select 'Permissions'. We are going to add the policy within the bucket.
- The last part of this is select our index.html as the Default root object within the settings of the CloudFront distribution that we've created.


### 3° Phase - Route53 in combination with CloudFront

- Register a hosted zone using Route53. In my case, I used my test domain doingwithservicecloudproviders.free.nf, a personal domain that I got using InfinityFree (a hosting provider offers free subdomains and free hosting services).
- Edit the CloudFront changing 'Alternate domain names' section within 'Settings'.
- Add a custom domain name using your personal domain (without using 'wwww' please!).
- Route your AWS URL link to your personal domain.


### 4° Phase - Create an AWS DynamoDB table

- Create a dynamic DynamoDB table to store the items.
- Add a table name and then select as 'id' as a partition key.
- Check the items that we have (we suppose to have zero items returned).
- After checking, lets create our first item setting up id as 0 and 'views' (as the count of views of our website) as 1.


### 5° Phase - Create an IAM role for the new Lamda function

- We are going to use this IAM role to give permissions to allow access to our new DynamoDB table.
- Go to the IAM section and create a new AWS role to using Lambda functions.
- Filter by DynamoDB and select the following predefined IAM role: 'AmazonDynamoDBFullAccess' (remember that allowing full access is not compliance with the Principle of least privilege and it's not recommended for real cloud situations, but, for this case, we are going to use it with all its permissions).
- Finally, add a name and create the role! You should have it now and you can see it within your IAM Roles list.


### 6° Phase - Create a Lambda function

- Go to AWS Lambda and create a function.
- I'll use the same name that we have been using (serverless-web-application-on-aws-project) and Pyhton 3.8 in my case, but you can use other languages.
- Within 'Advanced settings', allow 'Enable function URL' to assign HTTP(S) endpoints to your Lambda function.
- For this case, we'll select NONE as auth type, but it's recommended to limit access through AWS_IAM (luckyly you can change it later if you want).
- Since it possible to access it publicly, you should see the default Lamdbda message "Hello from Lambda!". When checking the function URL, you might encounter an error message like {"Message":"Forbidden"}, situation that happened to me. If that's your case, you probably fogot to change default execution role using the role that we have previously created. Just select the role when creating the Lambda function and the error will be solved. In my case, this worked.
- Create the code (in my case with Python) to carry out the count of viewers of the website. In my case, the code goes as follows:


`import json
import boto3

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('serverless-web-application-on-aws-project')

def lambda_handler(event, context):
    response = table.get_item(Key={
        'id':'0'
    })
    views = response['Item']['views']
    views = views + 1
    
    print(views)
    
    response = table.put_item(Item={
        'id':'0',
        'views': views
    })
    
    return views`
    

### 7° Phase - Set up the Lambda function

- 


### 8° Phase - Delete the services (in case you need it)

- In my case, I don't want to be charged for these services that I've created, so I'll proceed to delete everything with the aim of avoiding future charges.
- 




* Create a DynamoDB table to store the items.
* Build a Lambda function to handle the CRUD operations on the DynamoDB table.
* Use S3 to store and host the web application's static files within a bucket (HTML, CSS, and JavaScript).
* Create a CloudFront distribution to serve the S3-hosted static files with low latency.




## Expected Outcome:

Upon completing the project, you will have a working serverless web application hosted on AWS.
You will have hands-on experience building a serverless application using AWS Lambda, DynamoDB, S3, CloudFront.
Additionally, you will have experience working with AWS services and integrating them to create a complete solution.

This project will help you improve your skills in cloud computing, serverless architecture, and AWS services.









CHEQUEAR ESTO 

This workshop shows you how to build a dynamic, serverless web application. You'll learn how to host static web resources with Amazon S3, how to use Amazon Cognito to manage users and authentication, and how to build a RESTful API for backend processing using Amazon API Gateway, AWS Lambda and Amazon DynamoDB.

In this project, we went through how to build a dynamic, serverless web application. In detail, we will host static web resources with Amazon S3, how to use Amazon Cognito to manage users and authentication, and how to build a RESTful API for backend processing using Amazon API Gateway, AWS Lambda and Amazon DynamoDB.




create an AWS Lambda function that will persist data to an Amazon DynamoDB table.


