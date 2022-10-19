CMPE 281: cloudProject-1

University Name: San Jose State University http://www.sjsu.edu/
Course: Cloud Technologies
Professor: Sanjay Garje
Student: Ram Dara


AWS Components to be setup

EC2: Create the EC2 instance and install node js, nginx as web server. Clone the project from git repositories. Configure the nginx web server to route all /api request to node server and all other requests to react app. Create AMI of EC2 instance with the above configurations. Further EC2 instances will use this AMI when they will get spawned by Auto scaling policies.

AutoScaling Group: Configure the auto scaling policy to make the system highly-available and application that can scale to configured max instances with a desired instance of 1 and max instance of 2. You can change these configs anytime in the autoscaling policy based on the Params like CPU Util, network in out, data rates etc.

Classic Load Balancer: Load balancer transfer request in the round robin fashion to multiple EC2 instances spawned under the target groups.

S3: This will be used to store and manage the files uploaded by user. The storage of this bucket will be Standard S3.

S3 - Standard Infrequent Access: S3 allows to specify the lifecycle rules for given s3 bucket, I have configured it max duration for given objects in bucket to stay in this storage class for 75 days.

Transfer Acceleration for S3 Bucket: This allows the bucket for secure and accelerated transfer in terms of the data rates for files.

AWS Glacier for S3 bucket: Glacier storage class is the cold storage and I have configured the files to move here after 365 days.

Mysql: Create a Mysql instance for keeping track of the files uploaded by the user and their respective params like description, created and updated time etc.

CloudFront: Create a CloudFront (CDN), which will be configured for download of files and setup minimum TTL as 30 sec which will reload the cache.

Route 53: This is the Domain Name Server which is used to resolve the IP address of the application domain.

CloudWatch: This will be used to create monitoring for the auto scaling, ec2, dynamodb etc when the CPU utilization of ec2 instances will reach at high or low threshold and sends the notification via SNS.

Lambda: On any delete events in S3 bucket, it invoked the Lambda function created in nodeJS which will further invoke SNS topic to send notification via email.

SNS: It is the Simple Notification Service for AWS resources which sends email and text messages on the particular top gets the configured events.

Amazon Cognito: Create the userpool for users to sign up or sign in to the application using custom login/signup and social identity providers like google and facebook

Required Libraries:

boto3==1.17.17
Collectfast==2.2.0
Django==3.1.7
django-environ==0.4.5
psycopg2-binary==2.8.6


Architecture Diagram:

![Arch](https://user-images.githubusercontent.com/61180970/196610442-90724544-fcdc-45de-8415-042f0546d3c5.jpg)

Sign in/ Sign up 

<img width="1220" alt="Signin:Signup" src="https://user-images.githubusercontent.com/61180970/196611022-4b811ed6-d52a-434f-bdfc-e6ce0cc90ad8.png">

Login Page:

<img width="986" alt="Login Page" src="https://user-images.githubusercontent.com/61180970/196611142-df658dc4-8681-4ee3-80c4-40707c8c4a49.png">

Landing Page :

<img width="808" alt="Landing page" src="https://user-images.githubusercontent.com/61180970/196611291-ed621a1f-104c-4e6d-bfb3-21f98aa0d585.png">





