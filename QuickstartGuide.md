# Quickstart Guide

Steps to launch AMI:

1. Login to AWS account&rarr;Click on Launch instances&rarr;enter name (e.g. CommonAPI)
2. Search for “AS400” or “iSeries” or “IBM i” on AWS Marketplace and find Infoview’s AWSGateway product / AMI
3. Select AMI from marketplace & Instance type&rarr;Click on create new key pair&rarr;In security group allow access to port 8080&rarr;Finally click on launch instance

Login to created EC2 instance and run the below command to check status of application

sudo service as400-common-api-service status

If you see application is not running then run below command 

sudo service as400-common-api-service start 

Make sure application is running and check logs with below command

tail -n 200 /var/log/as400-common-api-service.log

Go for trial






