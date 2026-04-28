**Q: What is an Auto Scaling Group?**<br/>
**Answer:**
An Auto Scaling Group automatically adjusts the number of EC2 instances based on demand, ensuring high availability and cost efficiency by scaling out during peak traffic and scaling in during low usage.

Q: What is a Launch Template?<br/>
**Answer:**
A Launch Template defines EC2 configuration such as AMI, instance type, security groups, and user data, allowing consistent and repeatable instance deployment.

Q: How does scaling work with ALB?<br/>
**Answer:**
The ALB distributes traffic across instances in the Auto Scaling Group. As new instances are launched, they are automatically registered with the target group and begin receiving traffic.
