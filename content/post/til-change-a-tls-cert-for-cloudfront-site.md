---
title: "TIL: How to Change a TLS Certificate for a CloudFront Hosted Site"
date: 2020-04-20
categories:
- til
tags:
- til
- tls
- aws
- cloudfront
thumbnailImagePosition: left
thumbnailImage: images/chris-panas-0Yiy0XajJHQ-unsplash.jpg
---

Recently, I had to change the certificate for this site to include the naked domain (https://gidzero.com) in addition to the subdomains. The site is hosted in S3 and exposed to the internet via cloudfront with the TLS certificate provided by Amazon Certificate Manager (ACM). All of this made generating a new certificate and swapping it in pretty straight forward. Below were the steps I took:

1. Create the new certificate through Amazon certificate manager (ACM) with the relevant domains and subdomains 
    - Request a public certificate 
    - Choose validation method. Email or DNS. Email validation is probably easiest 
    - Add optional tag 
    - Review and submit request
2. Verify request through email or DNS to create the new certificate. If you went with email, you should get a mail in the inbox of the domain's registered email address
3. Copy the ARN number for the new certificate from ACM
4. Go to the cloudfront page
    - Select the site from the cloudfront distributions list 
    - Click edit 
    - Select custom certificate 
    - Paste the copied ARN number

And you're all done. The new certificate should be served immediately.