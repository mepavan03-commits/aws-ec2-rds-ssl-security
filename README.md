🚀 Secure Amazon RDS (MySQL 8.4) Connection from EC2 using SSL/TLS

A production-inspired AWS hands-on project demonstrating how to securely connect an Amazon EC2 instance to an Amazon RDS MySQL database using SSL/TLS encryption. This project focuses on AWS networking, security, database connectivity, and encrypted communication.

📌 Project Overview

In this project, I configured a secure connection between an Ubuntu EC2 instance and an Amazon RDS MySQL 8.4 database inside AWS. I implemented networking, security group configuration, SSL certificate validation, and verified encrypted database communication using the MySQL client.

🛠️ AWS Services & Technologies Used

Amazon EC2 (Ubuntu)

Amazon RDS (MySQL 8.4)

Amazon VPC (same VPC for EC2 and RDS)

Security Groups

MySQL Client

AWS Root CA Certificate (SSL/TLS)

🏗️ Architecture

Both the EC2 instance and the RDS database were placed inside the same VPC. RDS was kept without public access, so the database is only reachable from within the private network — not from the public internet.



EC2 (Ubuntu, private subnet) → Security Group (port 3306) → RDS MySQL (private, same VPC)

Because both resources are in the same VPC, the actual database traffic travels over AWS's internal private network rather than the public internet. Internet access was only needed once — to download the AWS Root CA certificate used for the SSL connection.

🔐 Security Group Configuration

The RDS security group's inbound rule was restricted to the EC2 instance's Security Group ID, instead of allowing any specific IP or opening the port to the public (0.0.0.0/0).

Why this approach:



Blocks all public internet access to port 3306

Keeps working even if the EC2 instance's private IP changes after a stop/start, since it references the Security Group rather than a fixed IP

TypeSourceMySQL/Aurora (Inbound)EC2 Security Group IDOutbound0.0.0.0/0 (default, allows RDS to reach out for updates)

🔒 SSL/TLS Setup & Connection

To encrypt data in transit, I downloaded AWS's Root CA bundle on the EC2 instance and used it to enforce a verified, encrypted connection to RDS.

1. Download AWS's Root CA certificate:
wget https://truststore.pki.rds.amazonaws.com/global/global-bundle.pem

2. Connect to RDS with SSL enforced:
mysql -h pavan-mysql-rds.c7u8qkg00da6.ap-south-1.rds.amazonaws.com \
-P 3306 -u pavan_admin -p \
--ssl-mode=VERIFY_IDENTITY \
--ssl-ca=./global-bundle.pem

VERIFY_IDENTITY makes the client verify that the server's certificate is valid and actually matches the RDS endpoint being connected to, so the connection can't be silently redirected to a different server.


STATUS;

This confirmed the session was using cipher TLS_AES_128_GCM_SHA256 and connecting through port 3306 over the RDS endpoint.





🎯 Summary

I deployed an Amazon RDS MySQL instance, restricted access to it using Security Groups instead of public IP rules, and connected to it from an EC2 instance using an SSL/TLS-encrypted connection verified with VERIFY_IDENTITY m
