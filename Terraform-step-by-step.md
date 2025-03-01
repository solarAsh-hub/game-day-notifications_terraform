![image](https://github.com/user-attachments/assets/ea4086d5-b429-4ee5-a8cf-5d2dce208af9)

## Prerequisites

Before you begin, ensure you have the following installed and configured:

- AWS CLI

- Terraform

- An account with SportsData.io to retrieve an API key

- IAM permissions to use AWS Systems Manager Parameter Store, Lambda, SNS, and EventBridge

# Setup Instructions

## 1. Navigate to the Terraform Directory

![image](https://github.com/user-attachments/assets/362d09c4-e8ab-421f-a2c8-7df9ab034300)

``` bash
cd game-day-notifications-terraform
```

## 2. Retrieve API Key from SportsData.io

- Log in to SportsData.io

- Navigate to your API keys section and copy the API key

![image](https://github.com/user-attachments/assets/3d72167c-4d1c-450b-9bb6-e77faf397bda)


## 3. Store API Key in AWS Systems Manager Parameter Store

- Run the following AWS CLI command to store your API key securely:

![image](https://github.com/user-attachments/assets/20a3f9d3-fe67-417b-867a-06af7b7ca71d)
``` bash 
aws ssm put-parameter --name "nba-api-key" --value "YOUR_API_KEY_HERE" --type "SecureString"
```

## 4. Initialize Terraform

![image](https://github.com/user-attachments/assets/cac0c933-b614-420b-a4dd-8161ef37fdc9)
```bash
terraform init
```

## 5. Format Terraform Code

![image](https://github.com/user-attachments/assets/694ef9e8-94dc-44da-b7e1-97e614376415)
```bash
terraform fmt
```

## 6. Validate Terraform Configuration

![image](https://github.com/user-attachments/assets/5cf97f64-f038-463e-be70-79c9e9ecc70a)
```bash
terraform validate
```

## 7. Deploy the Infrastructure

![image](https://github.com/user-attachments/assets/758d846b-a131-4f36-8373-d944e7aeb297)
``` bash
terraform apply -auto-approve
```

# Verifying Lambda Deployment

## 1. Go to AWS Lambda Console

- Navigate to AWS Lambda

![image](https://github.com/user-attachments/assets/7d3c8396-b92b-423d-bb08-3fac2f25052e)

- Click on Functions

![image](https://github.com/user-attachments/assets/4c805a3e-8742-408f-88dd-2b2d382ea99c)


- Locate and click the most recent function to verify it has been created


![image](https://github.com/user-attachments/assets/f0aba2b0-5813-4a3a-8f9d-ffc481a8c713)


# Configure SNS for Game Alerts

## 1. Go to Amazon SNS Console

- Navigate to Amazon SNS

![image](https://github.com/user-attachments/assets/9727eb43-8c49-4f02-915b-0fa04463bea6)

- Click on Topics

![image](https://github.com/user-attachments/assets/855301d0-a2dc-475b-a10f-380bdf6222b8)

- Find and click nba_game_alerts

![image](https://github.com/user-attachments/assets/58c319b9-b191-4305-8fd0-1ba236f8ac76)

## 2. Create an Email Subscription

- Click Create Subscription

- Select Email as the protocol

- Enter your email address

![image](https://github.com/user-attachments/assets/680f97e2-4c8b-4b1b-9c90-ed29b729c738)

- Click Create Subscription

![image](https://github.com/user-attachments/assets/b025f293-f3a3-4019-909f-5b5bd33bdf37)


## 3. Confirm Subscription

- Check your email inbox for a confirmation message

![image](https://github.com/user-attachments/assets/62ff5e68-4208-4e22-adcc-94c0aed5e1e8)

- Click the confirmation link to activate the subscription

![image](https://github.com/user-attachments/assets/622b2a86-1008-4ddf-be12-f862ff7bad8d)

![image](https://github.com/user-attachments/assets/d949efb5-18fb-4cb7-befe-ae010ed8893e)


# Testing Lambda Execution

## 1. Navigate to AWS Lambda Console

![image](https://github.com/user-attachments/assets/90be8f02-a2bd-4649-8850-c29c1b3d9de6)

- Go to AWS Lambda

- Select nba_game_alerts function

![image](https://github.com/user-attachments/assets/158c0de8-07b9-42fe-af67-2eb2397688c7)

- Click Test

![image](https://github.com/user-attachments/assets/399f429b-1cd3-4d0d-9283-74ae28a08a92)

- Name your test event

- Click Test

![image](https://github.com/user-attachments/assets/e02be888-69d7-427d-b081-a3c8acb525dc)

- Ensure a successful execution message appears

![image](https://github.com/user-attachments/assets/d1484e84-625c-4d5a-8ca5-277b20885add)

## 2. Verify Email Notifications

- Check your email for an NBA Game Update

![image](https://github.com/user-attachments/assets/12c8d848-4567-4c79-8808-1b7cc6d12913)

- Configure EventBridge Rule

![image](https://github.com/user-attachments/assets/f62af621-436f-4dcd-9321-92d3d64fa9bb)

## 1. Go to Amazon EventBridge Console

- Navigate to Amazon EventBridge

- Click the blue link to view event details

- Go to Rules section to confirm setup

![image](https://github.com/user-attachments/assets/6ac996bf-39f9-4ac2-b00a-20afad3c5e54)

Destroy Infrastructure

![image](https://github.com/user-attachments/assets/228fff79-128d-470e-9ed2-d9e0a0a1334d)

If you need to remove all resources created by Terraform, run:
```bash
terraform destroy -auto-approve
```
This will clean up all AWS resources associated with the project.

## Conclusion

This setup ensures automated NBA game notifications using AWS Lambda, SNS, and EventBridge, all managed through Terraform. If you encounter any issues, check AWS CloudWatch logs for debugging.

