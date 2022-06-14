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

Now, application is ready to go for trial through postman


1. Establish new connection with IBM i(AS400) server

select method as POST

URL:  http://{Host}:{Port}/admin/connections/test-connection

Where Host: public Ip of EC2 instance

      port: on which application is running(ex: 8080)
	  
Set Authentication to Basic Auth with below credentials:

Username: Admin

Password: Password
  
send below content in body 

{

"endpoint":"as400.infoviewsystems.com",

"userId":"MULEDEV",

"password":"oOvb+ffEwDt2ymQSfZwQRdAMb2plY4cgaPh4mqCT+wyJnTi5uZ0XByMLfEaEsWF6Qw==",

"iasp":"",

"libraryList":"AWSDEMOS,WTF400DEV",

"secureConnection":false,

"status": "OPEN",

"licenseUrl":"file:/opt/as400-common-api/config/as400-license.lic",

"operationType":2,

"ccsid":0,

"preStartCountDataQueue":2,

"preStartCountCommand":2,

"cleanupInterval":2,

"maxConnections":5,

"maxInactivity":10,

"maxLifetime":60000,

"maxUseCount":10,

"maxUseTime":30000,

"pretestConnections":true,

"runMaintenance":false,

"threadUsed":false,

"keepalive":true,

"loginTimeOut":0,

"receiveBufferSize":1000,

"sendBufferSize":1000,

"soLinger":0,

"soTimeout":0,

"tcpNoDelay":false,


"truststorePassword":"rIVt/A36BQnchBB9V0luuVOdxxivrAEfb5nDMA75JGVhQOyTWHkOrz5qNrnv6ZIb7TE=",

"tlsIsInsecure":"false",

"tlsKeystoreConfigured":"true",

"tlsTruststoreConfigured":"true",


"s3Bucket":"as400-license-bucket-test1",

"s3Region":"us-east-2",

"s3AccessKey":"jS+6d8Q9Sx4Odnp/iBq+DfbWfIpdeOjkqXKjSrYr/7uUvDOrVxptjm6/QJHaDcouromles8abIt8QkT/",

"s3SecretKey":"SnTvKAKB2TLh/zyDFcrG68nW2h/m/42C/Zvf4as+i1jeQdeRL11mnp+boH3e9dsc1yAp9Aj556KGaEeIrr1o4DCPOfjwC3MRj2H5UjXABQc=",


"httpUrl":"murmuring-cove-76932.herokuapp.com",

"httpDirPath":"license",

"httpUsername":"admin",

"httpPassword":"urizgUbYGJKcpRkLbC3KF0N1++17FIgQlZaKjp40IYljB6eVss5ree3FLR70",


"ftpHost":"192.168.150.20",

"ftpDirPath":"abc",

"ftpUsername":"admin",

"ftpPassword":"urizgUbYGJKcpRkLbC3KF0N1++17FIgQlZaKjp40IYljB6eVss5ree3FLR70",


"filePath":"/opt/as400-common-api/config/",


"licenseFileProtocol":"FILE",

"truststoreFileProtocol":"FILE"

}

expected response:
              {
                "message": "Connection: 'test-connection' created."
              }









