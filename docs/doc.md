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


**Task 3:**

To install the web application and database on our EC2 instance, we executed a script (found in the helper-scripts folder). Subsequently, we successfully launched the instance.

**Task 4:**

Finally, we tested the deployment to ensure successful access and navigation through the application.

### Phase 3:

**Task 1:**

We modified the inbound rules in the security group associated with the database (MySQL Aurora) to allow access from the VPC.

**Task 2:**

Next, we created an Amazon Relational Database using MySQL engine named “STUDENTS”. The database instance resides in the private subnets within our VPC, ensuring enhanced security.

**Task 3:**

We established a Cloud9 environment to run AWS Command Line Interface (CLI) commands, ensuring reliable connection and access to the RDS MySQL database.

**Task 4:**

Provisioned AWS Secret Manager using a script (found in the helper-scripts folder).

**Task 5:**

Created another EC2 instance similar to the previous one, executing a script for user data (found in the helper-scripts folder).

**Task 6:**

Migrated the database from the original EC2 instance to the new one created in Cloud9 using a script (found in the helper-scripts folder).

### Phase 4:

In this phase, we focused on ensuring high availability and scalability by launching an Application Load Balancer.

**Task 1:**

We created an Application Load Balancer, configuring its settings and routing.

**Task 2:**

Set up the EC2 instance and auto scaling group, ensuring dynamic scaling and high availability.

**Task 3:**

Tested the application by performing CRUD operations.

**Task 4:**

Executed a script against the load balancer on Cloud9.

By completing this project, we gained practical experience across various aspects, including architecture design, cost estimation, deployment, network configuration, security measures, high availability, scalability, and access management.

## Final Architectural Diagram:

![Final Architectural Diagram](Aspose.Words.36814d73-4fa7-4ae6-9129-af1f3906b459.012.jpeg)

Our primary focus was to achieve a comprehensive understanding and practical experience with AWS services.
