# Assignment 3: IAM Roles and Role Assumption

## Problem Statement
XYZ Corporation needs to implement role-based access control allowing specific users to assume roles with permissions for VPC and DynamoDB resources.

## Tasks Performed

### Task 1: Create IAM Role with Custom Trust Policy

**Role Name**: `FullAccess-VPC-DynamoDB`

**Trusted Users**: Dev1 and Dev2 (using their ARNs)

#### Steps:
1. Navigate to IAM → Roles
2. Click "Create role"
3. Select "Custom Trust Policy" as trusted entity type
4. Edit JSON trust policy to include ARNs:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": [
          "arn:aws:iam::ACCOUNT-ID:user/Dev1",
          "arn:aws:iam::ACCOUNT-ID:user/Dev2"
        ]
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

### Task 2: Attach Permissions to Role

Attach the following AWS managed policies:
- **AmazonVPCFullAccess** - Full access to VPC operations
- **AmazonDynamoDBFullAccess** - Full access to DynamoDB operations

#### Steps:
1. In Create Role wizard, select "Add permissions"
2. Search for and select "AmazonVPCFullAccess"
3. Add another permission and select "AmazonDynamoDBFullAccess"
4. Review and create role

### Task 3: Test Role Assumption

#### Steps:
1. Login to AWS Console as Dev1 user
2. Click on account menu (top right corner)
3. Select "Switch Role"
4. Provide:
   - Account ID: Your AWS Account ID
   - Role Name: `FullAccess-VPC-DynamoDB`
5. Verify access to:
   - VPC dashboard and resources
   - DynamoDB tables and operations

## Role Architecture

```
┌─────────────────────────────────────┐
│    IAM Users (Dev1, Dev2)            │
└──────────┬──────────────────────────┘
           │ sts:AssumeRole
           ▼
┌─────────────────────────────────────┐
│  FullAccess-VPC-DynamoDB Role        │
│  ├─ AmazonVPCFullAccess              │
│  └─ AmazonDynamoDBFullAccess         │
└─────────────────────────────────────┘
           │
           ├──► VPC Resources
           └──► DynamoDB Resources
```

## Security Benefits

1. **Separation of Duties**: Users don't have permanent VPC/DynamoDB permissions
2. **Time-Limited Access**: Role sessions have configurable duration (default 1 hour)
3. **Audit Trail**: AWS CloudTrail logs all role assumption and actions
4. **Fine-grained Control**: Specific users can assume specific roles
5. **Temporary Credentials**: Role assumption provides temporary security credentials

## Role Session Configuration

- **Maximum Session Duration**: 1 hour (default, can be increased)
- **Session Token**: Valid for the duration, automatically expires
- **Temporary Access Key**: Automatically managed by AWS
- **Session Name**: Tracked in CloudTrail for audit purposes

## Verification

After assuming the role, verify permissions by:
1. Navigate to VPC console - should have full access
2. Navigate to DynamoDB console - should have full access
3. Attempt to access other services - should receive "Access Denied"
4. Check CloudTrail for AssumeRole action logs
