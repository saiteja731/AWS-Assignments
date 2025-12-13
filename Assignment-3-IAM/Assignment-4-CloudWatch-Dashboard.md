# Assignment 4: CloudWatch Dashboard Creation

## Problem Statement
Monitor EC2 instance performance by creating a CloudWatch dashboard that displays CPU utilization and network metrics.

## Tasks Performed

### Task 1: Launch EC2 Instance

**Instance Configuration:**
- **Name**: `demoEc2`
- **AMI**: Amazon Linux 2
- **Instance Type**: t3.micro (Free tier eligible)
- **Security Group**: Allow SSH and HTTP traffic

#### Steps:
1. Navigate to EC2 → Launch Instances
2. Select Amazon Linux 2 AMI
3. Choose t3.micro instance type
4. Configure security group to allow HTTP and SSH
5. Launch the instance
6. Note the Instance ID for dashboard creation

### Task 2: Create CloudWatch Dashboard

**Dashboard Name**: `demoEc2-dashboard`

#### Steps:
1. Navigate to CloudWatch → Dashboards
2. Click "Create dashboard"
3. Enter dashboard name: `demoEc2-dashboard`
4. Click "Create dashboard"
5. Add widgets by clicking "+" button

### Task 3: Add Metrics Widgets

#### Widget 1: CPU Utilization
- **Widget Type**: Line chart
- **Metric**: EC2 → Per-Instance Metrics → CPU Utilization
- **Instance**: Select demoEc2 instance
- **Time Range**: 1 hour
- **Statistics**: Average

#### Widget 2: Network Metrics
Create multiple widgets for:
- **NetworkIn**: Data coming into the instance
- **NetworkOut**: Data leaving the instance
- **NetworkPacketsIn**: Incoming packets
- **NetworkPacketsOut**: Outgoing packets

#### Steps to Add Widgets:
1. Click "+" to add widget
2. Select widget type (Line chart for metrics)
3. Click "Add metric"
4. Browse metrics:
   - Select EC2 namespace
   - Search for instance ID
   - Select specific metrics
5. Customize:
   - Set time range
   - Configure statistics (Average, Sum, Maximum)
   - Add title
6. Click "Create widget"

### Task 4: Generate Metrics Data

To see meaningful graphs on the dashboard:

#### Apply Load to Instance:
```bash
# SSH into the EC2 instance
ssh -i your-key.pem ec2-user@instance-public-ip

# Apply CPU stress
sha1sum /dev/zero

# This will generate CPU utilization metrics
```

#### Monitor Network Activity:
```bash
# Generate network traffic
ping google.com

# Or download files to generate network metrics
wget large-file-url
```

## Dashboard Layout

```
┌─────────────────────────────────────┐
│  demoEc2-dashboard                    │
├─────────────────────────────────────┤
│                CPU Utilization      │
│  ┌──────────────────────────────────┐  │
│  │ Line Chart (%) vs Time            │  │
│  └──────────────────────────────────┘  │
├─────────────────────────────────────┤
│         Network Metrics          │
│  ┌──────────────────────────────────┐  │
│  │ NetworkIn/Out (Bytes) vs Time │  │
│  └──────────────────────────────────┘  │
└─────────────────────────────────────┘
```

## CloudWatch Metrics Explained

### CPU Utilization
- **Description**: Percentage of CPU capacity used
- **Range**: 0% - 100%
- **Unit**: Percent
- **Typical Threshold**: Alert if > 80%

### Network Metrics
| Metric | Description | Unit |
|--------|-------------|------|
| NetworkIn | Incoming bytes | Bytes |
| NetworkOut | Outgoing bytes | Bytes |
| NetworkPacketsIn | Incoming packet count | Count |
| NetworkPacketsOut | Outgoing packet count | Count |

## Dashboard Best Practices

1. **Time Range**: Set appropriate time windows for your use case
2. **Aggregation**: Use Average for usage trends, Sum for throughput
3. **Thresholds**: Set visual thresholds for alerting conditions
4. **Labeling**: Add descriptive titles to each widget
5. **Refresh**: Set auto-refresh intervals (1 min, 5 min, etc.)

## Monitoring Benefits

- **Real-time Visibility**: Monitor instance performance in real-time
- **Trend Analysis**: Identify usage patterns and peak times
- **Capacity Planning**: Use historical data for scaling decisions
- **Troubleshooting**: Correlate application issues with resource metrics
- **Cost Optimization**: Monitor underutilized resources

## Next Steps

1. Add more instances to dashboard for comparison
2. Set up alarms for critical thresholds
3. Create custom metrics for application-specific monitoring
4. Configure SNS notifications for alarm triggers
