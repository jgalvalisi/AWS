## Website Portfolio

With AWS, you can host static web pages such as, for example, a website portfolio. In this case, I will host my personal web portfolio using Amazon S3 Buckets, Amazon Route 53, and CloudFront to accomplish this goal.

### Why will we use these services?

- Amazon S3 Buckets: we will use them to host the files of our website (HTML, CSS, images, etc.)
- Amazon Route 53: to define where you want to route internet traffic for your domain (you can create your own domain within AWS or bring it from outside).
- Amazon CloudFront: we will get better performance since it will cache all the related data and improve the security of your website allowing HTTPS version.

### Amazon S3 Buckets
 
- Create two buckets: one will host all the files related to the website, and the other to redirect the request to the proper domain (the one with wwww).
- Bucket 1: Name it as your domain website without wwww, enable 'Static website hosting' within the jgalvalisi.io (en realidad wwww), and select 'https' as the main protocol.
- Bucket 2: Name it as your domain website with wwww, enable 'Redirect requests for an object' to www.jgalvalisi.io and select 'https' as the main protocol.


### Amazon Route 53

- Afterward, go to Route 53 and create two records (with and without wwww as the record name) using the 'Alias to S3 website endpoint' option. In my case, I'll use a simple routing policy and select the same region where the bucket is based on. In my case, it's based on Europe (Frankfurt) eu-central-1.
  
<img width="820" alt="Screenshot 2023-10-09 at 15 54 09" src="https://github.com/jgalvalisi/AWS/assets/97465207/d663856b-1573-449f-947c-6acd09126f2b">

- Check if your website actually works.
- If so, you will see that it's not secure, and we will use CloudFront to solve this situation to get HTTPS since Amazon S3 website endpoints do not support HTTPS or access points (we will return to Route 53 after carrying out some steps with Amazon CloudFront).

 ### Amazon CloudFront

 - Go to Certificates Manager and request public certificate
 - Include both domain names: with and without wwww
 - After that, you will find them as 'Pending validation'. To validate them, you need to create 2 new records there and check in Route 53 for these two as CNAME. You should see these Certificates as 'Issued' status (don´t forget to be on the Us-East-1, since it is the only region Cloudfront can pull from).
 - Go to CloudFront and create two distributions, including the URL that you can find in the S3 buckets of both versions, selecting 'Redirect HTTP to HTTPS' to automatically foward the request to HTTPS, and putting the corresponding CNAME considering www or not www versions.
 - In Route 53, change both records type A using the domain name you can find in CloudFront instead of pointing directly to S3.
 - Change from 'Alias to S3 website endpoint' to 'Alias to CloudFront distribution' and select also the new distribution.

After all these changes, you should see now your website with the SSL certificate that authenticates our website's identity and enables an encrypted connection!
