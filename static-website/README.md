Website Portfolio

With AWS you are able to host static web pages such as, for example, a website portfolio. In this case, I will host my personal webportfolio using Amazon S3 Buckets, Amazon Route 53, and CloudFront to accomplish this goal.
Why we will use these services?
Amazon S3 Buckets: we will use them to host the files of our website (HTML, CSS, images, etc.)
Amazon Route 53: to define where you want to route internet traffic for your domain (you can create your own domain within AWS or bring it from outside).
Amazon CloudFront: we will get better performance since it will cache all the data related.

Amazon S3 Buckets

- Create two different buckets: one will be used to host all the files related to the website and the other one to redirect the request to the propper domain.
- 
- Bucket 1: Name it as your domain website without wwww, enable 'Static website hosting' within the jgalvalisi.io (en realidad wwww) and select 'https' as the main protocol.
- Bucket 2: Name it as your domain website with wwww, enable 'Redirect requests for an object' to www.jgalvalisi.github.io and select 'https' as the main protocol.


Amazon Route 53

- After that, go to Route 53 and create 2 different records (with and without wwww as the record name) using the 'Alias to S3 website endpoint' option. In my case, I'll use a simple routing policy and select the same region where the bucket is based on. In my case, it's based on Europe (Frankfurt) eu-central-1.
- 
<img width="820" alt="Screenshot 2023-10-09 at 15 54 09" src="https://github.com/jgalvalisi/AWS/assets/97465207/d663856b-1573-449f-947c-6acd09126f2b">

- Check if your website actually works.
- If so, you will see that it's a not secure and we will use CloudFront to solve this situation to get HTTPS since Amazon S3 website endpoints do not support HTTPS or access points.

 Amazon CloudFront

 - Go to Certificates Manager
