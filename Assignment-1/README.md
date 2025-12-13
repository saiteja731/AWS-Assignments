# Assignment 1: EC2, AMI, and EBS Management

## Overview

This assignment demonstrates practical implementation of AWS EC2 instances, Amazon Machine Images (AMI), and Elastic Block Store (EBS) volumes in a multi-region architecture.

## Original File
**Case-Study.pdf** - Complete assignment documentation with screenshots

## Tasks Completed

### 1. EC2 Instance Creation
- ✅ Launched EC2 instance in **US-East-1 (N. Virginia)** region
- ✅ Selected **Linux OS** as operating system
- ✅ Configured security groups
- ✅ Set up key pairs for secure access
- Instance Type: **t2.micro** (Free tier eligible)

### 2. AMI Creation & Management
- ✅ Created custom AMI from the running EC2 instance
- ✅ Named AMI: "assignment1"
- ✅ Enabled automatic snapshots during AMI creation
- ✅ Verified AMI status (Available)

### 3. Multi-Region Replication
- ✅ Copied AMI from **US-East-1** to **US-West-2 (Oregon)**
- ✅ Configured copy options:
  - Enabled "Copy tags"
  - Configured snapshot copying
  - Encrypted EBS snapshots

### 4. Instance Launch from AMI
- ✅ Launched new instance in US-West-2 Oregon from copied AMI
- ✅ Instance Name: "assignment1-oregon"
- ✅ Verified public IP assignment
- ✅ Confirmed running state

### 5. EBS Volume Management

#### Volume Creation
- ✅ Created **2 EBS volumes**
- Volume Size: **10 GiB** each
- Volume Type: **gp2 (General Purpose)**
- Availability Zone: **us-east-1b**

#### Volume Attachment
- ✅ Attached both volumes to US-East-1 instance
- ✅ Device mapping: /dev/sdf and /dev/sdg
- ✅ Verified attachment status

#### Volume Modification
- ✅ **Deleted Volume 2** after detaching it safely
- ✅ **Extended Volume 1** from 10 GiB to **20 GiB**
- ✅ Verified size increase in volume properties

### 6. Backup & Snapshots
- ✅ Created **EBS Snapshot** of the extended volume
- ✅ Snapshot contains full backup of 20 GiB volume
- ✅ Can be used for disaster recovery or volume restoration

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                    AWS Cloud Infrastructure                  │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  ┌──────────────────────┐      ┌──────────────────────┐    │
│  │  US-East-1 (N. VA)   │      │  US-West-2 (Oregon)  │    │
│  │  ┌────────────────┐  │      │  ┌────────────────┐  │    │
│  │  │  EC2 Instance  │  │      │  │  EC2 Instance  │  │    │
│  │  │  assignment1   │  │      │  │ assignment1-   │  │    │
│  │  │                │  │      │  │   oregon       │  │    │
│  │  └────────────────┘  │      │  └────────────────┘  │    │
│  │                      │      │  (Launched from      │    │
│  │  ┌────────────────┐  │      │   Copied AMI)        │    │
│  │  │  EBS Volume 1  │  │      └──────────────────────┘    │
│  │  │  (20 GiB) ✓    │  │                                    │
│  │  └────────────────┘  │                                    │
│  │                      │                                    │
│  │  [EBS Snapshot] ✓    │                                    │
│  └──────────────────────┘                                    │
│                                                               │
│          AMI: assignment1 (Copied to Oregon)                 │
│                                                               │
└─────────────────────────────────────────────────────────────┘
```

## Technical Details

### Instance Specifications
- **Instance ID (US-East-1)**: i-02aff2659fb337910
- **Instance ID (US-West-2)**: i-09b108c53b9c19dc6
- **Instance Type**: t2.micro
- **Root Volume**: 8 GiB (gp2)
- **Additional EBS**: 20 GiB (Extended from 10 GiB)

### AMI Details
- **AMI ID (Source)**: ami-094d172aac5e2d219 (US-East-1)
- **AMI ID (Copy)**: ami-0f74961ad73a92ab4 (US-West-2)
- **Root Device**: EBS (/dev/xvda)
- **Virtualization**: HVM (Hardware Virtual Machine)
- **Architecture**: x86_64

### EBS Volume Management
- **Volume 1**: vol-xxx (10 GiB) → Extended to 20 GiB
- **Volume 2**: vol-xxx (10 GiB) → Deleted
- **Snapshot**: snap-xxx (20 GiB backup)

## Key Learnings

1. **EC2 Instances**: Scalable compute capacity in the cloud
2. **AMI Creation**: Custom machine images for consistent deployments
3. **Multi-Region Architecture**: Disaster recovery and global reach
4. **EBS Volumes**: Persistent block-level storage
5. **Volume Scaling**: Dynamic storage expansion without downtime
6. **Snapshots**: Point-in-time backups for data protection

## AWS Services Used

| Service | Purpose | Region |
|---------|---------|--------|
| EC2 | Compute Resources | US-East-1, US-West-2 |
| AMI | Machine Images | US-East-1, US-West-2 |
| EBS | Block Storage | US-East-1 |
| Snapshots | Backup & Recovery | US-East-1 |
| VPC | Networking | US-East-1, US-West-2 |

## Best Practices Applied

✅ Used IAM for secure access
✅ Enabled encryption for EBS snapshots
✅ Implemented proper security groups
✅ Utilized key pairs for SSH access
✅ Created backups before volume modifications
✅ Documented all steps with screenshots

## Cost Optimization

- Utilized **Free Tier** resources (t2.micro, 30 GiB free EBS storage)
- Deleted unused volumes to reduce costs
- Created snapshots for backup instead of duplicate volumes

## Completion Status

**✅ ASSIGNMENT COMPLETED** - All tasks successfully implemented and documented

*Completed: September 2025*
*Student: Chatha Sai Teja*
