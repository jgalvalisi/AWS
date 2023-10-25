## Building a Serverless Application

In this project, we went through how to build a dynamic, serverless web application. In detail, we will host static web resources with Amazon S3, how to use Amazon Cognito to manage users and authentication, and how to build a RESTful API for backend processing using Amazon API Gateway, AWS Lambda and Amazon DynamoDB.








Utilizing AWS, you have the capability to host static web pages, such as a website portfolio. In this instance, I will host my personal web portfolio using Amazon S3 Buckets, Amazon Route 53, and CloudFront to achieve this objective (www.jgalvalisi.com)

### Why will we use these services?

- Amazon S3 Buckets: We will use these to host our website's files (HTML, CSS, images, etc.).
- Amazon Route 53: This service defines where you want to direct internet traffic for your domain (you can either create your own domain within AWS or import it from an external source).
- Amazon CloudFront: This will enhance performance by caching related data and bolstering website security by allowing an HTTPS version.
Amazon S3 Buckets.

### Amazon S3 Buckets
 
- Create two buckets: one to host all website-related files and another to redirect requests to the proper domain (the one without "www").
- Bucket 1: Name it after your domain without 'www', enable 'Static website hosting' within jgalvalisi.com (actually "www"), and select 'https' as the primary protocol.
- Bucket 2: Name it after your domain with 'www', enable 'Redirect requests for an object' to www.jgalvalisi.com, and select 'https' as the primary protocol.
Amazon Route 53

### Amazon Route 53

- Next, navigate to Route 53 and create two records (with and without "www" as the record name) using the 'Alias to S3 website endpoint' option. In my case, I'll use a simple routing policy and select the same region where the bucket is located, which is Europe (Frankfurt) eu-central-1 in my case.
- Verify that your website is functioning properly.
- If it is, you'll notice that it's not secure. We'll address this by utilizing CloudFront to secure the website with HTTPS, as Amazon S3 website endpoints do not support HTTPS or access points. We will revisit Route 53 after implementing specific steps with Amazon CloudFront.
Amazon CloudFront

 ### Amazon CloudFront

 - Go to Certificates Manager and request public certificate
 - Include both domain names: with and without 'www'
 - After that, you will find them as 'Pending validation'. To validate them, you have to create two new records there and check in Route 53 for these two as CNAME. You should see these Certificates as 'Issued' status (don´t forget to be on the Us-East-1, since it is the only region Cloudfront can pull from).
 - Go to CloudFront and create two distributions, including the URL that you can find in the S3 buckets of both versions, selecting 'Redirect HTTP to HTTPS' to automatically forward the request to HTTPS, and putting the corresponding CNAME considering www or not www versions.
 - In Route 53, change both records type A using the domain name you can find in CloudFront instead of pointing directly to S3.
 - Change from 'Alias to S3 website endpoint' to 'Alias to CloudFront distribution' and select also the new distribution.

 - Proceed to Certificates Manager and request a public certificate.
- Include both domain names: with and without 'www'.
- Following that, you'll find them listed as 'Pending validation.' To complete the validation, create two new records and verify them in Route 53 as CNAME records. 
- You should see these certificates with an 'Issued' status. Don't forget to be in the us-east-1 region, as it's the only region CloudFront can pull from.
- In CloudFront, create two distributions, incorporating the URLs found in the S3 buckets of both versions. Select 'Redirect HTTP to HTTPS' to automatically redirect requests to HTTPS, and specify the corresponding CNAME, considering the 'www' or non-'www' versions.
- In Route 53, modify both A record types using the domain name from CloudFront instead of directly pointing to S3.
- Change from 'Alias to S3 website endpoint' to 'Alias to CloudFront distribution', and also select the new distribution.

After implementing all these modifications, you should now see your website with an SSL certificate that authenticates our website's identity and enables an encrypted connection!

