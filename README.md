# Automated Static Website Deployment on AWS using Docker and CloudFormation

A fully automated, production-ready DevOps project that provisions infrastructure as code (IaC) using AWS CloudFormation, builds a containerized static website using Docker, and deploys it on an AWS EC2 instance. The project also implements real-time monitoring and alert notifications using AWS CloudWatch and Amazon SNS.

---

## Project Architecture

The architecture flow of the infrastructure is as follows:

1. Infrastructure as Code: AWS CloudFormation template provisions a secure Virtual Private Cloud (VPC) environment with an EC2 Instance, Security Groups, and IAM Roles.
2. Containerization: A static HTML/CSS website is containerized using a Dockerfile on an Nginx base image.
3. Automation/User Data: Upon EC2 boot-up, AWS User Data scripts automatically install Docker, pull the website repository, build the Docker image, and run the container on Port 80.
4. Monitoring and Alerts: AWS CloudWatch tracks CPU Utilization, and Amazon SNS triggers email notifications if thresholds are breached.

---

## Tech Stack and Tools Used

* Cloud Platform: Amazon Web Services (AWS) — EC2, VPC, CloudWatch, SNS, IAM
* Infrastructure as Code: AWS CloudFormation (YAML)
* Containerization: Docker (Nginx Base Image)
* Version Control: Git and GitHub
* Editor: Visual Studio Code

---

## Repository Structure

automated-static-website-aws/
* cloudformation/template.yaml (CloudFormation template for AWS Infrastructure)
* website/index.html (Static website homepage code)
* Dockerfile (Docker configuration to containerize the website)
* README.md (Project documentation)

---

## Deployment Steps

### 1. Prerequisites
* An active AWS Account with administrative privileges.
* AWS CLI configured or access to the AWS Management Console.
* Git installed on your local machine.

### 2. Clone the Repository
Run these commands in your local terminal:
git clone https://github.com/Puneet-Xt/static-website-using-docker-aws.git
cd static-website-using-docker-aws

### 3. Deploy Infrastructure via CloudFormation
1. Log in to the AWS Management Console.
2. Navigate to CloudFormation and click on Create stack (with new resources).
3. Select Upload a template file and upload the cloudformation/template.yaml file.
4. Enter the Stack Name (e.g., StaticWebsiteStack) and provide parameters like your Email for SNS alerts and KeyPair name.
5. Acknowledge IAM capabilities and click Submit.

### 4. Verify Docker Container Deployment
Once the CloudFormation stack status changes to CREATE_COMPLETE:
1. Go to the EC2 Dashboard and find your newly created instance.
2. Copy the Public IPv4 Address of the instance.
3. Paste the IP address into any web browser using the format: http://YOUR_EC2_PUBLIC_IP
4. You should see your custom static website running live, served through the Dockerized Nginx container!

---

## Monitoring and Alarm Testing

This setup monitors the EC2 health continuously:
* Metric: CPU Utilization greater than 80% for 5 minutes.
* Action: Triggers an Amazon SNS topic.
* Notification: Sends an immediate alert email to the subscribed user.

Note: Remember to confirm the SNS Subscription via the confirmation email received right after launching the CloudFormation stack.

---

## Resource Cleanup (To Avoid AWS Charges)

To ensure no unexpected costs are incurred under the AWS Free Tier, delete all provisioned resources when testing is completed:

1. Open the AWS CloudFormation Console.
2. Select your stack (e.g., StaticWebsiteStack).
3. Click on the Delete button at the top right.
4. CloudFormation will automatically clean up the EC2 instance, security groups, and related monitoring setups seamlessly.

---
