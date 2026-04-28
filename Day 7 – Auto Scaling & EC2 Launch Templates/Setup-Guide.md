## Industrial Setup Standard – Step-by-Step Solution

**LAB 1 – Create Launch Template** <br/>
**Step 1 – Navigate to Launch Templates**
- AWS Console → EC2
- Left menu → Launch Templates
- Click Create launch template

**Step 2 – Configure Template**
- Name: ```web-launch-template```
- AMI: ```Amazon Linux 2```
- Instance type: ```t2.micro```
- Key pair:: ```Select existing key```

**Network Settings** <br/>
- Security group: Use your web server SG (HTTP allowed)

**Advanced → User Data (Optional)** <br/>
- Install a simple web server:
```
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "Hello from $(hostname)" > /var/www/html/index.html
```
- Click Create launch template 

**Outcome**<br/>
Reusable template for consistent EC2 deployments

**LAB 2 – Configure Auto Scaling Group** <br/>
**Step 1 – Create ASG**<br/>
1. EC2 → Auto Scaling Groups
2. Click Create Auto Scaling group

**Configuration**
- Name: ```web-asg```
- Launch template: Select ```web-launch-template```

**Network**
- VPC: Your VPC
- Select at least 2 public subnets (multi-AZ)

**Group Size**
- Desired: 2
- Minimum: 2
- Maximum: 4

**Scaling Policy**
- Select: ```Target tracking scaling policy```
- Metric: ```Average CPU utilization```
- Target Value: ```50%```

**Outcome**
Auto Scaling Group automatically adjusts capacity

**LAB 3 – Test Scaling by Load <br/>
Step 1 – Generate Load**

Use a browser or tool:
- Refresh ALB URL continuously
OR
- Use a load tool (e.g., Apache Benchmark)

**Step 2 – Monitor Scaling**<br/>
- Go to:```EC2 → Auto Scaling Groups → Activity```
- Observe: - New instances launched when CPU increases

**Outcome**<br/>
System scales out automatically under load

**LAB 4 – Integrate with ALB
Step 1 – Attach ASG to Target Group** <br/>
1. Go to Auto Scaling Group
2. Edit → Load balancing
- Select: ```Attach to existing load balancer```
- Choose: ```web-target-group (from Day 6)```
- Save Changes

**Step 2 – Verify**<br/>
- Go to ALB DNS
- Refresh multiple times
- Stop one instance → ASG replaces it

**Outcome**<br/>
Fully integrated auto-scaling + load-balanced architecture

**Final Project Outcome**<br/>
I have implemented:
- Auto Scaling Group with dynamic scaling
- Launch Templates for consistency
- Multi-AZ high availability
- ALB integration
- Fault tolerance + cost optimization
