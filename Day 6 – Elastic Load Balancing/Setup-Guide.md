## Industrial Setup Standard – Step-by-Step Solution
**Architecture Overview**

The solution architecture includes:
- 2 EC2 web servers
- Public subnets across availability zones
- Application Load Balancer
- Target group for traffic routing
- Health checks for automatic failure detection
Traffic Flow:<br/>
```
User → Application Load Balancer → EC2 Instances
```
This ensures traffic is automatically distributed and unhealthy servers are removed from rotation.

**LAB 1 – Create Application Load Balancer (ALB)** <br/>
**Step 1 – Navigate to Load Balancer Service**

- Log in to AWS Console
- Search for EC2
- Scroll to the left navigation panel
- Under Load Balancing, click Load Balancers

**Step 2 – Create Load Balancer**
- Click Create Load Balancer
- Select Application Load Balancer
- Click Create

**Step 3 – Configure Load Balancer - Basic Configuration**
- Name: ``` web-app-alb ```
- Scheme: ``` Internet-facing ```
- IP Address Type: ``` IPv4 ```
- **Network Mapping**
  - Select your VPC & choose two public subnets from different availability zones for high availability.
      - Example Public Subnet 1 (AZ-A) & Public Subnet 2 (AZ-B)
- **Security Groups**
   - Create or select a security group allowing HTTP traffic.
   ```
   | Type | Port | Source    |
     HTTP | 80   | 0.0.0.0/0 |
   This allows users to access the web application.
   ```
- **Listeners**
   - Create or select a security group allowing HTTP traffic.
     Ensure the following listener exists:
     ```
     HTTP : 80
     ```
- Proceed to Target Group creation.<br/>
**Outcome** <br/>
The load balancer is created and ready to distribute traffic.

**LAB 2 – Add Target Groups**<br/>
Target groups define the backend servers that receive traffic from the load balancer.

**Step 1 – Create Target Group** <br/>
In the ALB setup wizard:
- Click: ``` Create target group ```
- Configuration:
  - Target Type: ``` Instance ```
  - Name: ``` web-target-group ```
  - Protocol: ``` HTTP ```
  - Port: ``` 80 ```
- Select your VPC.
- Click Next

**Step 2 – Register Targets**<br/>
- Select your EC2 web servers.
i.e:
``` 
web-server-1
web-server-2
```
- Click:
``` Include as pending below ```
- Then click:
``` Create target group ``` <br/>

**Outcome** <br/>
The target group now contains the backend EC2 instances.

**LAB 3 – Configure Health Checks** <br/>
Health checks allow the load balancer to automatically detect unhealthy instances.

**Step 1 – Open Target Groups**
- Navigate to:
  ``` EC2 → Target Groups ```
- Select:
  ``` web-target-group ```

**Step 2 – Configure Health Check**
- Click:
  ``` Health checks → Edit ```
- Configuration:
- Protocol:
  ``` HTTP ```
- Path: ``` / ```
- Advanced settings:
``` 
  Healthy threshold: 3
  Unhealthy threshold: 3
  Timeout: 5 seconds
  Interval: 30 seconds
```
- Save changes.

**Outcome** <br/>
The load balancer can detect server failures automatically.

**LAB 4 – Test Load Balancing** <br/>
**Step 1 – Get ALB DNS Name**
- Navigate to:
  ``` EC2 → Load Balancers ```
- Select:
  ``` web-app-alb ```
- Copy the DNS name.
i.e
``` web-app-alb-123456.us-east-1.elb.amazonaws.com ```

**Step 2 – Access the Application**
- Open a browser and visit:
  ``` http://<ALB-DNS-NAME> ```
- Refresh the page several times.
- You should see responses from different instances.
- For example, output from web servers:
  ```
       Server 1
       Server 2
  ```
**Step 3 – Test Fault Tolerance**
- Stop one EC2 instance:
  ``` EC2 → Instances → Stop Instance ```
- Observe:
  ``` Target Groups → Health Status ```
- The stopped instance becomes Unhealthy, and traffic automatically routes to the remaining server.

**Outcome**
The load balancer successfully distributes traffic and removes unhealthy servers.

**Final Project Outcome** <br>
By completing this project, I successfully implemented:
- Highly available web architecture
- Traffic distribution using Application Load Balancer
- Backend instance management using target groups
- Automatic failure detection using health checks
- Fault-tolerant application infrastructure

This architecture is widely used in production SaaS and enterprise cloud environments.
