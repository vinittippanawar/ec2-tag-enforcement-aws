# 🚀 EC2 Tag Enforcement Using IAM Policy on AWS

<p align="center">
  <img src="https://img.shields.io/badge/AWS-Cloud-orange?style=for-the-badge&logo=amazonaws" />
  <img src="https://img.shields.io/badge/IAM-Security-blue?style=for-the-badge&logo=amazonaws" />
  <img src="https://img.shields.io/badge/EC2-Compute-FF9900?style=for-the-badge&logo=amazonaws" />
  <img src="https://img.shields.io/badge/Policy-Governance-green?style=for-the-badge" />
</p>

---

## 📌 Project Overview

This project demonstrates how to enforce **mandatory tagging on EC2 instances** using **IAM policies** in AWS.

In many organizations, EC2 instances are launched without proper tags, leading to:
- Billing issues
- Lack of ownership tracking
- Poor governance

This project ensures that:

> ❌ EC2 instances **cannot be launched without required tags**  
> ✅ EC2 instances **launch successfully only when all tags are provided**

---

## 🎯 Objective

The main objective of this project is to enforce **tag-based governance** for EC2 instances.

### Key Goals:
- Prevent EC2 launch without mandatory tags
- Ensure proper cost allocation
- Track resource ownership
- Implement IAM-based policy enforcement
- Demonstrate real-world cloud governance

---

## 🏗️ Architecture

### High-Level Flow

```text
IAM User → EC2 Launch Request
        ↓
IAM Policy Validation
        ↓
✔ If tags present → Instance Launch Allowed
❌ If tags missing → Launch Denied

```
