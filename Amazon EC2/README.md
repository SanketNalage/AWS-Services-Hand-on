# 🚀 Amazon EC2 Guide  

This repository contains hands-on examples and implementations for **Amazon Elastic Compute Cloud (EC2)**, including:  

## 📌 Features  
✅ **EC2 Instance Creation** – Launch and manage EC2 instances  
✅ **SSH Access** – Connect to EC2 instances using SSH  
✅ **Security Groups** – Configure firewall rules for EC2 instances  
✅ **Elastic IP** – Associate and manage Elastic IPs for EC2 instances  
✅ **Key Pairs** – Generate and use key pairs for secure login  
✅ **AMI (Amazon Machine Images)** – Create and use custom AMIs for instance launch  
✅ **Autoscaling** – Set up EC2 Autoscaling to handle variable traffic loads  
✅ **EC2 Best Practices** – Cost optimization, security, and performance tips  

## 🔧 How to Use  
1. **Setup AWS CLI & Boto3**  
2. **Run the provided scripts** to launch EC2 instances and configure security  
3. **Verify EC2 instances** and configurations in the AWS Console  

### **Example Commands**  
- **Launch an EC2 Instance**:  
```sh
aws ec2 run-instances --image-id ami-xxxxxxxx --count 1 --instance-type t2.micro --key-name MyKeyPair
