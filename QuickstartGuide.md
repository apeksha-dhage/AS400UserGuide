# Quickstart Guide

## Environment Setup

1. Login to AWS account&rarr;Click on "Launch Instances"&rarr;enter name (e.g. CommonAPI)
2. Search for “AS400” or “iSeries” or “IBM i” on AWS Marketplace and find Infoview’s AWSGateway product / AMI
3. Select AMI from marketplace & Instance type&rarr;Click on create new key pair&rarr;In security group allow access to port 8080&rarr;Finally click on launch instance
4. Verify the launched AMI is working by calling get connections API from below postman collection link

   [https://github.com/apeksha-dhage/AS400UserGuide/blob/main/Get%20Connections.postman_collection.json](https://github.com/apeksha-dhage/AS400UserGuide/blob/main/Get%20Connections.postman_collection.json)
   
   configure EC2 server public ip instead of localhost and click on send.
   
   If the response of API is empty array([]) everything is fine with AMI setup.

Here, two types of API's are there
1. Admin API
    1. Encryption API
    
        This API will allow to encrypt the sensative data like passwords and other secrets.
	
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

  
  2. functional API

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

IBM i Prerequisites

- IBM i OS version:V5R4 and higher
- AWS VPC where the AMI is running must be able to reach the IBM i servers on ports 446, 449, 8470, 8472,8473,8475 and 8476 for non-SSL communications, and ports 448, 449, 9470, 9472, 9473, 9475 and 9476 accessible for SSL communications.
- IBM i must have **\*CENTRAL, \*DTAQ, \*RMTCMD, \*SIGNON and \*SRVMAP** host servers running in the QSYSWRK subsystem
- If secure TLS connection is used, the TLS certificate must be applied to Central, Data Queue, Remote Command, File, Signon, and DDM / DRDA services in Digital Certificate Manager
- IBM i user ID must be authorized to perform the operations on the intended IBM i objects
- If there&#39;s an additional security software that locks down the remote execution functionality, the IBM i user ID defined for connector configuration must be allowed to execute remote calls and access database, IFS and DDM services

 Call create connection api provided to establish the connection with IBM i(AS400) server.
 refer the below screenshot to configure connection. for requst body refer the swagger documentation link which is given below
 
 ![image](https://user-images.githubusercontent.com/46368616/174233922-e532c674-8ccc-4a3e-ad9c-1423e305adba.png)
 
 if secureConnection property set as true then below are the mandatory cofiguration needs to be provided and truststore file related information as well, refer from     below license management section
 
 "truststorePassword":"rIVt/A36BQnchBB9V0luuVOdxxivrAEfb5nDMA75JGVhQOyTWHkOrz5qNrnv6ZIb7TE="
 
 "tlsIsInsecure":"false"
 
 "tlsKeystoreConfigured":"true"
 
 "tlsTruststoreConfigured":"true"
 
 **License Management:**

IBM i connector will allow users to access API's only for first 15 minutes from the AMI launch. 
The IBM i connector requires a license file &quot;as400-license.lic&quot; from Infoview to enable access to specific IBM i system(s). 
please conctact to infoview systems Inc.


Managing license in different ways by using different protocols such as S3, HTTP/HTTPS, FTP, FILE, SMB etc. and accessing it through these protocols in application needs to be configure required properties while creating connection with IBM i server.

Available Protocols to load license file/truststore file (HTTP,HTTPS, FTP, SMB, S3, FILE, CLASSPATH)

what protocol used to load license file/truststore file that need to be configured with create connection api as a request body.

ex. licenseFileProtocol=S3

Truststore file is used to establish the secure connection with IBM i AS400 system. if secure connection property set as true then needs to be configure truststore file prococol.

ex. truststoreFileProtocol=S3

If we set licenseFileProtocol and truststoreFileProtocol to S3 then needs to send S3 related properties as shown in below table and in the same way for others.
Following table contains the properties related to protocols requires to be configure:

| **#** | **Protocol Name** | **Properties** |
| --- | --- | --- |
| 1 | S3 | s3.bucket=path-to-bucket<br>s3.region=us-east-2<br>s3.accessKey=access-key<br>s3.secretKey=secret-key|
| 2 | HTTP/HTTPS | http.url=url-URL<br>http.dir.path=license-file-path<br>http.username=username</br>http.password=encrypted-pwd
| 3 | FTP | ftp.host=ftp-host<br>ftp.dir.path=path<br>ftp.username=username<br>ftp.password=encrypted-pwd
| 4 | FILE/SMB | file.Path=path-to-license-file|

3. Validate the connection is created or not

  Call get all connection api it will hep to confom connection is created or not, if created response will be array of objects(i.e [{}]) otherwise it will give 
  empty array(i.e []). Plaese refer the below screenshot. to see complete response content please refer the swagger documentaion link which is given below
  
  ![image](https://user-images.githubusercontent.com/46368616/174234062-8fc6b433-6a28-430a-8cbf-7f6c61ea345b.png)

  
 4. Register the program call through Admin API
    Frist admin will register the program call through register program call api so that program will be active.
    please refer the below screenshot.For requst body refer swagger documentation link which is given below.
    
    ![image](https://user-images.githubusercontent.com/46368616/174235493-46b741b8-56ff-4ffe-b03d-180afdd59190.png)

    
  5. Call Program call functional API 
   
   In previous step program has been already register if wants to conform call get all program admin api
   please refer the below screenshot.
   
   ![image](https://user-images.githubusercontent.com/46368616/174235989-4fbcf89c-6c1c-46a9-b01f-e54dc705af69.png)
   
   
   if response looks like the above screenshot response body,considering as program is in active state
   
   Now, call the program call functional API, It will execute program in IBM i(AS400) server and return response back.
   
   please refer the below screenshot.
   
   ![image](https://user-images.githubusercontent.com/46368616/174236761-add4c6a3-c1ec-48b2-a527-892ee5a52867.png)
   
   
  6. Register Poller through admin poller API
  
  Before publishing data to DATAQ will start poller to poll/listen DATAQ contineously amd send that data to SNS topic.
  to register and start poller call admin api it will register and start polling as well.
  please refer the below screenshot.
  
  ![image](https://user-images.githubusercontent.com/46368616/174238642-0b2688ff-bfbd-4347-afca-91607b8b36b7.png)
  
 Validate once the poller has been registered or not using get All registered poller admin api.
 please refer the screenshot.
 
 ![image](https://user-images.githubusercontent.com/46368616/174239084-e6f4e430-bcba-4556-9231-7a226a6a22af.png)


  Observe the response body from from above screenshot showing status as active.
  
  7. Publish data to DATAQ
  Call functional API to publish data to DATAQ so that already register poller for same DATAq will listen it contineously.
  Please refer ther screenshot.
  
  ![image](https://user-images.githubusercontent.com/46368616/174239819-2defb71d-d27e-4b28-a748-4c33c3693b04.png)


  8.SNS topic Subscription
  
  Able to see latest published data retrieved from DATAQ in any subscribe channel.
  
  ![image](https://user-images.githubusercontent.com/46368616/174241965-e2caf8ba-063e-46d3-9624-a36750fa43cc.png)






















