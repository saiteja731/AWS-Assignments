# Assignment-3: AWS IAM (Identity and Access Management)

## Overview
This assignment demonstrates comprehensive implementation of AWS IAM for managing users, groups, roles, and policies with hands-on practical examples.

## File Structure
- **README.md** - Main documentation
- **Assignment-1-IAM-Users.md** - Creating IAM users and groups
- **Assignment-2-IAM-Policies.md** - Creating and attaching policies
- **Assignment-3-IAM-Roles.md** - Creating IAM roles and trust policies
- **Assignment-4-CloudWatch-Dashboard.md** - CloudWatch dashboard setup
- **Assignment-5-CloudWatch-Alarms.md** - Setting up CloudWatch billing and CPU alarms

## Key Concepts Covered

### 1. IAM Users and Groups
- Creating individual IAM users (Dev1, Dev2, Test1, Test2)
- Organizing users into groups (Dev Team, Ops Team)
- Managing user permissions at group level

### 2. IAM Policies
- Custom policy creation with granular permissions
- Policy1: S3 full access, EC2 instance creation, RDS full access
- Policy2: CloudWatch and Billing full access, EC2/S3 list permissions
- Attaching policies to user groups

### 3. IAM Roles
- Creating roles with custom trust policies
- Cross-user role assumption using ARNs
- Role-based access control for VPC and DynamoDB resources
- Testing role functionality through console switching

### 4. CloudWatch Monitoring
- Creating CloudWatch dashboards for EC2 metrics
- Monitoring CPU utilization and network performance
- Setting up billing alarms (threshold: $500)
- Configuring CPU utilization alarms for EC2 instances
- SNS notifications for alarm triggers

## Security Best Practices Implemented
- Principle of least privilege (PoLP)
- Granular permission management
- User and group-based access control
- Role assumption with explicit trust relationships
- Monitoring and alerting for account security

## AWS Services Used
- AWS IAM (Identity and Access Management)
- AWS CloudWatch (Monitoring)
- AWS SNS (Simple Notification Service)
- AWS EC2 (Elastic Compute Cloud)
- AWS VPC (Virtual Private Cloud)
- AWS DynamoDB (NoSQL Database)

## Problem Statement
Implement a comprehensive security solution for XYZ Corporation to recognize and monitor different users while maintaining account security and resource management.

## Architecture Benefits
✓ Centralized user and access management
✓ Fine-grained permission control
✓ Real-time monitoring and alerting
✓ Audit trail for compliance
✓ Scalable access management
