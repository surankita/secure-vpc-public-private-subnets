 Overview
The goal of this project is to design and implement a secure Virtual Private Cloud (VPC) architecture with both public and private subnets. The public subnet hosts a Bastion Host, which acts as a controlled entry point, while the private subnet hosts EC2 instances that are not directly accessible from the internet. This setup ensures that sensitive workloads remain protected, with access restricted through the Bastion Host. 
By configuring Security Groups, routing rules, and Instance Metadata Service v2 (IMDSv2), the project demonstrates secure connectivity, proper isolation of resources, and verification of private instance details. This architecture is a foundational CloudOps practice for building secure environments in AWS.

Architecture Diagram
The project follows a secure VPC design with both public and private subnets:

-Local PC** → initiates SSH connection using the correct `.pem` key.
- **Bastion Host (Public Subnet)** → acts as the controlled entry point, accessible from the internet.  
  - Security Group allows inbound SSH (port 22) from trusted IPs.  
  - Outbound rules permit access to the private subnet.  
- **Private EC2 (Private Subnet)** → hosts sensitive workloads, not directly exposed to the internet.  
  - Security Group only allows inbound SSH from the Bastion Host’s Security Group.  
  - Verified using IMDSv2 metadata queries (private IP and security group).  

 Flow Representation
Local PC
│
▼
Bastion Host (Public Subnet, SG allows SSH from your IP)
│
▼
Private EC2 (Private Subnet, SG allows SSH only from Bastion SG)

This architecture ensures that private workloads remain isolated and secure, with controlled access through the Bastion Host.
## Verification Outputs

To confirm secure connectivity and proper isolation of the Private EC2 instance, the following commands were executed inside the instance:

```bash
# Check hostname
hostname
# Output:
ip-10-0-2-176.ec2.internal

# Check uptime
uptime
# Output:
16:18:53 up 3:52, 1 user, load average: 0.03, 0.03, 0.00

# Query private IP using IMDSv2
TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" \
  -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")
curl -H "X-aws-ec2-metadata-token: $TOKEN" \
  http://169.254.169.254/latest/meta-data/local-ipv4
# Output:
10.0.2.176

# Query security group using IMDSv2
curl -H "X-aws-ec2-metadata-token: $TOKEN" \
  http://169.254.169.254/latest/meta-data/security-groups
# Output:
launch-wizard-1

Conclusion

This project successfully demonstrates the design and implementation of a secure VPC architecture with both public and private subnets. By using a Bastion Host in the public subnet, access to private workloads is tightly controlled and monitored. The Private EC2 instance remains isolated from direct internet exposure, ensuring enhanced security and compliance with best practices.

Through the use of Security Groups, proper key pair management, and IMDSv2 metadata queries, the project validates secure connectivity and resource isolation. The workflow highlights essential CloudOps skills such as networking, secure access management, and documentation. 

This project forms a strong foundation for advanced AWS CloudOps practices and serves as a showcase of secure infrastructure design for recruiters and portfolio development.



