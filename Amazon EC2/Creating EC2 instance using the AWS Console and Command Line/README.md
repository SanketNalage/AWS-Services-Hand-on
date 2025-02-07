# 🚀 Creating an Amazon EC2 Instance Using AWS Console  

This guide provides step-by-step instructions to launch an **Amazon EC2** instance using the **AWS Management Console**.  

## 📌 Steps to Create an EC2 Instance  

### **1️⃣ Log in to AWS Console**  
- Go to [AWS Console](https://aws.amazon.com/console/).  
- Navigate to **EC2** under "Compute" services.  

### **2️⃣ Launch a New Instance**  
- Click **"Launch Instance"**.  
- Enter a **name** for your instance.  

### **3️⃣ Choose an Amazon Machine Image (AMI)**  
- Select an **Amazon Linux 2**, **Ubuntu**, or other AMI based on your requirements.  

### **4️⃣ Select Instance Type**  
- Choose a suitable instance type (e.g., `t2.micro` for free tier).  

### **5️⃣ Configure Key Pair**  
- Create a new **key pair** or select an existing one.  
- Download the `.pem` file (important for SSH access).  

### **6️⃣ Configure Security Group**  
- Allow inbound SSH traffic (`port 22`) for remote access.  
- Add HTTP (`port 80`) or HTTPS (`port 443`) if hosting a web app.  

### **7️⃣ Configure Storage**  
- Default storage: **8GB (Amazon Linux 2/Ubuntu)**.  
- Modify based on your needs.  

### **8️⃣ Review and Launch**  
- Verify settings and click **"Launch Instance"**.  
- Your EC2 instance will start running.  

## 🔧 Connecting to the EC2 Instance  

### **Using SSH (Mac/Linux)**
```sh
ssh -i MyKeyPair.pem ec2-user@your-public-ip
```

____________________________________________________________________________________________________________________________________________

# 🚀 Creating an Amazon EC2 Instance Using AWS CLI  

This guide provides step-by-step instructions to launch an **Amazon EC2** instance using the **AWS Command Line Interface (CLI)**.  

## 📌 Prerequisites  
✔️ **Install AWS CLI** → [Download Here](https://aws.amazon.com/cli/)  
✔️ **Configure AWS CLI** → Run:  
```sh
aws configure
```

### **1️⃣ Set Your Variables**
```ssh
AMI_ID="ami-xxxxxxxxxxxxxx"  # Amazon Linux 2 AMI (or your choice)
INSTANCE_TYPE="t2.micro"  # Free-tier eligible instance
KEY_NAME="MyKeyPair"  # Your key pair name
SECURITY_GROUP="MySecurityGroup"  # Security group name
SUBNET_ID="subnet-xxxxxxxxxxxxxx"  # Your subnet ID
```
### **2️⃣ Create a Security Group** 
```ssh
aws ec2 create-security-group --group-name MySecurityGroup --description "My EC2 security group"
```
✔️ **Allow SSH (port 22) access:**
```ssh
aws ec2 authorize-security-group-ingress --group-name MySecurityGroup --protocol tcp --port 22 --cidr 0.0.0.0/0
```

### **3️⃣ Launch EC2 Instance**  
```ssh
aws ec2 run-instances --image-id $AMI_ID --count 1 --instance-type $INSTANCE_TYPE --key-name $KEY_NAME --security-groups $SECURITY_GROUP --subnet-id $SUBNET_ID
```

### **4️⃣ Get Instance ID & Public IP**
```ssh
aws ec2 describe-instances --query "Reservations[*].Instances[*].[InstanceId,PublicIpAddress]" --output table
```

## 🔧 Connecting to the EC2 Instance  

### **Using SSH (Mac/Linux)**
```sh
ssh -i MyKeyPair.pem ec2-user@your-public-ip
```


