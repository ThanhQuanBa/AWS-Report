---
title: "Event 5: AWS Cloud Mastery Series #3 - AWS Well-Architected Security Pillar"
date: 2025-09-09
weight: 5
chapter: false
pre: " <b> 4.5. </b> "
---

# Event Report: “AWS Cloud Mastery Series #3: AWS Well-Architected Security Pillar”

## Date & Topic

- **Date:** Saturday, November 29, 2025 (8:30 AM – 12:00 PM)
- **Topic:** AWS Well-Architected Security Pillar

## Event Purpose

- Focus on the **Security Pillar** of the AWS Well-Architected Framework.
- Provide in-depth knowledge of the five main security domains: **Identity & Access Management (IAM), Detection, Infrastructure Protection, Data Protection, and Incident Response**.
- Introduce AWS services and best practices to secure workloads on the Cloud.

## Speakers

- Detailed speaker information is not available; assumed to be AWS Vietnam **Solution Architects**.

## Key Highlights

### 1. Security Foundation & IAM (Identity & Access Management)

- **Core Principles:** **Least Privilege, Zero Trust, Defense in Depth**, and **Shared Responsibility Model**.
- **Modern IAM:** User, Role, and Policy management; avoid long-term credentials; use **IAM Identity Center (SSO)**, **MFA**, and **Access Analyzer**.

### 2. Detection & Infrastructure Protection

- **Detection & Monitoring:** Use **CloudTrail** (org-level), **GuardDuty** (threat detection), **Security Hub**, and logging (VPC Flow Logs).
- **Network Security:** VPC segmentation, distinction between **Security Groups vs NACLs**, and using **WAF + Shield** and **Network Firewall**.

### 3. Data Protection & Incident Response

- **Data Protection:** Key management and encryption using **KMS** for at-rest and in-transit data (S3, RDS); store and rotate secrets with **Secrets Manager**.
- **Incident Response (IR):** IR lifecycle process and **Playbooks** for incidents such as compromised IAM keys or public S3 exposure; automation using **Lambda/Step Functions**.

## Key Learnings

### Comprehensive Security Knowledge

- **5 Security Pillars:** Understand full cloud security structure from identity protection to incident response.
- **Modern IAM:** Learn to design IAM architectures without long-term credentials to reduce risk.
- **Data Protection:** Master encryption standards and key management for sensitive data.
- **Automated IR:** Understand the role of automation for fast security incident response.

## Workplace Applications

- **Security Audits:** Apply Security Pillar principles to audit and improve current project configurations.
- **Deploy GuardDuty & Security Hub:** Implement continuous threat detection within AWS accounts.
- **Secrets Management:** Use AWS Secrets Manager and Parameter Store instead of hardcoding sensitive data, with proper rotation.

## Event Experience

- **Security Importance:** Emphasis on security as a shared responsibility and integrating it from design phase (**security by design**).
- **Hands-on Learning:** Mini demos for IAM Policy validation and incident response showed practical AWS tool usage.
- **Mindset Enhancement:** Shift from a “blocking” mindset to a proactive “detect and respond automatically” mindset.
  ![Event image](/images/5.jpg)
  ![Event image](/images/4.jpg)
  > This event is essential for building any AWS application securely while adhering to the highest standards.
