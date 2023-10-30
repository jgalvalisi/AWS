# Serverless Web Application on AWS

## Description:

In this project, we will build a dynamic serverless web application integrating [AWS Lambda](https://aws.amazon.com/es/lambda/), [Amazon DynamoDB](https://aws.amazon.com/es/dynamodb/), [Amazon S3](https://aws.amazon.com/es/s3/), [Amazon CloudFront](https://aws.amazon.com/es/cloudfront/), and [Amazon Route 53](https://aws.amazon.com/es/route53/) services.

What we want to accomplish at the end is to count the number of viewers our new web application has and check if it works or not using a DynamoDB table.

## Step by Step:


### ❇️  1° Phase - Create an S3 bucket to host the website

- Using Amazon S3, we will host and compile all the files related to the website, such as HTML, CSS, or JavaScript formats.
- Use the bucket name you like (I'll use serverless-web-application-on-aws-project.free.nf) and choose the region you need (in my case eu-central-1 Frankfurt).
- You can leave the rest as default settings.

<img width="1274" alt="Screenshot 2023-10-26 at 19 06 11" src="https://github.com/jgalvalisi/AWS/assets/97465207/bb8944ee-4458-48bc-8a2e-a891e2c6fdc7">
  
- Finally, upload the static files within the bucket.

<img width="1516" alt="Screenshot 2023-10-26 at 19 11 22" src="https://github.com/jgalvalisi/AWS/assets/97465207/5639ccdb-c3a7-4ff2-ad59-1d10bb42624c">


### ❇️  2° Phase - Create the CloudFront distribution

- To get low-latency of the website, we are going to settle CloudFront connected to our bucket.
- Select our S3 bucket as the origin domain.
- Select the option 'Origin access control settings (recommended)' since we did not make our S3 bucket public.
- Set the Origin access control creating a new one.
- Leave everything as default.
- After this, we need to copy our S3 bucket policy in order to attach it to our bucket.
- Under 'Origins,' select the origin name that we've created, click on 'Edit,' and copy the policy.
- Now go to your S3 bucket and select 'Permissions'. We are going to add the policy to the bucket.
- The last part of this is to select our index.html as the Default root object within the settings of the CloudFront distribution that we've created.


### ❇️  3° Phase - Route 53 in combination with CloudFront

- Register a hosted zone using Route 53. In my case, I used my test domain serverless-web-application-on-aws-project.free.nf, a personal domain that I got using InfinityFree (a hosting provider that offers free subdomains and free hosting services).
- Edit the CloudFront by changing the 'Alternate domain names' section within 'Settings.'
- Add a custom domain name using your domain (without using 'wwww', please!).
- Route your AWS URL link to your domain.


### ❇️  4° Phase - Create an AWS DynamoDB table

- Create a dynamic DynamoDB table to store the items.
- Add a table name and select 'id' as a partition key.
- Check the items that we have (we are supposed to have zero items returned).

<img width="1211" alt="Screenshot 2023-10-30 at 10 01 22" src="https://github.com/jgalvalisi/AWS/assets/97465207/ad70229b-e79c-48c5-828f-074b8101339a">

- After checking, let's create our first item, setting up id as 0 and 'views' (as the count of views of our website) as 1.

<img width="1290" alt="Screenshot 2023-10-30 at 10 04 06" src="https://github.com/jgalvalisi/AWS/assets/97465207/f7295cf4-7b85-436b-bae6-b06e785c1874">


### ❇️   5° Phase - Generate an IAM role for the new Lambda function

- We are going to use this IAM role to give permissions to allow access to our new DynamoDB table.
- Go to the IAM section and create a new AWS role to use Lambda functions.
- Filter by DynamoDB and select the following predefined IAM role: 'AmazonDynamoDBFullAccess' (remember that allowing full access is not in compliance with the Principle of least privilege, and it's not recommended for real cloud situations, but, for this case, we are going to use it with all its permissions).
- Finally, add a name and create the role! You should have it now, and you can see it within your IAM Roles list.


### ❇️   6° Phase - Design a Lambda function

- Go to AWS Lambda and create an AWS Lambda function that will persist data to an Amazon DynamoDB table.
- In my case, I'll use the same name we have been using (serverless-web-application-on-aws-project) and Python 3.8, but you can use other languages you feel comfortable with.
- Within 'Advanced settings,' allow 'Enable function URL' to assign HTTP(S) endpoints to your Lambda function.
- For this case, we'll select NONE as auth type, but it's recommended to limit access through AWS_IAM (luckily, you can change it later if you want).
- Since it is possible to access it publicly, you should see the default Lamdbda message _"Hello from Lambda!"_. When checking the function URL, you might encounter an error message like _{"Message":"Forbidden"}_, a situation that happened to me. If that's your case, you probably forgot to change the default execution role using the role that we have previously created. Select the role when creating the Lambda function, and the error will be solved. In my case, this worked.
- Create the code (in my case, with Python) to carry out the count of website viewers. In my case, the code goes as follows:

`
  
    import json
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
    
    return views

- You can split this Lambda function in two (one to GET the count and the other to UPDATE it), but I rather in this case do everything in one.    
- Now it's time to deploy our function and check if we have any errors. You can check it by clicking the Function URL and check if it's working as expected. If you refresh your website, you should see each time a new number of views!

<img width="1154" alt="Screenshot 2023-10-30 at 16 57 11" src="https://github.com/jgalvalisi/AWS/assets/97465207/12b6018a-4f2b-433c-b753-4e5e890bd94b">

- You can check the number of views also using your DynamoDB table, checking the items that it has.

<img width="973" alt="Screenshot 2023-10-30 at 16 06 46" src="https://github.com/jgalvalisi/AWS/assets/97465207/c0c3b43f-c7d6-4490-88b6-683595dc90c7">


### ❇️  7° Phase - Delete the services (in case you need it)

- In my case, I don't want to be charged for these services that I've created, so I'll proceed to delete everything with the aim of avoiding future charges.
- If you are in the same situation as me, delete your S3 Bucket, DynamoDB table, IAM role, CloudFront, DNS you indicated, and any other related resource!


## ❇️  Summary:

With this project, we created a serverless web application hosted on AWS, using AWS Lambda, DynamoDB, S3, and CloudFront, among other services.

Additionally, we obtained experience working with AWS services and integrating them to create a complete solution focused on Lambda.
