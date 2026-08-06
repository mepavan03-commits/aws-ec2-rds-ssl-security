## 🚀 Secure Amazon RDS (MySQL 8.4) Connection from EC2 using SSL/TLS

A production-inspired AWS hands-on project demonstrating how to securely connect an Amazon EC2 instance to an Amazon RDS MySQL database using SSL/TLS encryption. This project focuses on AWS networking, security, database connectivity, and encrypted communication.

---

## 📌 Project Overview

In this project, I configured a secure connection between an Ubuntu EC2 instance and an Amazon RDS MySQL 8.4 database inside AWS. I implemented networking, security group configuration, SSL certificate validation, and verified encrypted database communication using the MySQL client.

---

## 🛠️ AWS Services & Technologies Used

- Amazon EC2 (Ubuntu)
- Amazon RDS (MySQL 8.4)
- Amazon VPC
- Security Groups
- MySQL Client
- SSL/TLS Encryption
- Linux (Ubuntu)
- AWS CA Certificate Bundle

---

## ⚡ Project Architecture

```
EC2 (Ubuntu)
     │
     │ MySQL Client
     │
SSL/TLS Encrypted Connection
     │
Port 3306
     │
Security Group
     │
Amazon RDS (MySQL 8.4)
```

---

## 🔧 Implementation Steps

### 1. Amazon RDS Configuration

- Created an Amazon RDS MySQL 8.4 database.
- Configured networking inside the Default VPC.
- Configured database credentials.
- Verified database availability.

---

### 2. Network & Security Configuration

- Configured the RDS Security Group.
- Allowed MySQL traffic (Port 3306) only from the EC2 instance.
- Verified network connectivity between EC2 and RDS.

---

### 3. Connectivity Verification

Verified database reachability using:

```bash
nc -zv <RDS-ENDPOINT> 3306
```

This confirmed that Port 3306 was accessible from the EC2 instance.

---

### 4. SSL/TLS Configuration

- Downloaded the AWS CA Certificate Bundle (`global-bundle.pem`).
- Configured MySQL to use SSL encryption.
- Connected using:

```bash
mysql \
--host=<RDS-ENDPOINT> \
--user=pavan_admin \
--ssl-mode=VERIFY_IDENTITY \
--ssl-ca=global-bundle.pem
```

---

### 5. SSL Verification

Verified the encrypted session inside MySQL using:

```sql
STATUS;
```

Confirmed:

- SSL Enabled
- TLS Cipher:
  - `TLS_AES_128_GCM_SHA256`

Also verified the authenticated database user:

```sql
SELECT USER(), CURRENT_USER();
```

---

## 💻 Linux & MySQL Commands Used

```bash
nc -zv
wget
mysql
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

## 🎯 Skills Demonstrated

- Amazon RDS Administration
- Amazon EC2
- AWS Networking
- Amazon VPC
- Security Groups
- MySQL Connectivity
- SSL/TLS Encryption
- Linux Administration
- Database Security
- Cloud Troubleshooting

---

## 📸 Project Screenshots

### AWS RDS Dashboard

- RDS instance status
- MySQL Engine
- Database Availability

### Security Group Configuration

- Inbound Rule (Port 3306)
- Network Configuration

### SSL Verification

- MySQL STATUS Output
- Active TLS Cipher
- Secure Database Session

---

## 📚 Key Learnings

- Secure communication between EC2 and RDS
- Configuring AWS Security Groups
- Database networking inside AWS VPC
- SSL/TLS implementation for MySQL
- Identity verification using AWS CA certificates
- Troubleshooting database connectivity

---

## 🏆 Project Outcome

Successfully established a secure SSL/TLS encrypted connection between Amazon EC2 and Amazon RDS MySQL 8.4.

The database communication was verified using AWS CA certificates, encrypted TLS sessions, and MySQL status validation, following AWS security best practices for cloud database connectivity.
