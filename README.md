# Imran_Challenge
Challenge for SecNet

The following deploys a static webpage using sample HTML text.  


## General Notes

Deploying the website can be completed in a multitude of ways, such as via. a web server, Containerization, as well as with Lambda/ Serverless Application Model.  This is just one approach, which uses S3 and CloudFront as it is a simpler design and allows for easier management of the deployment and utilizes more PaaS services as opposed to self-managed resources.  

## Housing the Code

Website hosting can be completed for a static website via. a Amazon S3 bucket.  This public bucket houses all the HTML code needed in order to deliver the website as well as the error pages if applicable.  S3 buckets will also have Bucket Policies which indicate what type of access if any are allowed onto the bucket. 

## Delivering the Website

Once the website has been uploaded to S3, the website can be delivered via. a CDN (content delivery network) to the public.  This allows for the S3 bucket to remain secure while at the same time increasing the scalability of the site.  Each edge location of the CDN will have a copy of the website, increasing speed and decreasing the number of requests made directly to the S3 bucket (although this site is quite simple, the underlying concept is important to maintain). CloudFront is also configured to ONLY accept HTTPS requests.  

## Routing the Public

Amazon Route 53 is used here in order to route the traffic to the CloudFront Distribution.  It contains A records that resolve for both the domain name itself as well as the 'www' version of the domain.  NOTE: Domain must be purchased through Route 53 for this solution to work, otherwise special record sets must be deployed in order to address routing challenges from 3rd Party DNS services. Users can reach the website by going to "example.com" and hitting the underlying CF Distribution as it is directed to the underlying AWS resources via. RT 53. 

## Certificates

SSL Certs are provisioned through ACM (Amazon Certificate Manager) and assigned directly to the CloudFront Distribution.  This allows for the traffic to all traverse via. HTTPS instead of HHTP. 

## Logging 

A separate S3 bucket will also be provisioned to serve as the collector for logs.  CloudFront as well as the Root S3 Bucket have been configured to add logs to the Logging Bucket, each with its own headers so the origin of the log can be distinguished.  Log analytics tools can be deployed to read from this bucket (not added as part of this example)


## Python Challenge

In this repo is also the solution to the Complex Number challenge as presented.  It is writen in Python3.


#
