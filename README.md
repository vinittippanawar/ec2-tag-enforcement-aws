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

## 🏷️ Mandatory Tags

- The following tags are required during EC2 launch:


| Tag Key | Example Value                             |
| ------- | ----------------------------------------- |
| Name    | Vinit                                     |
| emailID | [vinit@gmail.com](mailto:vinit@gmail.com) |
| phoneNo | 9876543210                                |
| Place   | Pune                                      |

---

## 🛠️ AWS Services Used
- AWS IAM (Identity and Access Management)
- Amazon EC2 (Elastic Compute Cloud)

---

## 🔐 IAM Policy Enforcement

The following IAM policy ensures that EC2 instances cannot be launched unless all required tags are provided.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowRunInstances",
      "Effect": "Allow",
      "Action": "ec2:RunInstances",
      "Resource": "*"
    },
    {
      "Sid": "AllowCreateTagsDuringLaunch",
      "Effect": "Allow",
      "Action": "ec2:CreateTags",
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "ec2:CreateAction": "RunInstances"
        }
      }
    },
    {
      "Sid": "DenyIfNameMissing",
      "Effect": "Deny",
      "Action": "ec2:RunInstances",
      "Resource": "arn:aws:ec2:*:*:instance/*",
      "Condition": {
        "Null": {
          "aws:RequestTag/Name": "true"
        }
      }
    },
    {
      "Sid": "DenyIfEmailMissing",
      "Effect": "Deny",
      "Action": "ec2:RunInstances",
      "Resource": "arn:aws:ec2:*:*:instance/*",
      "Condition": {
        "Null": {
          "aws:RequestTag/emailID": "true"
        }
      }
    },
    {
      "Sid": "DenyIfPhoneMissing",
      "Effect": "Deny",
      "Action": "ec2:RunInstances",
      "Resource": "arn:aws:ec2:*:*:instance/*",
      "Condition": {
        "Null": {
          "aws:RequestTag/phoneNo": "true"
        }
      }
    },
    {
      "Sid": "DenyIfPlaceMissing",
      "Effect": "Deny",
      "Action": "ec2:RunInstances",
      "Resource": "arn:aws:ec2:*:*:instance/*",
      "Condition": {
        "Null": {
          "aws:RequestTag/Place": "true"
        }
      }
    }
  ]
}
```

---

## 🚀 Implementation Steps

# ⭐ Step 1: Create IAM User
- Create IAM user: ec2-tag-user
- Enable console access
--- 
# ⭐ Step 2: Attach Policies

Attach:

- AmazonEC2FullAccess

- EC2-Tag-Enforcement (custom policy)
---
# ⭐ Step 3: Launch EC2 WITH Tags

- Add the following tags:
```
Name = Vinit
emailID = vinit@gmail.com
phoneNo = 9876543210
Place = Pune
```

✅ Result:

EC2 instance launches successfully.

---
# ⭐ Step 4: Launch EC2 WITHOUT Tags

Remove one tag (e.g., phoneNo)

❌ Result:

- Launch fails with authorization error
---

# 🧪 Test Results

| Test Case         | Result    |
| ----------------- | --------- |
| All tags provided | ✅ Success |
| One tag missing   | ❌ Failed  |
| No tags           | ❌ Failed  |

---

# 📸 Screenshots

1. IAM Policy Creation
   
  <img width="1854" height="1048" alt="Image" src="https://github.com/user-attachments/assets/60bd621c-2d79-42c2-8fc6-a3264350c922" />
  
---

2. IAM User Permissions

  <img width="1854" height="1048" alt="Image" src="https://github.com/user-attachments/assets/cd158228-361e-4587-a221-d3d6798ed923" />

  ---

3. EC2 Launch Success

  <img width="1854" height="1048" alt="Image" src="https://github.com/user-attachments/assets/8ce9c1fe-19d3-4c5f-adc2-1d652d1483ec" />

---

4. EC2 Launch Failure

<img width="1854" height="1048" alt="Image" src="https://github.com/user-attachments/assets/79e5c684-1508-4f0d-8576-c645f05450aa" />

---

# 🧠 Key Learnings
- IAM policies can enforce governance rules
- aws:RequestTag is used for tag validation
- Deny rules override allow permissions
- EC2 launch involves multiple resources (instance, network interface, volume)
- Proper policy scoping is critical
---

# 🏁 Conclusion

- This project successfully enforces mandatory tagging for EC2 instances using IAM policies.

- ✔ Improves governance
- ✔ Enables cost tracking
- ✔ Prevents misconfigured resources
- ✔ Demonstrates real-world AWS security practices

---
