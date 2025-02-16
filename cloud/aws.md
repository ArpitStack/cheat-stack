# AWS CLI Commands CheatSheet

A comprehensive guide covering essential AWS CLI commands for managing various AWS services.

## Table of Contents

- [S3 (Simple Storage Service)](#s3-simple-storage-service)
- [EC2 (Elastic Compute Cloud)](#ec2-elastic-compute-cloud)
- [IAM (Identity & Access Management)](#iam-identity--access-management)
- [RDS (Relational Database Service)](#rds-relational-database-service)
- [Lambda](#lambda)
- [CloudWatch](#cloudwatch)
- [VPC (Virtual Private Cloud)](#vpc-virtual-private-cloud)
- [ECS (Elastic Container Service)](#ecs-elastic-container-service)
- [EKS (Elastic Kubernetes Service)](#eks-elastic-kubernetes-service)
- [SQS (Simple Queue Service)](#sqs-simple-queue-service)
- [SNS (Simple Notification Service)](#sns-simple-notification-service)
- [CloudFormation](#cloudformation)

## S3 (Simple Storage Service)

List all S3 buckets:

```bash
aws s3 ls
```

Create a new bucket:

```bash
aws s3 mb s3://my-new-bucket
```

Upload a file to S3:

```bash
aws s3 cp myfile.txt s3://my-bucket/
```

Download a file from S3:

```bash
aws s3 cp s3://my-bucket/myfile.txt ./
```

Delete a file from S3:

```bash
aws s3 rm s3://my-bucket/myfile.txt
```

## EC2 (Elastic Compute Cloud)

List all EC2 instances:

```bash
aws ec2 describe-instances
```

Start an EC2 instance:

```bash
aws ec2 start-instances --instance-ids i-1234567890abcdef0
```

Stop an EC2 instance:

```bash
aws ec2 stop-instances --instance-ids i-1234567890abcdef0
```

Terminate an EC2 instance:

```bash
aws ec2 terminate-instances --instance-ids i-1234567890abcdef0
```

## IAM (Identity & Access Management)

List all IAM users:

```bash
aws iam list-users
```

Create a new IAM user:

```bash
aws iam create-user --user-name my-user
```

Attach a policy to a user:

```bash
aws iam attach-user-policy --user-name my-user --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess
```

## RDS (Relational Database Service)

List all RDS instances:

```bash
aws rds describe-db-instances
```

Create a new RDS instance:

```bash
aws rds create-db-instance --db-instance-identifier mydb --allocated-storage 20 --db-instance-class db.t2.micro --engine mysql --master-username admin --master-user-password mypassword
```

Delete an RDS instance:

```bash
aws rds delete-db-instance --db-instance-identifier mydb --skip-final-snapshot
```

## Lambda

List all Lambda functions:

```bash
aws lambda list-functions
```

Invoke a Lambda function:

```bash
aws lambda invoke --function-name my-function output.json
```

Delete a Lambda function:
```bash
aws lambda delete-function --function-name my-function
```

## CloudWatch

List all CloudWatch log groups:

```bash
aws logs describe-log-groups
```

Get logs from a specific log stream:

```bash
aws logs get-log-events --log-group-name my-log-group --log-stream-name my-log-stream
```

## VPC (Virtual Private Cloud)

List all VPCs:

```bash
aws ec2 describe-vpcs
```

Create a new VPC:

```bash
aws ec2 create-vpc --cidr-block 10.0.0.0/16
```

Delete a VPC:

```bash
aws ec2 delete-vpc --vpc-id vpc-12345678
```

## ECS (Elastic Container Service)

List ECS clusters:

```bash
aws ecs list-clusters
```

Create a new ECS cluster:

```bash
aws ecs create-cluster --cluster-name my-cluster
```

Delete an ECS cluster:

```bash
aws ecs delete-cluster --cluster my-cluster
```

## EKS (Elastic Kubernetes Service)

List EKS clusters:

```bash
aws eks list-clusters
```

Create an EKS cluster:

```bash
aws eks create-cluster --name my-cluster --role-arn arn:aws:iam::123456789012:role/EKSRole --resources-vpc-config subnetIds=subnet-abcde123,securityGroupIds=sg-01234abc
```

Delete an EKS cluster:

```bash
aws eks delete-cluster --name my-cluster
```

## SQS (Simple Queue Service)

List all SQS queues:

```bash
aws sqs list-queues
```

Create a new SQS queue:

```bash
aws sqs create-queue --queue-name my-queue
```

Send a message to an SQS queue:

```bash
aws sqs send-message --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue --message-body "Hello World"
```

## SNS (Simple Notification Service)

List all SNS topics:

```bash
aws sns list-topics
```

Create an SNS topic:

```bash
aws sns create-topic --name my-topic
```

Publish a message to an SNS topic:

```bash
aws sns publish --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic --message "Hello SNS"
```

## CloudFormation

List all CloudFormation stacks:

```bash
aws cloudformation list-stacks
```

Create a new CloudFormation stack:

```bash
aws cloudformation create-stack --stack-name my-stack --template-body file://template.yaml
```

Delete a CloudFormation stack:

```bash
aws cloudformation delete-stack --stack-name my-stack
```
