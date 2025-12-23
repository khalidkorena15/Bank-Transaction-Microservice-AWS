🏦 Bank Transaction Microservice – Secure AWS Architecture Project



📌 Project Overview

This project implements a secure bank transaction microservice deployed on AWS using a public and private EC2 architecture, following enterprise‑grade security best practices.

The solution is designed to isolate sensitive workloads, enforce network segmentation, and continuously monitor security posture using AWS-native services and open‑source security tools.



🏗️ Architecture Design



🌐 Networking (VPC \& Subnets)



VPC with network segmentation



Public Subnet



Hosts a Public EC2 (Amazon Linux)



Private Subnet



Hosts a Private EC2 (Ubuntu)



Hosts the database inside the private EC2 for maximum isolation



🖥️ Compute Layer



🔹 Public EC2 – Amazon Linux (Bastion / Gateway)



Located in a public subnet



Has a public IP



Acts as:



Bastion host for secure SSH access



Gateway for outbound internet access for the private EC2



Used for:



SSH ProxyJump to the private EC2



Secure file transfer (SCP)



Temporary storage of security scan results



Inbound access is strictly limited to SSH from trusted IPs



🔹 Private EC2 – Ubuntu (Transaction Microservice + Database)



Located in a private subnet



No public IP



Hosts:



Bank transaction microservice (API)



Database (inside the private EC2)



Securely pulls application source code from GitHub



Has outbound‑only internet access, routed through the public EC2



Fully isolated from direct internet exposure



🔐 Security \& Monitoring



🛡️ Prowler Security Scanning



Prowler runs on the private EC2



Scans AWS services:



EC2



VPC



IAM



Generates reports in:



HTML



CSV



Workflow:



Prowler generates results on the private EC2



Results are copied to the public EC2



Final reports are securely transferred to the local laptop



HTML reports are used for:



Security analysis



Email sharing



Portfolio and documentation



📊 Amazon CloudWatch



Enabled on both EC2 instances



Monitors:



CPU utilization



Memory usage



Network traffic



Instance health



Provides real‑time visibility into system performance and availability



🚨 Amazon GuardDuty



Enabled at the AWS account level



Continuously analyzes:



VPC Flow Logs



CloudTrail logs



DNS activity



Detects:



Suspicious API calls



Potential intrusions



Compromised instances



Findings are reviewed and correlated with Prowler results



🔁 Secure Traffic Flow



Inbound: Internet → Public EC2 only



Administrative Access: Local Machine → Public EC2 → Private EC2 (SSH ProxyJump)



Outbound: Private EC2 → Public EC2 → Internet



Database Access: Internal only (inside private EC2)



🔧 Architectural Decisions \& Free Tier Considerations



While designing this architecture, I intentionally balanced security, cost efficiency, and AWS Free Tier limitations.



Although AWS provides more scalable and fully managed services for production environments, some services were not used due to cost constraints, while still maintaining a secure and well‑architected design.



Examples of production‑grade alternatives:



NAT Gateway



Not used due to hourly and data processing costs



Instead, the public EC2 acts as a controlled outbound gateway for the private EC2



This approach maintains outbound connectivity while staying within the Free Tier



Application Load Balancer (ALB)



Not implemented to avoid additional costs



In production, ALB would provide:



High availability



Health checks



Secure HTTPS traffic distribution



Amazon RDS



Database is hosted inside the private EC2 for simplicity and cost control



In production, RDS in private subnets would be preferred for:



Automated backups



Multi‑AZ availability



Managed patching and scaling



Auto Scaling Groups



Not enabled to remain within Free Tier limits



Production systems would benefit from automatic scaling and self‑healing



✅ Key Security Benefits



No direct internet access to sensitive banking workloads



Strong isolation using public \& private subnets



Secure SSH access via bastion host



Continuous monitoring with CloudWatch



Threat detection with GuardDuty



Automated security posture assessment with Prowler



Architecture aligned with the AWS Well‑Architected Framework – Security Pillar.





💬 I’d love to hear feedback or suggestions for further improvement, especially around scalability, automation, or additional security hardening.



\#AWS #CloudSecurity #DevOps #CyberSecurity #EC2 #VPC #IAM #Prowler #GuardDuty #CloudWatch #Portfolio

