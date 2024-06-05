DevOps Engineering on AWS Cloud
Project: Building a Highly Available, Scalable Web Application
Group 3: Amina Merić & Selma Imširović
This project aims to plan, design, build, and deploy a web application to the AWS Cloud in line with the best practices of the AWS Well-Architected Framework.

Phase 1:
Task 1:

In the initial phase, we meticulously planned the architectural design for the infrastructure. Using the Lucid Chart tool, we created a blueprint for each subsequent phase.

Task 2:

Additionally, we estimated the costs of building the web application using the AWS Pricing Calculator. The estimated monthly cost for our infrastructure, comprising Amazon Private Cloud (VPC), Amazon RDS for MySQL, and an Amazon EC2 instance, is 55.70 USD.

Phase 2:
Task 1:

We began by creating an Amazon Virtual Private Cloud (VPC) named "amina-vpc" in the US East (N. Virginia) region. Our VPC comprises two public subnets and two private subnets, each distributed across two availability zones.

Task 2:

Following the VPC setup, we launched an Amazon EC2 instance using Ubuntu as the Amazon Machine Image (AMI) and the t2.micro instance type. The instance was configured with the previously created VPC, subnets, and security groups.

Task 3:

To install the web application and database on our EC2 instance, we executed a script (found in the helper-scripts folder). Subsequently, we successfully launched the instance.

Task 4:

Finally, we tested the deployment to ensure successful access and navigation through the application.

Phase 3:
Task 1:

We modified the inbound rules in the security group associated with the database (MySQL Aurora) to allow access from the VPC.

Task 2:

Next, we created an Amazon Relational Database using MySQL engine named “STUDENTS”. The database instance resides in the private subnets within our VPC, ensuring enhanced security.

Task 3:

We established a Cloud9 environment to run AWS Command Line Interface (CLI) commands, ensuring reliable connection and access to the RDS MySQL database.

Task 4:

Provisioned AWS Secret Manager using a script (found in the helper-scripts folder).

Task 5:

Created another EC2 instance similar to the previous one, executing a script for user data (found in the helper-scripts folder).

Task 6:

Migrated the database from the original EC2 instance to the new one created in Cloud9 using a script (found in the helper-scripts folder).

Phase 4:
In this phase, we focused on ensuring high availability and scalability by launching an Application Load Balancer.

Task 1:

We created an Application Load Balancer, configuring its settings and routing.

Task 2:

Set up the EC2 instance and auto scaling group, ensuring dynamic scaling and high availability.

Task 3:

Tested the application by performing CRUD operations.

Task 4:

Executed a script against the load balancer on Cloud9.

By completing this project, we gained practical experience across various aspects, including architecture design, cost estimation, deployment, network configuration, security measures, high availability, scalability, and access management.

Final Architectural Diagram:


Our primary focus was to achieve a comprehensive understanding and practical experience with AWS services.

