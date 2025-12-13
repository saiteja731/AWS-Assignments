# Assignment 1: IAM Users and Groups Creation

## Problem Statement
XYZ Corporation needs to manage user access to AWS resources. Create IAM users and organize them into groups for efficient permission management.

## Tasks Performed

### Task 1: Create 4 IAM Users
Create the following users in AWS IAM console:
- **Dev1** - Developer user
- **Dev2** - Developer user
- **Test1** - Test user
- **Test2** - Test user

#### Steps to Create Users:
1. Navigate to AWS IAM Service
2. Click on Users in the dashboard
3. Click "Create User"
4. Specify username (e.g., Dev1)
5. Enable "Provide user access to AWS Management Console"
6. Set custom password
7. Review and create user
8. Repeat for Dev2, Test1, Test2

### Task 2: Create 2 User Groups
Organize users into groups for centralized permission management:
- **Dev Team** - Contains Dev1 and Dev2
- **Ops Team** - Contains Dev1, Test1, Test2

#### Steps to Create Groups:
1. Navigate to IAM Console
2. Click on User Groups
3. Click "Create user group"
4. Specify group name (DevTeam or OpsTeam)
5. Skip permissions for now (will be attached later)
6. Create group

### Task 3: Add Users to Groups

#### Add to Dev Team:
1. Open DevTeam group
2. Click "Add users"
3. Select Dev1 and Dev2
4. Confirm addition

#### Add to Ops Team:
1. Open OpsTeam group
2. Click "Add users"
3. Select Dev1, Test1, and Test2
4. Confirm addition

## Summary
Successfully created 4 IAM users and 2 user groups with proper user memberships:
- **Dev Team**: Dev1, Dev2 (2 members)
- **Ops Team**: Dev1, Test1, Test2 (3 members)

This group structure enables efficient permission management where policies can be attached at the group level rather than individual users.
