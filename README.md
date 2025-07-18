# aws-cloudwatch-monitoring
AWS CloudWatch With SNS Setup
#  AWS EC2 Monitoring with CloudWatch Alarm & SNS Email Alert

This project demonstrates how to monitor an EC2 instance's CPU usage using **Amazon CloudWatch** and trigger an **SNS email notification** when CPU exceeds a threshold.  
It includes setup, stress testing, alert creation, email notification, and cleanup.

---

##  Project Goal

- Create a CloudWatch Alarm to monitor EC2 instance CPU utilization.
- Send an email notification using SNS when CPU > 70%.
- Simulate high CPU usage using `stress` tool.
- Clean up all AWS resources to avoid billing.

---

## Technologies Used

- **Amazon EC2**
- **Amazon CloudWatch**
- **Amazon SNS**
- **Amazon Linux 2023**
- **Linux CLI (Terminal, MobaXterm)**

---

##  Screenshots

> Screenshots are stored in the `/screenshots` folder.

- EC2 Launch & Setup
- IAM Role Creation & Attachment
- CloudWatch Alarm Configuration
- SNS Topic & Subscription
- Terminal Commands & Stress Test
- Alarm State (OK → ALARM → OK)
- Email Received
- Resource Cleanup

---

## ⚙Steps to Reproduce

### 1. Launch EC2 Instance

- OS: Amazon Linux 2023
- Type: t2.micro (Free Tier)
- Security Group: Allow SSH (port 22)
- Key Pair: Create/download `.pem`


### 2. Create CloudWatch Alarm

- Metric: `CPUUtilization`
- Threshold: `> 70%`
- Period: `5 minutes`
- Datapoints: `1 out of 1`
- Action: Send to SNS topic

---

###  3. Create SNS Topic & Subscription

```bash
aws sns create-topic --name HighCPUAlertTopic
aws sns subscribe --topic-arn <TOPIC_ARN> --protocol email --notification-endpoint yourmail@example.com

5. SSH into EC2 & Install stress
bash
Copy
Edit
sudo yum install stress -y
Run stress test for 5 minutes to spike CPU:

bash
Copy
Edit
stress --cpu 2 --timeout 300 &
You can monitor CPU usage with:

bash
Copy
Edit
top
