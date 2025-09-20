# Basic Nginx Web Server with AWS CloudFormation

This project uses a simple AWS CloudFormation template to automatically deploy an Amazon Linux 2023 EC2 instance and install an Nginx web server.

It demonstrates a basic understanding of Infrastructure as Code (IaC) for standing up web infrastructure on AWS.

Features
- Deploys an EC2 instance (t3.micro).
- Uses the latest Amazon Linux 2023 AMI.
- Installs and enables the Nginx web server via User Data.
- Outputs the public URL of the web server after creation.

Prerequisites
Before you begin, ensure you have the following:
1. An AWS Account.
2. The AWS CLI installed and configured.
3. A pre-existing VPC, Subnet, and Security Group. The Security Group must allow inbound traffic on port 80 (HTTP).

How to Deploy

1. Update the Template: Open the `cloudformation.template` file and replace the placeholder values for `SecurityGroupIds` and `SubnetId` with your own.

2. Deploy the Stack: Run the following command from your terminal in the project directory.
   aws cloudformation create-stack \
     --stack-name my-nginx-server \
     --template-body file://cloudformation.template
   
4. Check the Status: You can check the status of your stack creation with this command. Wait for it to show CREATE_COMPLETE
   aws cloudformation describe-stacks \
    --stack-name "my-nginx-server" \
    --query "Stacks[0].StackStatus"

5. Get the URL: Once the stack is complete, the public URL will be in the "Outputs" tab in the CloudFormation console or you can retrieve it via the CLI:
   aws cloudformation describe-stacks \
    --stack-name "my-nginx-server" \
    --query "Stacks[0].Outputs[0].OutputValue"
   
