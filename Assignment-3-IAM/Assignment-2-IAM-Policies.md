# Assignment 2: IAM Policies Creation and Attachment

## Problem Statement
Create custom IAM policies with granular permissions and attach them to user groups to enforce principle of least privilege.

## Tasks Performed

### Task 1: Create Policy 1 (Dev Team Policy)
Policy with the following permissions:
- **S3**: Complete access (all actions)
- **EC2**: Create instances only (RunInstances action)
- **RDS**: Full access (all actions)

#### Steps to Create Policy 1:
1. Navigate to IAM → Policies
2. Click "Create policy"
3. Use Visual Editor:
   - **Service**: S3 → Effect: Allow → All Actions
   - **Service**: EC2 → Effect: Allow → Action: RunInstances
   - **Service**: RDS → Effect: Allow → All Actions
4. Review and create with name: `Policy1-DevTeam`

### Task 2: Create Policy 2 (Ops Team Policy)
Policy with the following permissions:
- **CloudWatch**: Complete access (all actions)
- **Billing**: Complete access (all actions)
- **EC2**: List resources only (DescribeInstances action)
- **S3**: List resources only (ListAllMyBuckets, ListBucket actions)

#### Steps to Create Policy 2:
1. Navigate to IAM → Policies
2. Click "Create policy"
3. Use Visual Editor:
   - **Service**: CloudWatch → Effect: Allow → All Actions
   - **Service**: Billing → Effect: Allow → All Actions
   - **Service**: EC2 → Effect: Allow → Action: DescribeInstances
   - **Service**: S3 → Effect: Allow → Action: ListAllMyBuckets, ListBucket
4. Review and create with name: `Policy2-OpsTeam`

### Task 3: Attach Policies to Groups

#### Attach Policy1 to Dev Team:
1. Navigate to Policies
2. Select Policy1
3. Click Actions → Attach
4. Select "DevTeam" user group
5. Confirm attachment

#### Attach Policy2 to Ops Team:
1. Navigate to Policies
2. Select Policy2
3. Click Actions → Attach
4. Select "OpsTeam" user group
5. Confirm attachment

## Policy Summary

### Policy1 Permissions Matrix
| Service | Action | Effect |
|---------|--------|--------|
| S3 | All | Allow |
| EC2 | RunInstances | Allow |
| RDS | All | Allow |

### Policy2 Permissions Matrix
| Service | Action | Effect |
|---------|--------|--------|
| CloudWatch | All | Allow |
| Billing | All | Allow |
| EC2 | Describe* | Allow |
| S3 | List* | Allow |

## Security Implementation
- **Principle of Least Privilege**: Dev Team can only create EC2 instances (not terminate)
- **Read-only for Ops**: EC2 and S3 are read-only for operations team
- **Full Monitoring Access**: Ops team can monitor all resources
- **Billing Visibility**: Ops team can monitor costs

## Verification Steps
1. Login as Dev1 and verify S3, EC2 create, and RDS access
2. Login as Test1 and verify CloudWatch, Billing, and read-only EC2/S3 access
3. Attempt to perform unauthorized actions and verify denial
