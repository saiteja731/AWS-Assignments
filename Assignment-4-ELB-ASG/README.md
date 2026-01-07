# Assignment 4: ELB, ASG, and Route 53

## 📋 Case Study Problem Statement

XYZ Corporation uses on-premise solutions with a limited number of systems. With increasing application requests, the load increases significantly. To handle this growth, they were previously required to purchase new systems regularly, which became very expensive.

To reduce infrastructure costs, they decided to migrate their infrastructure to AWS and implement auto-scaling capabilities with load balancing.

## 🎯 Objectives

1. **Manage Scaling Requirements**: Implement Auto Scaling Group (ASG) to automatically deploy and remove compute resources based on demand
   - Deploy new EC2 instances when CPU utilization exceeds 80%
   - Remove instances when CPU utilization drops below 60%

2. **Distribute Load**: Create a load balancer to distribute traffic across multiple compute resources

3. **Route Traffic**: Route traffic to the company's domain using Route 53

## 🏗️ Architecture Overview

Internet -> Load Balancer (ALB/NLB) -> EC2 Instances (ASG) -> Route 53 handles DNS routing to the Load Balancer

## 📝 Implementation Steps

### Step 1: Create Auto Scaling Group (ASG)

**Create Launch Template:**
- Launch Template Name: demoLt
- AMI: Amazon Linux 2023
- Instance Type: t2.nano or t2.micro
- Key Pair: Select your existing key pair
- Security Group: default or create a new one
- User Data (Optional):
  ```bash
  #!/bin/bash
  sudo su
  yum update -y
  yum install httpd -y
  service httpd start
  chkconfig httpd on
  echo "Hello from $(hostname -f)" > /var/www/html/index.html
  ```

**Configure ASG Settings:**
- ASG Name: demoAsg
- Launch Template: Select the created template
- VPC: Default VPC
- Availability Zones: Select multiple AZs for high availability

**Group Size Configuration:**
- Desired Capacity: 2
- Min Capacity: 1  
- Max Capacity: 4

### Step 2: Create Dynamic Scaling Policies

**Configure Target Tracking Policy:**
1. In the ASG details, click 'Automatic Scaling'
2. Click 'Create dynamic scaling policy'
3. Policy Settings:
   - Policy Type: Target Tracking Scaling
   - Metric Type: Average CPU utilization
   - Target Value: 80 (to scale out when CPU > 80%)
   - Instance Warmup: 300 seconds

Target tracking automatically handles scale-in when utilization drops below approximately 60%.

### Step 3: Create Load Balancer

**Via ASG Integration:**
1. In ASG details, click 'Integrations'
2. Click 'Edit' in the Load Balancing section
3. Select Load Balancer Type:
   - ALB: For HTTP/HTTPS (Layer 7)
   - NLB: For high performance, TCP/UDP (Layer 4)
4. Configure:
   - Load Balancer Name: demoAsg-1
   - Scheme: Internet-facing
   - Network Mapping: Select subnets from different AZs
   - Listener Configuration:
     * Protocol: HTTP
     * Port: 80
   - Create Target Group: demoAsg-1 (auto-created)
5. Click 'Update Auto Scaling group'

**Verification:**
- Check Activity history for successful load balancer creation
- Verify instances are registered with the target group

### Step 4: Route 53 Configuration (Optional)

To route traffic to your domain:
1. Register or use an existing domain with Route 53
2. Create a record set:
   - Type: A (for IPv4)
   - Target: Your Load Balancer DNS name
3. Test DNS resolution

Note: Domain registration may incur additional costs.

## 🔑 Key AWS Services Used

| Service | Purpose | Details |
|---------|---------|----------|
| EC2 | Compute Resources | Virtual servers for applications |
| Auto Scaling | Dynamic Capacity | Automatically scale instances based on demand |
| Elastic Load Balancer | Traffic Distribution | Distribute load across instances |
| CloudWatch | Monitoring | Monitor CPU and trigger scaling policies |
| Route 53 | DNS Management | Route domain traffic to load balancer |
| VPC | Network | Isolated network environment |

## 📊 Scaling Behavior

### Scale-Out (Add Instances)
- Trigger: CPU utilization > 80% for 2-3 minutes
- Action: ASG launches new EC2 instance
- Warmup Period: 300 seconds
- Max Limit: Cannot exceed max capacity (4 instances)

### Scale-In (Remove Instances)
- Trigger: CPU utilization < 60% for 5 minutes
- Action: ASG terminates least important instances
- Min Limit: Cannot go below min capacity (1 instance)
- Protection: Can enable scale-in protection for critical instances

## 📈 Expected Results

After implementation:
- ✅ Automatic instance scaling based on CPU utilization
- ✅ Load distributed evenly across all running instances
- ✅ High availability with instances across multiple AZs
- ✅ Reduced operational overhead - no manual scaling needed
- ✅ Cost optimization - instances scale down during low traffic
- ✅ Self-healing - ASG automatically replaces unhealthy instances

## 📋 Completion Checklist

- [ ] Launch Template created with proper configuration
- [ ] Auto Scaling Group created with desired capacity = 2
- [ ] Scaling policies configured (target: 80% CPU)
- [ ] Load Balancer (ALB/NLB) created and integrated
- [ ] Target Group created and instances registered
- [ ] CloudWatch metrics showing CPU utilization
- [ ] Instances automatically scaling based on demand
- [ ] Load balanced traffic verified (visit LB DNS)
- [ ] Route 53 domain configured (if applicable)

## 🛠️ Tools & Technologies

- AWS EC2: Compute service
- Auto Scaling: Dynamic capacity management
- Elastic Load Balancer: ALB/NLB for load distribution
- CloudWatch: Monitoring and metrics
- Route 53: DNS service
- AWS Management Console: Web UI for configuration
- SSH: For instance management

## 📚 Key Learnings

1. **Elasticity**: Applications automatically scale to meet demand
2. **High Availability**: Multiple AZs ensure fault tolerance
3. **Cost Optimization**: Resources scale down when not needed
4. **Load Distribution**: ELB ensures even traffic distribution
5. **Self-Healing**: ASG automatically replaces failed instances
6. **Monitoring**: CloudWatch metrics drive scaling decisions

## ⚠️ Important Considerations

- Keep at least 1 instance running (per min capacity)
- ASG waits after scaling to prevent rapid fluctuations
- Ensure your AMI has all necessary software
- Allow inbound traffic on required ports (80, 443, SSH)
- Ensure instances have permissions for CloudWatch
- Monitor AWS costs as scaling can increase expenses
- Test scaling policies in non-production first

## 📖 References

- [AWS EC2 Auto Scaling Documentation](https://docs.aws.amazon.com/autoscaling/)
- [Elastic Load Balancer Documentation](https://docs.aws.amazon.com/elasticloadbalancing/)
- [Route 53 Documentation](https://docs.aws.amazon.com/route53/)
- [CloudWatch Documentation](https://docs.aws.amazon.com/cloudwatch/)
- [VPC & Networking](https://docs.aws.amazon.com/vpc/)

## 👤 Author

**Sai Teja** - Cloud Computing Learner  
Assignment: ELB, Auto Scaling Group (ASG), and Route 53 Integration  
Date: January 2026

---

*This assignment demonstrates practical implementation of auto-scaling and load balancing in AWS, core skills for cloud architecture and DevOps.*
