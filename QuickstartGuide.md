# Quickstart Guide

## Environment Setup

1. Login to AWS account&rarr;Click on Launch instances&rarr;enter name (e.g. CommonAPI)
2. Search for “AS400” or “iSeries” or “IBM i” on AWS Marketplace and find Infoview’s AWSGateway product / AMI
3. Select AMI from marketplace & Instance type&rarr;Click on create new key pair&rarr;In security group allow access to port 8080&rarr;Finally click on launch instance
4. Login to created EC2 instance and run the below command to check status of application

     sudo service as400-common-api-service status

5. If you see application is not running then run below command 

     sudo service as400-common-api-service start 

6. Make sure application is running and check logs with below command

     tail -n 200 /var/log/as400-common-api-service.log
     
 
## API Test

Now, application is ready to go for trial through postman

Please refer the above atached link for postman collection to test API's

1. Before creating connections require to encrypt the passwords using Encryption API.
2. Establish new connection with IBM i(AS400) server using create connection API from postman collection.
3. Make sure the connection created and started using Get All Connection API.
4. Before calling program for IBM i(AS400) It shoud be ready to call use Register Program Call API and register program.
5. Validate the program is ready or not using Get All Registered Program API if you see that program in response, now we are ready to call functional API.
6. Now call the program to add record entry in IBM i(AS400) using Execute program Call API from functional resources.
7. To poll data from dataQ contineously requires active pollers which will listen dataQ contineously and send notifications to SNS topic
   register and start poller using Register Dq Poller API 
8. Publish some data to dataQ by using Publish message into data queue API 
   ex. {
	"dataQueueEntry": "Hiiiiiii"
      }
9. If you subscribe the SNS topic using any of the client ex. Lamda, email,SQS ... will be able to see publish messages 


