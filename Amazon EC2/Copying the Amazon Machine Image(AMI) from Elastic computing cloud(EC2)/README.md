# 🚀 Copying Amazon Machine Image (AMI) in EC2  

This guide explains how to **copy an Amazon Machine Image (AMI)** within the same or different AWS regions using **AWS Management Console** and **AWS CLI**.  

---

## 📌 Why Copy an AMI?  
✔️ **Disaster Recovery** – Keep backups in different regions  
✔️ **Faster Deployment** – Create multiple instances from a single AMI  
✔️ **Security & Compliance** – Store AMIs in restricted accounts  

---

## 🔧 Copying an AMI Using AWS Console  

1️⃣ **Log in to AWS Console** → Navigate to **EC2 Dashboard**  
2️⃣ **Go to AMIs** → Select the AMI to copy  
3️⃣ Click **Actions** → **Copy AMI**  
4️⃣ Select the **Destination Region**  
5️⃣ (Optional) **Encrypt the AMI**  
6️⃣ Click **Copy AMI** → The copied AMI will appear in the destination region  

---

## 🖥️ Copying an AMI Using AWS CLI  

### **1️⃣ Set Your Variables**  
```sh
SOURCE_AMI_ID="ami-xxxxxxxxxxxxxxxxx"  # Replace with your AMI ID
SOURCE_REGION="us-east-1"  # Change to the source region
DEST_REGION="us-west-2"  # Change to the destination region
NEW_AMI_NAME="MyCopiedAMI"
```

### **2️⃣ Copy the AMI* 
```ssh
aws ec2 copy-image --source-image-id $SOURCE_AMI_ID --source-region $SOURCE_REGION --region $DEST_REGION --name "$NEW_AMI_NAME"
```

### **3️⃣ Verify the Copied AMI**  
```ssh
aws ec2 describe-images --region $DEST_REGION --filters "Name=name,Values=$NEW_AMI_NAME"
```
