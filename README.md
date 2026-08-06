# 🚀 Secure Amazon RDS (MySQL 8.4) Connection from Amazon EC2 using SSL/TLS

A production-inspired AWS hands-on project demonstrating how to securely connect an Amazon EC2 instance to an Amazon RDS MySQL database using SSL/TLS encryption. This project focuses on AWS networking, database security, secure connectivity, and encrypted communication.

---

# 📌 Project Overview

In this project, I configured a secure connection between an Ubuntu EC2 instance and an Amazon RDS MySQL 8.4 database inside AWS. I implemented networking, Security Group configuration, SSL certificate validation, and verified encrypted database communication using the MySQL client.

---

# 🛠️ AWS Services & Technologies Used

- Amazon EC2 (Ubuntu)
- Amazon RDS (MySQL 8.4)
- Amazon VPC
- AWS Security Groups
- MySQL Client
- Linux (Ubuntu)
- SSL/TLS
- AWS Root CA Certificate

---

# 🏗️ Architecture

The Amazon EC2 instance and Amazon RDS MySQL database were deployed inside the same AWS VPC.

Database connectivity was secured by allowing MySQL (Port 3306) access **only from the EC2 Security Group**, instead of exposing the database to the internet using `0.0.0.0/0`.

Database traffic between EC2 and RDS travels through AWS networking while SSL/TLS encrypts the communication between the client and the database server.

```
                Amazon VPC
+---------------------------------------------+

        EC2 (Ubuntu)
      MySQL Client Installed
               │
               │
      Port 3306 (MySQL)
               │
      Security Group
 (Only EC2 SG Allowed)
               │
               ▼
      Amazon RDS MySQL 8.4

+---------------------------------------------+
```

---

# 🔐 Security Group Configuration

The RDS Security Group was configured using AWS Security Best Practices.

### Inbound Rule

| Type | Source |
|------|--------|
| MySQL/Aurora (3306) | EC2 Security Group |

### Why this approach?

- Restricts database access to the EC2 instance only.
- Prevents unnecessary public access using `0.0.0.0/0`.
- Continues working even if the EC2 private IP changes after stop/start because the rule references the Security Group instead of an IP address.

---

# 🔒 SSL/TLS Secure Connection

To encrypt data in transit, I downloaded the AWS Root CA certificate on the EC2 instance and configured MySQL to verify the server identity before establishing the connection.

## Download AWS Root CA Certificate

```bash
wget https://truststore.pki.rds.amazonaws.com/global/global-bundle.pem
```

---

## Connect to Amazon RDS using SSL

```bash
mysql \
-h pavan-mysql-rds.c7u8qkg00da6.ap-south-1.rds.amazonaws.com \
-P 3306 \
-u pavan_admin \
-p \
--ssl-mode=VERIFY_IDENTITY \
--ssl-ca=./global-bundle.pem
```

Using **VERIFY_IDENTITY** ensures that:

- The server certificate is valid.
- The certificate matches the actual RDS endpoint.
- The client is protected against Man-in-the-Middle (MITM) attacks.

---

# ✅ SSL Verification

Inside the MySQL shell:

```sql
STATUS;
```

Verified:

- SSL Enabled
- Cipher Suite

```
TLS_AES_128_GCM_SHA256
```

Also verified the authenticated user:

```sql
SELECT USER(), CURRENT_USER();
```

---

# 💻 Linux & MySQL Commands Used

```bash
wget
mysql
nc -zv
ls
pwd
chmod
```

```sql
STATUS;
SELECT USER();
SELECT CURRENT_USER();
```

---

# 🎯 Skills Demonstrated

- Amazon EC2
- Amazon RDS
- Amazon VPC
- AWS Security Groups
- Linux Administration
- MySQL Client
- SSL/TLS Encryption
- Database Connectivity
- AWS Networking
- Cloud Security Best Practices

---

# 📸 Project Screenshots

### 1. Amazon RDS Dashboard

- RDS Instance Status
- MySQL Engine Version
- Database Availability

---

### 2. Security Group Configuration

- MySQL Port (3306)
- EC2 Security Group Access
- Secure Inbound Rule Configuration

---

### 3. SSL/TLS Verification

- MySQL STATUS Output
- TLS_AES_128_GCM_SHA256
- Secure Database Session

---

# 📚 Key Learnings

- Secure communication between Amazon EC2 and Amazon RDS.
- AWS Security Group configuration for database security.
- SSL/TLS implementation using AWS Root CA certificates.
- Identity verification using VERIFY_IDENTITY.
- Troubleshooting secure database connectivity.
- AWS networking best practices.

---

# 🏆 Project Outcome

Successfully established a secure SSL/TLS encrypted connection between Amazon EC2 and Amazon RDS MySQL 8.4.

The encrypted connection was verified using the AWS Root CA certificate, VERIFY_IDENTITY mode, and TLS session validation.

This project strengthened my practical understanding of AWS networking, Linux administration, database security, and secure cloud architecture.
