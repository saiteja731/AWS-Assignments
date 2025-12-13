# Assignment 5: CloudWatch Alarms and Notifications

## Problem Statement
Set up proactive monitoring with CloudWatch alarms to detect billing overages and EC2 resource utilization issues, with SNS notifications for immediate alerting.

## Tasks Performed

### Task 1: Create Billing Alarm (Threshold: $500)

#### Prerequisites:
- Enable Billing Alerts in AWS Billing console
- Verify your email for SNS subscriptions

#### Steps:
1. Navigate to CloudWatch → All Alarms
2. Click "Create Alarm"
3. **Specify Metric:**
   - Search metric: Billing
   - Select: Total Estimated Charges (USD)
   - Currency: USD
4. **Set Conditions:**
   - Threshold type: Static
   - Whenever EstimatedCharges is: Greater than 500
   - Period: 6 hours
5. **Configure Actions:**
   - Alarm state trigger: In alarm
   - Send notification to SNS topic
   - Create new topic: `CloudWatchBillingAlarm`
   - Email address: your-email@example.com
6. **Add Alarm Details:**
   - Alarm name: `Billing-Threshold-Alert`
   - Alarm description: "Alert when estimated charges exceed $500"
7. Review and create alarm

#### SNS Confirmation:
- Check email inbox for SNS subscription confirmation
- Click the confirmation link to activate notifications

### Task 2: Create CPU Utilization Alarm for EC2

**Alarm Configuration:**
- **Instance**: demoEc2
- **Metric**: CPU Utilization
- **Threshold**: 65%
- **Period**: 5 minutes

#### Steps:
1. Navigate to CloudWatch → All Alarms
2. Click "Create Alarm"
3. **Specify Metric:**
   - Search for EC2 instance: demoEc2
   - Select Per-Instance Metrics
   - Choose: CPU Utilization
4. **Set Conditions:**
   - Threshold type: Static
   - Whenever CPU Utilization is: Greater than 65
   - Period: 5 minutes
   - Datapoints to alarm: 1 out of 1
5. **Configure Actions:**
   - Alarm state trigger: In alarm
   - Send notification to: Create new SNS topic
   - Topic name: `EC2-CPU-Alert`
   - Email: your-email@example.com
6. **Add Alarm Details:**
   - Alarm name: `CPU-Utilization-High`
   - Alarm description: "Alert when CPU exceeds 65%"
7. Review and create alarm

## Alarm Architecture

```
┌─────────────────────────────────────┐
│  CloudWatch Metrics                  │
├──────────┬──────────────────────────┘
│     Billing     │   CPU Utilization      │
└──────────┴──────────────────────────┘
           │              │
           ▼              ▼
      ┌─────────┐  ┌─────────┐
      │ Alarm 1     │  │ Alarm 2     │
      │ ($500)      │  │ (>65%)      │
      └─────────┘  └─────────┘
           │              │
           ▼              ▼
      ┌─────────────────────┐
      │ SNS Topics (Notifications)     │
      │ ├─ CloudWatchBillingAlarm      │
      │ └─ EC2-CPU-Alert               │
      └─────────────────────┘
           │
           ▼
      ┌─────────┐
      │ Email Alert │
      └─────────┘
```

## Alarm States

### Alarm State Transitions

| State | Condition | Action |
|-------|-----------|--------|
| **OK** | Metric within threshold | No notification |
| **ALARM** | Metric exceeds threshold | Send SNS notification |
| **INSUFFICIENT_DATA** | Not enough data points | No action (initial state) |

## Testing the Alarms

### Test Billing Alarm:
- Verify SNS email subscription is confirmed
- Create some billable resources (EC2 instances, S3 storage)
- Alarm will trigger when estimated charges reach $500

### Test CPU Alarm:
1. SSH into demoEc2 instance:
```bash
ssh -i your-key.pem ec2-user@instance-public-ip
```

2. Generate CPU load:
```bash
# Run CPU-intensive process
sha1sum /dev/zero

# Monitor CPU utilization
top
```

3. Watch CloudWatch metrics in real-time
4. Alarm should trigger when CPU > 65% for 5 minutes
5. Check email for SNS notification

## Alarm Best Practices

1. **Threshold Selection**: 
   - CPU: 65-80% depending on workload
   - Memory: 80-90% for alerts
   - Billing: Set based on budget

2. **Period Configuration**:
   - CPU: 5 minutes (quick response)
   - Billing: 6 hours (trends over time)
   - Network: 1 minute (DDoS detection)

3. **Notification Strategy**:
   - Critical alerts: Multiple channels (email + SMS + Slack)
   - Warning alerts: Email only
   - Info alerts: CloudWatch Logs

4. **Alarm Naming**:
   - Include metric name: "CPU-Utilization-High"
   - Include threshold: "CPU-80-percent"
   - Include resource: "Production-Web-Server"

## Alarm Troubleshooting

### Alarm Not Triggering:
- Verify metric is being collected
- Check alarm threshold vs actual metric values
- Confirm SNS topic subscriptions are confirmed
- Check CloudTrail for alarm events

### Too Many Notifications:
- Increase threshold value
- Increase period duration
- Implement alarm actions instead of notifications
- Use SNS topic filtering

## Integration with Other Services

### SNS to Slack:
- Create Lambda function to transform SNS → Slack
- Subscribe Lambda to SNS topic
- Post formatted alerts to Slack channel

### SNS to Email:
- Direct SNS email subscription
- Requires email confirmation
- Supports HTML and plain text

### SNS to Lambda:
- Trigger auto-remediation functions
- Scale resources based on metrics
- Create tickets in incident management systems

## Next Steps

1. **Auto-Scaling**: Trigger scaling policies from alarms
2. **Advanced Notifications**: Integrate with Slack, PagerDuty
3. **Custom Metrics**: Create application-specific alarms
4. **Composite Alarms**: Combine multiple metrics
5. **Anomaly Detection**: Use ML-based thresholds
