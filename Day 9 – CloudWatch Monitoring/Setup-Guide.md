# Industrial Setup Standard – Step-by-Step Solution

**LAB 1 – Enable EC2 Detailed Monitoring**<br/>

**Step 1 – Navigate to EC2**<br/>
- AWS Console → EC2
- Click Instances
- Select your EC2 instance

**Step 2 – Enable Detailed Monitoring**<br/>
- Click Actions
- Select: ```Monitor and troubleshoot → Manage detailed monitoring```
- Click Enable

**Outcome**
Metrics are now collected at 1-minute intervals (instead of 5 minutes)

**LAB 2 – Create CloudWatch Alarm**<br/>

**Step 1 – Navigate to CloudWatch**<br/>
- AWS Console → CloudWatch
- Click Alarms
- Click Create alarm

**Step 2 – Select Metric**<br/>
- Click Select metric
- Navigate: ```EC2 → Per-Instance Metrics```
- Select: ```CPUUtilization```
- Click Metric

**Step 3 – Configure Alarm**<br/>
- Threshold: ```Greater than 70%```
- Period: ```1 minute```
- Evaluation: ```2 consecutive periods```

**Step 4 – Configure SNS Notification**<br/>
- Click Create new topic
- Name: ```cloudwatch-alerts```
- Add your email address
- Confirm subscription from email

**Step 5 – Complete Alarm**<br/>
- Name: ```High-CPU-Alarm```
- Click Create alarm

**Outcome**<br/>
System will alert when CPU exceeds threshold

**LAB 3 – Create CloudWatch Dashboard**<br/>

**Step 1 – Create Dashboard**<br/>
- CloudWatch → Dashboards
- Click Create dashboard
  - Name: ```web-app-dashboard```

**Step 2 – Add Widgets**<br/>
- Add widget → Line graph
- Select: ```EC2 → CPUUtilization```
- Add additional metrics:
  - Network In/Out
  - Disk Read/Write
- Save dashboard

**Outcome**<br/>
Centralized visualization of system performance

**LAB 4 – Test Monitoring & Alerts**<br/>

**Step 1 – Generate CPU Load**<br/>
- SSH into EC2: ```stress --cpu 2 --timeout 300``` (or install stress if needed ```sudo amazon-linux-extras install epel -y && sudo yum install stress -y```) 

**Step 2 – Observe Alarm**<br/>
- CloudWatch → Alarms → Status changes to ALARM
- Check email → SNS notification received

**Step 3 – View Dashboard**
- CloudWatch → Dashboard
- Observe CPU spike visually

**Outcome**
- Monitoring system successfully detects and alerts on issues

**Final Project Outcome**<br/>

I implemented:<br/>
- Real-time monitoring using CloudWatch
- Alerting using SNS
- Performance dashboards
- Incident detection via alarms

