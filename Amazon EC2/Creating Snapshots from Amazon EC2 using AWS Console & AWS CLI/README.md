# 🚀 Creating Snapshots from Amazon EC2  

This guide explains how to create **Amazon Elastic Block Store (EBS) Snapshots** from an EC2 instance using **AWS Console** and **AWS CLI**.  

---

## 📌 Why Create Snapshots?  
✔️ **Backup & Recovery** – Protect data from failures  
✔️ **Disaster Recovery** – Restore instances quickly  
✔️ **Instance Migration** – Move storage to another region  
✔️ **Compliance & Security** – Maintain secure backups  

---

## 🔧 Creating Snapshots Using AWS Console  

1️⃣ **Log in to AWS Console** → Navigate to **EC2 Dashboard**  
2️⃣ Click **Volumes** in the left panel  
3️⃣ Select the **EBS volume** attached to your instance  
4️⃣ Click **Actions** → **Create Snapshot**  
5️⃣ Enter a **name & description** for the snapshot  
6️⃣ Click **Create Snapshot** → The snapshot will appear in **Snapshots**  

---

## 🖥️ Creating Snapshots Using AWS CLI  

### **1️⃣ Set Your Variables**  
```sh
INSTANCE_ID="i-xxxxxxxxxxxxxxxxx"  # Replace with your EC2 instance ID
VOLUME_ID=$(aws ec2 describe-instances --instance-ids $INSTANCE_ID --query "Reservations[*].Instances[*].BlockDeviceMappings[*].Ebs.VolumeId" --output text)
```

### **2️⃣ Create a Snapshot** 
```ssh
aws ec2 create-snapshot --volume-id $VOLUME_ID --description "Backup Snapshot"
```

### **3️⃣ Verify the Snapshot** 
```ssh
aws ec2 describe-snapshots --filters "Name=volume-id,Values=$VOLUME_ID" --query "Snapshots[*].SnapshotId"
```
