# Assignment 2: EFS (Elastic File System) Multi-Instance Setup

## Overview

This assignment demonstrates the creation and management of Amazon Elastic File System (EFS) connected to multiple EC2 instances with different operating systems, showcasing shared storage and file synchronization capabilities.

## Original File
**Assignment.pdf** - Complete assignment documentation with step-by-step procedures

## Objective

Create a scalable, shared file storage solution using EFS that can be accessed simultaneously from multiple EC2 instances running different Linux distributions.

## Tasks Completed

### 1. EFS Creation & Configuration
- ✅ Created Amazon EFS file system
- ✅ Named: "assignment1"
- ✅ VPC: vpc-07c56690086316e6f (Default VPC)
- ✅ Throughput Mode: **Elastic** (automatic scaling)
- ✅ Automatic Backups: **Enabled**
- ✅ Encryption: **Enabled**
- ✅ File System State: **Available**

### 2. EC2 Instances with Different OS

Launched **3 EC2 instances** with diverse operating systems:

#### Instance 1: Ubuntu
- **Name**: Ubuntu Instace
- **Instance ID**: i-044197889a12c3912
- **OS**: Ubuntu Server 24.04 LTS
- **Instance Type**: t3.micro
- **Public IP**: 3.94.190.168
- **Private IP**: 172.31.19.80
- **Region**: US-East-1

#### Instance 2: Amazon Linux
- **Name**: Amazon Linux Instance
- **Instance ID**: i-0ba7dfa12cb04a6a6
- **OS**: Amazon Linux 2023
- **Instance Type**: t3.micro
- **Public IP**: 54.90.164.250
- **Private IP**: 172.31.23.111
- **Region**: US-East-1

#### Instance 3: Red Hat Enterprise Linux
- **Name**: Red Hat Instance
- **Instance ID**: i-077799d41d96ea67b
- **OS**: Red Hat Enterprise Linux 10
- **Instance Type**: t3.micro
- **Public IP**: 34.207.151.117
- **Private IP**: 172.31.27.204
- **Region**: US-East-1

### 3. Security Configuration
- ✅ Modified Security Group inbound rules
- ✅ **All Traffic allowed** from anywhere (IPv4: 0.0.0.0/0)
- ✅ Security Group: sg-0ee4964a5d8ad971b (default)
- ✅ Enabled NFS access for EFS

### 4. NFS Setup on Each Instance

#### Ubuntu Setup
```bash
sudo apt-get update
sudo apt install nfs-common
mkdir efs
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport 172.31.92.9:/efs
```

#### Amazon Linux Setup
```bash
sudo yum update
sudo yum install nfs-utils
mkdir efs
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport 172.31.92.9:/efs
```

#### Red Hat Enterprise Linux Setup
```bash
sudo yum update
sudo yum install nfs-utils
mkdir efs
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport 172.31.93.118:/efs
```

### 5. EFS Mount Points Configuration

EFS automatically creates mount targets in all AZs:

| Availability Zone | Mount Target State | Mount Target IP | Network Interface |
|------------------|-------------------|-----------------|-------------------|
| us-east-1a | Available | 172.31.92.9 | eni-0548478e8 |
| us-east-1b | Available | 172.31.23.1 | eni-0031590400 |
| us-east-1c | Available | 172.31.42.7 | eni-0d8c6fa296 |
| us-east-1d | Available | 172.31.0.12 | eni-059eb7d18 |
| us-east-1f | Available | 172.31.78.1 | eni-01f70ad5ba |

### 6. File Synchronization Testing

#### File Created: `assignmentfile.txt`
- **Created on**: Amazon Linux Instance (Instance 2)
- **Location**: /home/ec2-user/efs/
- **Method**: `sudo touch assignmentfile.txt`

#### File Verification:
- ✅ **Ubuntu Instance**: File found via `ls /home/ubuntu/efs/`
- ✅ **Amazon Linux Instance**: File found via `ls /home/ec2-user/efs/`
- ✅ **Red Hat Instance**: File found via `ls /home/ec2-user/efs/`

**Result**: All instances have synchronized access to the same file!

## Key Features Demonstrated

### 1. **Shared Storage**
- Single EFS filesystem accessed by 3 different instances
- No data replication needed between instances
- Automatic synchronization across mount points

### 2. **Multi-OS Compatibility**
- EFS works seamlessly with Ubuntu, Amazon Linux, and Red Hat
- Same NFS mounting commands work across distributions
- Unified file access regardless of OS

### 3. **Scalability**
- EFS automatically scales throughput
- No pre-provisioning of capacity needed
- Elastic Mode handles variable workloads

### 4. **High Availability**
- Mount targets span multiple Availability Zones
- Automatic failover if one AZ becomes unavailable
- Regional file system (not limited to single AZ)

### 5. **Security**
- Encryption at rest and in transit
- Security Group controls access
- NFS v4.1 protocol for security

## Technical Specifications

### EFS Properties
- **File System ID**: fs-012ef5db5d23a105d
- **Status**: Available
- **Performance Mode**: General Purpose
- **Throughput Mode**: Elastic (Automatic)
- **Availability**: Regional (All AZs in US-East-1)
- **Metered Size**: Scales with usage

### Networking
- **VPC**: vpc-07c56690086316e6f (Default)
- **Security Group**: sg-0ee4964a5d8ad971b
- **Mount Target Protocol**: NFS v4.1
- **Network Interface**: Multiple (one per AZ)

## Comparison: EBS vs EFS

| Feature | EBS | EFS |
|---------|-----|-----|
| **Attachment** | Single Instance | Multiple Instances |
| **Availability** | Single AZ | Multiple AZs (Regional) |
| **Scaling** | Manual | Automatic (Elastic) |
| **Access** | Block Storage | File System (NFS) |
| **Use Case** | Databases, OS | Shared Storage, Apps |
| **Cost** | Lower | Higher |

## Best Practices Applied

✅ Used appropriate instance types (t3.micro)
✅ Enabled encryption for data protection
✅ Implemented automatic backups
✅ Used Security Groups for access control
✅ Tested file synchronization across all instances
✅ Documented all mount procedures
✅ Verified multi-OS compatibility
✅ Ensured proper NFS configuration

## Learning Outcomes

1. **Shared Storage Architecture**: Understanding how EFS enables centralized storage
2. **Multi-OS Management**: Deploying and managing instances across different Linux distributions
3. **File Synchronization**: Verifying real-time file access across instances
4. **Network File System**: Understanding NFS protocol and mount options
5. **AWS Best Practices**: Security, scalability, and high availability
6. **Cost Optimization**: Using elastic resources instead of over-provisioning

## Completion Status

**✅ ASSIGNMENT COMPLETED** - All tasks successfully implemented

### Checklist
- [x] Created EFS file system
- [x] Launched 3 EC2 instances (Ubuntu, Amazon Linux, Red Hat)
- [x] Installed NFS utilities on all instances
- [x] Configured security groups
- [x] Mounted EFS on all instances
- [x] Created test file
- [x] Verified file synchronization
- [x] Documented all procedures

*Completed: September 2025*
*Student: Chatha Sai Teja*
