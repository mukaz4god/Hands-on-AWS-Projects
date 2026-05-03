# Day 40 – AWS Network Firewall

# Interview Ready Wording

## Question: What is AWS Network Firewall?

**Answer:**  
AWS Network Firewall is a managed firewall service that provides centralized traffic inspection and filtering for VPC traffic using stateless and stateful rules.

---

## Question: What is the difference between stateless and stateful firewall rules?

**Answer:**  
Stateless rules evaluate packets individually without tracking connection state. Stateful rules inspect traffic flows and can make decisions based on session context and deeper packet inspection.

---

## Question: Why use Network Firewall if you already have Security Groups and NACLs?

**Answer:**  
Security Groups and NACLs provide foundational network filtering, but Network Firewall adds centralized inspection, deeper rule logic, stateful analysis, and more advanced traffic filtering across routed VPC paths.

---

## Question: What is a common mistake when deploying Network Firewall?

**Answer:**  
A common mistake is creating the firewall but not updating route tables to steer traffic through the firewall endpoint. Without routing changes, traffic will bypass inspection.
