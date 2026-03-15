## Interview Ready Wording


**Question: What is the purpose of an Application Load Balancer?** <br/>
**Answer:** An Application Load Balancer distributes incoming HTTP or HTTPS traffic across multiple EC2 instances to improve application availability, scalability, and fault tolerance. It ensures that no single server becomes overloaded and automatically routes traffic only to healthy instances.

**Question: What are target groups in ALB?** <br/>
**Answer:** Target groups define the backend resources that receive traffic from the load balancer. These resources can include EC2 instances, containers, or IP addresses. Health checks monitor the targets and remove unhealthy instances from traffic routing.

**Question: Why are health checks important?** <br/>
**Answer:** Health checks allow the load balancer to continuously monitor the status of application servers. If a server fails or becomes unhealthy, the load balancer automatically stops sending traffic to that instance, ensuring high availability and reliability.
