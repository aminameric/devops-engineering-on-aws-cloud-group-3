DevOps Engineering on AWS Cloud

**Project: Building a Highly Available, Scalable Web Application** Group 3: Amina Merić & Selma Imširović

The goal of this project is to plan, design, build, and deploy a web application to the AWS Cloud in a way that is consistent with best practices of the AWS Well-Architected Framework.

- *First Phase:*

**Task 1:**

Starting with the first phase, we have planned out architectural design for the infrastructure and for every next phase, we created it using the Lucid Chart tool.

**Task 2:**

Additionally we estimated the costs that we will spend building the web application using the AWS Pricing Calculator. In the AWS Pricing Calculator we added all the services that we used in our infrastructure which are Amazon Private Cloud (VPC), Amazon RDS for MySQL and the Amazon EC2 instance. At the end our estimated monthly cost is 55.70 USD.

- *Second Phase:*

**Task 1:**

In this phase, we first created an Amazon Virtual Private Cloud (VPC) named "amina-vpc" in the US East (N. Virginia) / us-east-1 region. Our VPC consists of two public subnets and two private subnets. One pair of public and private subnets (public1 and private1) is in the us-east-1a availability zone, while the other pair (public2 and private2) is in the us-east-1b availability zone.

Next, we created an internet gateway and attached it to the VPC to enable communication with the internet. Then we created a Route Table for our VPC. We

added routes to this Route Table for the internet gateway and associated the Route Table with our public subnets. To allow the private subnets to access the internet, we created a NAT Gateway in one of the public subnets and added the necessary routes to the Route Table associated with the private subnets.

After successfully creating the Route Tables, we created two Security Groups: one for the EC2 instances and the other for the database. We configured the inbound rules for these Security Groups to allow the necessary inbound traffic. With this setup, we successfully launched our VPC.

**Task 2:**

In the second task we launched an Amazon EC2 instance. For the amazon machine Image (AMI) we selected Ubuntu, and the instance type is t2.micro. For this instance we selected the VPC and subnets previously created, and attached the security groups from task one.

In order to install the web application and database on our virtual machine, we executed this script:

![](Aspose.Words.36814d73-4fa7-4ae6-9129-af1f3906b459.001.jpeg)

(Script can be found in the helper-scripts folder.)

After that we launched the instance. **Task 3:**

Last task was to actually test this deployment and to ensure that we can successfully access and navigate through it (screenshot can be seen below).

![](Aspose.Words.36814d73-4fa7-4ae6-9129-af1f3906b459.002.jpeg)

**Architectural diagram after second phase:**

![](Aspose.Words.36814d73-4fa7-4ae6-9129-af1f3906b459.003.jpeg)


- *Third phase:*

The aim of this phase is to make our application runnable on separate virtual machines. **Task 1:**

In this task we modified the inbound rules in the previously created security group that is associated with the database (MySQL Aurora) in order for the VPC to be able to access the instances of the database.

**Task 2:**

Second task was about the creation of the Amazon Relational Database using MySQL engine. The database instance is called “STUDENTS” and it resides in the private subnets within our VPC in order to ensure that it is not publicly accessible and to ensure that it is more secure.

**Task 3:**

In this task we needed to establish the Cloud9 environment in order to run AWS Command Line Interface (CLI) commands. We used the t3.micro EC2 instance which is configured with the SSH - Secure Shell access for secure and reliable connection and also our Cloud 9 environment has access to the RDS MySQL database.

**Task 4:**

With the fourth task we provisioned AWS Secret Manager. We did that by running this script:

![](Aspose.Words.36814d73-4fa7-4ae6-9129-af1f3906b459.004.png)

(Script can be found in the helper-scripts folder.) **Task 5:**

In the following we made a new EC2 instance in the same way as the previous one, only for the user data we inserted and executed the following script:

![](Aspose.Words.36814d73-4fa7-4ae6-9129-af1f3906b459.005.jpeg)

(Script can be found in the helper-scripts folder.) **Task 6:**

In this task we migrated the database from the original EC2 instance to the new one which we created in Cloud9. On the Cloud9 we run the following script:

![](Aspose.Words.36814d73-4fa7-4ae6-9129-af1f3906b459.006.png)

(Script can be found in the helper-scripts folder.)

With this we successfully migrated the database and made sure that everything works properly.

**Architectural diagram after third phase:**

![](Aspose.Words.36814d73-4fa7-4ae6-9129-af1f3906b459.007.jpeg)

- *Fourth phase*

Phase four was about ensuring the high availability and scalability. Because of that we launched the Application Load Balancer.

**Task 1:**

We created an Application Load Balancer and configured its name, schema, AZs (two availability zones: *us-east-1a* and *us-east-1b*), security settings and routing.

**Task 2:**

After creating LB, we set up the EC2 instance by creating a Launch Template, selecting the appropriate AMI and instance type, and enabling auto assigned IPv4 addresses for public access. Then we configured the auto scaling group by selecting VPC in subnets and attaching LB.

This setup ensures that our web application is publicly accessible and can dynamically scale to handle different loads, providing high availability and scalability.

**Task 3:**

We tested the application by performing some basic CRUD operations in order to see if everything works correctly and fine.

Adding the student:

![](Aspose.Words.36814d73-4fa7-4ae6-9129-af1f3906b459.008.jpeg)

![](Aspose.Words.36814d73-4fa7-4ae6-9129-af1f3906b459.009.jpeg)

Getting the student’s data:

![](Aspose.Words.36814d73-4fa7-4ae6-9129-af1f3906b459.010.jpeg)

**Task 4:**

At the end we executed the following script on Cloud9 against the load balancer:

![](Aspose.Words.36814d73-4fa7-4ae6-9129-af1f3906b459.011.png)

(Script can be found in the helper-scripts folder.)

By this we successfully completed this project that covers various aspects of architecture design, cost estimation, web application deployment, network configuration, security measure setup, high availability and scalability, and access permission management.

**Final Architectural diagram:**

![](Aspose.Words.36814d73-4fa7-4ae6-9129-af1f3906b459.012.jpeg)

The goal and sour focus was to obtain a comprehensive understanding and practical experience with AWS services.

