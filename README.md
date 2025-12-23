\# 🏦 Bank Transaction Microservice – Secure AWS Architecture



\## Overview

This project demonstrates a secure AWS microservice architecture using:

\- Public \& Private EC2

\- Bastion Host

\- NAT Instance

\- CloudWatch

\- GuardDuty

\- Prowler Security Scanning



\## Architecture

\- Public EC2 acts as Bastion + NAT Instance

\- Private EC2 hosts the banking microservice and database

\- No direct internet access to sensitive workloads



\## Security

\- Network segmentation using VPC \& subnets

\- IAM hardening (MFA, no root keys)

\- Continuous security assessment with Prowler



