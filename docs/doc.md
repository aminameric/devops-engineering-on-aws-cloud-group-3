# DevOps Engineering on AWS Cloud

## Project: Building a Highly Available, Scalable Web Application
### Group 3: Amina Merić & Selma Imširović

This project aims to plan, design, build, and deploy a web application to the AWS Cloud in line with the best practices of the AWS Well-Architected Framework.

### Phase 1:

**Task 1:**
Starting with the first phase, we have planned out architectural design for the infrastructure and for every next phase, we created it using the Lucid Chart tool.

**Task 2:**
Additionally we estimated the costs that we will spend building the web application using the AWS Pricing Calculator. In the AWS Pricing Calculator we added all the services that we used in our infrastructure which are Amazon Private Cloud (VPC), Amazon RDS for MySQL and the Amazon EC2 instance. At the end our estimated monthly cost is 55.70 USD.

### Phase 2:

**Task 1:**
In this phase, we first created an Amazon Virtual Private Cloud (VPC) named "amina-vpc" in the US East (N. Virginia) / us-east-1 region. Our VPC consists of two public subnets and two private subnets. One pair of public and private subnets (public1 and private1) is in the us-east-1a availability zone, while the other pair (public2 and private2) is in the us-east-1b availability zone.

Next, we created an internet gateway and attached it to the VPC to enable communication with the internet. Then we created a Route Table for our VPC. We added routes to this Route Table for the internet gateway and associated the Route Table with our public subnets. To allow the private subnets to access the internet, we created a NAT Gateway in one of the public subnets and added the necessary routes to the Route Table associated with the private subnets.

After successfully creating the Route Tables, we created two Security Groups: one for the EC2 instances and the other for the database. We configured the inbound rules for these Security Groups to allow the necessary inbound traffic. With this setup, we successfully launched our VPC.

**Task 2:**
In the second task we launched an Amazon EC2 instance. For the amazon machine Image (AMI) we selected Ubuntu, and the instance type is t2.micro. For this instance we selected the VPC and subnets previously created, and attached the security groups from task one. 

In order to install the web application and database on our virtual machine, we executed this script:

![clipboard_image_9315ecfceb817c23](https://github.com/aminameric/devops-engineering-on-aws-cloud-group-3/assets/116023819/2eb465bd-7033-4e86-8ce2-8c39a3ec06b3)
(Script can be found in the helper-scripts folder.)

After that we launched the instance. 
**Task 3:**

Last task was to actually test this deployment and to ensure that we can successfully access and navigate through it (screenshot can be seen below).

![Screenshot_20240604_035600](https://github.com/aminameric/devops-engineering-on-aws-cloud-group-3/assets/116023819/526bfb11-7076-471f-bcc9-1c9bac3db051)

## Architectural diagram after second phase:
![Cloud Architecture](https://github.com/aminameric/devops-engineering-on-aws-cloud-group-3/assets/116023819/02b98b5b-e5f3-4460-a311-36fda9e2046f)

### Phase 3:

The aim of this phase is to make our application runnable on separate virtual machines.

**Task 1:**

In this task we modified the inbound rules in the previously created security group that is associated with the database (MySQL Aurora) in order for the VPC to be able to access the instances of the database. 

**Task 2:**

Second task was about the creation of the Amazon Relational Database using MySQL engine. The database instance is called “STUDENTS” and it resides in the private subnets within our VPC in order to ensure that it is not publicly accessible and to ensure that it is more secure. 

**Task 3:**

In this task we needed to establish the Cloud9 environment in order to run AWS Command Line Interface (CLI) commands. We used the t3.micro EC2 instance which is configured with the SSH - Secure Shell access for secure and reliable connection and also our Cloud 9 environment has access to the RDS MySQL database.

**Task 4:**

With the fourth task we provisioned AWS Secret Manager. We did that by running this script: 
![clipboard_image_27834e1ab6bae19c](https://github.com/aminameric/devops-engineering-on-aws-cloud-group-3/assets/116023819/1a5edcba-9b47-4dd0-b391-67fb27562be6)

(Script can be found in the helper-scripts folder.)

**Task 5:**

In the following we made a new EC2 instance in the same way as the previous one, only for the user data we inserted and executed the following script:

![clipboard_image_82a3d604bdd1075d](https://github.com/aminameric/devops-engineering-on-aws-cloud-group-3/assets/116023819/04947ac0-a97d-4ea6-9485-00970a58516e)

(Script can be found in the helper-scripts folder.)

**Task 6:**

In this task we migrate the database from the original EC2 instance to the new one which we created in Cloud9. On the Cloud9 we run the following script:

![clipboard_image_36ec69dbdddf5183](https://github.com/aminameric/devops-engineering-on-aws-cloud-group-3/assets/116023819/3ac6d8eb-46bd-48ae-9c76-479a429203c6)

(Script can be found in the helper-scripts folder.)

With this we successfully migrated the database and made sure that everything works properly.

## Architectural diagram after third phase:

![Cloud Architecture (3)](https://github.com/aminameric/devops-engineering-on-aws-cloud-group-3/assets/116023819/e935354b-5b5a-435f-8564-58ad2f63d926)

### Phase 4:

Phase four was about ensuring the high availability and scalability. Because of that we launched the Application Load Balancer.

**Task 1:**

We created an Application Load Balancer and configured its name, schema, AZs (two availability zones: us-east-1a and us-east-1b), security settings and routing. 

**Task 2:**

After creating LB, we set up the EC2 instance by creating a Launch Template, selecting the appropriate AMI and instance type, and enabling auto assigned IPv4 addresses for public access. Then we configured the auto scaling group by selecting VPC in subnets and attaching LB.

This setup ensures that our web application is publicly accessible and can dynamically scale to handle different loads, providing high availability and scalability.

**Task 3:**

We tested the application by performing some basic CRUD operations in order to see if everything works correctly and fine.

Adding the student:
![Screenshot_20240604_035626](https://github.com/aminameric/devops-engineering-on-aws-cloud-group-3/assets/116023819/be470751-398f-4c8e-91c7-fabcf2a5275f)

![Screenshot_20240604_035639](https://github.com/aminameric/devops-engineering-on-aws-cloud-group-3/assets/116023819/ac8a5252-9451-4fb2-9193-a2460672e16e)

Getting the student’s data:
![Screenshot_20240604_035549](https://github.com/aminameric/devops-engineering-on-aws-cloud-group-3/assets/116023819/7a5bea49-975b-45d1-ac22-ed0268eeccab)

**Task 4:**

At the end we executed the following script on Cloud9 against the load balancer:
![clipboard_image_749909ee90f67530](https://github.com/aminameric/devops-engineering-on-aws-cloud-group-3/assets/116023819/afb9cbc7-f1f7-4da5-a209-b535a0e7a42a)

(Script can be found in the helper-scripts folder.)

By this we successfully completed this project that covers various aspects of architecture design, cost estimation, web application deployment, network configuration, security measure setup, high availability and scalability, and access permission management.

## Final Architectural Diagram:
![Cloud Architecture (2)](https://github.com/aminameric/devops-engineering-on-aws-cloud-group-3/assets/116023819/8b516a98-f9cf-499f-8f3c-3da98115ab51)

The goal and sour focus was to obtain a comprehensive understanding and practical experience with AWS services

