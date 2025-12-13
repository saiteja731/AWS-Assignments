# AWS Cloud Computing Assignments

This repository contains AWS cloud computing assignments covering EC2, EBS, EFS, and AMI management. All assignments are documented with step-by-step procedures and screenshots.

## 📋 Assignments Overview

### Assignment 1: EC2, AMI, and EBS Management
**File:** `Case-Study.pdf`

**Objective:** Implement secure web servers on Linux using AWS EC2 instances, manage AMIs across regions, and handle EBS volumes.

**Topics Covered:**
- EC2 Instance Creation (US-East-1 N. Virginia region)
- Creating custom AMI from instances
- Replicating AMI to different regions (US-West-2 Oregon)
- Launching instances from AMI in different regions
- EBS Volume Creation and Management
- Attaching multiple volumes to instances
- Detaching and deleting EBS volumes
- Extending EBS volume size
- EBS Volume Snapshots for backup

**Key AWS Services Used:**
- Amazon EC2
- Amazon Machine Images (AMI)
- Amazon EBS (Elastic Block Store)
- AWS Management Console

---

### Assignment 2: EFS (Elastic File System) Multi-Instance Setup
**File:** `Assignment.pdf`

**Objective:** Create an EFS file system and connect it to multiple EC2 instances with different operating systems to demonstrate shared storage capabilities.

**Topics Covered:**
- Amazon EFS Creation and Configuration
- Creating EC2 instances with different OS:
  - Ubuntu 24.04 LTS
  - Amazon Linux 2023
  - Red Hat Enterprise Linux 10
- Installing NFS utilities on each instance
- Mounting EFS to multiple instances
- Verifying shared storage functionality
- File creation and synchronization across instances

**Key AWS Services Used:**
- Amazon EFS (Elastic File System)
- Amazon EC2 (Multiple Instances)
- VPC and Security Groups
- NFS Protocol

**Key Features Demonstrated:**
- EFS is region-specific, not AZ-specific
- Shared storage accessible from multiple instances
- File synchronization across different OS
- Auto-scaling mount targets

---

## 🛠️ Tools & Technologies

- **AWS Management Console**
- **AWS CLI** (where applicable)
- **Linux Terminal** (Ubuntu, Amazon Linux, Red Hat)
- **NFS (Network File System)**
- **VPC & Security Groups**

## 📚 Learning Outcomes

After completing these assignments, you will understand:

1. **EC2 Management**
   - Launching and configuring EC2 instances
   - Understanding instance types and key pairs
   - Managing security groups and network access

2. **AMI & Image Management**
   - Creating custom AMIs from running instances
   - Copying AMIs across AWS regions
   - Launching instances from custom AMIs

3. **Storage Solutions**
   - EBS volumes - block-level storage
   - EFS - shared file system storage
   - Snapshots and backups
   - Volume scaling and management

4. **Multi-Region & Multi-Instance Architecture**
   - Replicating infrastructure across regions
   - Managing resources in multiple regions
   - Ensuring high availability

5. **Networking & Access Control**
   - Security group configuration
   - Inbound/outbound rules
   - VPC management

## 📁 Repository Structure

```
AWS-Assignments/
├── README.md
├── Case-Study.pdf (Assignment 1 - EC2, AMI, EBS)
└── Assignment.pdf (Assignment 2 - EFS Multi-Instance)
```

## ✅ Completion Checklist

### Assignment 1:
- [x] Created EC2 instance in US-East-1 (N. Virginia)
- [x] Created custom AMI from instance
- [x] Copied AMI to US-West-2 (Oregon)
- [x] Launched instance in Oregon from copied AMI
- [x] Created and attached 2 EBS volumes
- [x] Detached and deleted one volume
- [x] Extended remaining volume size
- [x] Created EBS snapshots for backup

### Assignment 2:
- [x] Created EFS file system
- [x] Launched 3 EC2 instances (Ubuntu, Amazon Linux, Red Hat)
- [x] Mounted EFS on all instances
- [x] Verified file synchronization across instances
- [x] Demonstrated shared storage functionality

## 🔑 Key Learnings

1. **Scalability**: Both EBS and EFS allow scaling, but EFS provides automatic scaling without intervention
2. **Availability**: EFS spans multiple AZs for higher availability compared to single-AZ EBS
3. **Cost Optimization**: Understanding trade-offs between EBS and EFS for different use cases
4. **Regional Architecture**: Best practices for multi-region deployments
5. **Security**: Proper security group configuration for accessing shared resources

## 📖 References

- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
- [Amazon EBS Documentation](https://docs.aws.amazon.com/ebs/)
- [Amazon EFS Documentation](https://docs.aws.amazon.com/efs/)
- [AWS AMI Documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html)

## 👤 Author

**Chatha Sai Teja**
- B.Tech Cybersecurity Student
- AWS Cloud Aspirant
- GitHub: [@saiteja731](https://github.com/saiteja731)

---
