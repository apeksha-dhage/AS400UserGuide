# Quickstart Guide

## Environment Setup

1. Login to AWS account&rarr;Click on Launch instances&rarr;enter name (e.g. CommonAPI)
2. Search for “AS400” or “iSeries” or “IBM i” on AWS Marketplace and find Infoview’s AWSGateway product / AMI
3. Select AMI from marketplace & Instance type&rarr;Click on create new key pair&rarr;In security group allow access to port 8080&rarr;Finally click on launch instance
4. Verify the launched AMI is working by calling get connections API from below postman collection link

   [https://github.com/apeksha-dhage/AS400UserGuide/blob/main/Get%20Connections.postman_collection.json](https://github.com/apeksha-dhage/AS400UserGuide/blob/main/Get%20Connections.postman_collection.json)
   
   configure EC2 server public ip instead of localhost and click on send.
   
   If the response of API is empty array([]) everything is fine with AMI setup.

Here, two types of API's are there
1. Admin API
    1. Encryption API
    
        This API will allow to encrypt the sensative data like passwords and ather secrets.
	
    3. Connections API
    
        API related to Connections will help you register and establish connection with IBM i(AS400) server and you can manage all operations like UPDATE,DELETE and           GET connection.
	
    3. DataQ Poller API
    
       API related to DataQ poller will help you register and managing pollers to read data contineously from DATAQ and push to SNS topic and manage other operation          like UPDATE,DELETE and GET pollers.
       
    4. Program Call API
    
       API related to Program call will help you to register program call with applications so that it will be active before calling the functional api for program            call and manage other operations like UPDATE,DELETE and GET program call. 
       
  There is a feature called Authentication so while accessing Admin related API's through postman client before calling API, please select Aunthentication as a 
  "Basic Auth" then it will ask for credentials i.e Username and Password provide below credentials.
  
  Username = Admin
  
  Password = Password
  
  Please refer the screenshot.
  
  ![image](https://user-images.githubusercontent.com/46368616/174233236-158b6ee1-7e99-4d0a-a115-239e09759fac.png)

  
  
3. functional API

   As a part of functional call API, provided four API to get result from IBM i(AS400) server.
   
   1. Execute Command Call API
   3. Publish Data To DATAQ API
   4. Execute Program CAll API
   5. Read Data From DATAQ API
   
  To access functional API through postman client select Authentication as "Basic Auth" and provide below credentials.
  
  Username = User
  
  Password = Password@123
  
  please refer screenshot
  
  ![image](https://user-images.githubusercontent.com/46368616/174233363-371e6141-dc64-4cf9-916b-221526e7f716.png)


## API Test

IN this section test the API one by one.

1. Before establishing the connection with IBM I(AS400) server go for encryption which will help to secure data that is passwords and other secrets.
   this connector apploication will provide the feature called encryption and there is a API called to encrypt the password and other secret.
   please  refre the screenshot.
   
   ![image](https://user-images.githubusercontent.com/46368616/174231414-a30f82d7-79f5-4e90-8515-dd3a005731eb.png)

   
   
1. Configuring new IBM i(AS400) connection

 Call create connection api provided to establish the connection with IBM i(AS400) server.
 refer the below screenshot to configure connection. for requst body refer the swagger documentation link which is given below
 
 ![image](https://user-images.githubusercontent.com/46368616/174233922-e532c674-8ccc-4a3e-ad9c-1423e305adba.png)



3. Validate the connection is created or not

  Call get all connection api it will hep to confom connection is created or not, if created response will be array of objects(i.e [{}]) otherwise it will give 
  empty array(i.e []). Plaese refer the below screenshot. to see complete response content please refer the swagger documentaion link which is given below
  
  ![image](https://user-images.githubusercontent.com/46368616/174234062-8fc6b433-6a28-430a-8cbf-7f6c61ea345b.png)

  
  

















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


