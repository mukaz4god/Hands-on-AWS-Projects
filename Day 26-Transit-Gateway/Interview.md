# Day 34 – Transit Gateway

# Interview Ready Wording

## Question: Why use Transit Gateway instead of VPC peering?

**Answer:**  
Transit Gateway provides a centralized hub-and-spoke model for connecting multiple VPCs. It scales better than managing many point-to-point VPC peering connections and simplifies routing across large AWS environments.

---

## Question: What is the most important design requirement before connecting VPCs?

**Answer:**  
The VPC CIDR ranges must not overlap. Overlapping CIDRs cause routing conflicts and prevent reliable communication between networks.

---

## Question: What can break cross-VPC communication?

**Answer:**  
Common causes include missing VPC route table entries, missing Transit Gateway route propagation, restrictive Security Groups, restrictive NACLs, and overlapping CIDR ranges.

---

## Question: Where is Transit Gateway commonly used?

**Answer:**  
It is commonly used in enterprise AWS environments to connect multiple VPCs, shared services, inspection VPCs, on-premises networks, VPN, and Direct Connect.
