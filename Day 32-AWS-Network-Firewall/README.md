# Day 40 – AWS Network Firewall

## Project Goal

To deploy AWS Network Firewall with stateless and stateful inspection rules for centralized VPC traffic filtering and inspection.

## Services Used

- AWS Network Firewall
- Amazon VPC
- Route Tables
- EC2
- Firewall Policies
- Stateless Rule Groups
- Stateful Rule Groups

## Outcome

A managed network inspection architecture was implemented, providing deeper traffic visibility, policy enforcement, and layered protection for VPC traffic flows.

## Key Learning

- Network Firewall adds deeper inspection beyond SGs/NACLs.
- Stateless rules inspect packets individually.
- Stateful rules inspect flows.
- Routing must steer traffic through firewall endpoints.
