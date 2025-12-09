---
title: "Event 5: AWS Cloud Mastery Series #3 - Theo AWS Well-Architected Security Pillar"
date: 2025-09-09
weight: 5
chapter: false
pre: " <b> 4.5. </b> "
---

# Bài thu hoạch “AWS Cloud Mastery Series #3: Theo AWS Well-Architected Security Pillar”

### Thời gian và Chủ đề

- **Thời gian:** Thứ Bảy, 29 tháng 11, 2025 (8:30 AM – 12:00 PM)
- **Chủ đề:** Theo AWS Well-Architected Security Pillar

### Mục Đích Của Sự Kiện

- Tập trung vào **Trụ cột Bảo mật (Security Pillar)** của Khung kiến trúc AWS Well-Architected.
- Cung cấp kiến thức sâu về 5 lĩnh vực bảo mật chính: **Identity & Access Management (IAM), Detection, Infrastructure Protection, Data Protection và Incident Response**.
- Giới thiệu các dịch vụ và thực tiễn tốt nhất để bảo vệ workloads trên Cloud.

### Danh Sách Diễn Giả

- Thông tin chi tiết về diễn giả không có trong dữ liệu gốc, giả định là các chuyên gia giải pháp (Solution Architects) của AWS Vietnam.

### Nội Dung Nổi Bật

#### 1. Security Foundation & IAM (Identity & Access Management)

- **Nguyên tắc Cốt lõi:** **Least Privilege, Zero Trust, Defense in Depth** và **Shared Responsibility Model**.
- **Modern IAM:** Quản lý User, Role, Policy, tránh sử dụng Long-term credentials, sử dụng **IAM Identity Center** (SSO), **MFA** và **Access Analyzer**.

#### 2. Detection & Infrastructure Protection

- **Detection & Monitoring:** Sử dụng **CloudTrail** (org-level), **GuardDuty** (phát hiện mối đe dọa), **Security Hub** và logging (VPC Flow Logs).
- **Network Security:** Phân đoạn VPC, phân biệt **Security Groups vs NACLs**, sử dụng **WAF + Shield** và **Network Firewall**.

#### 3. Data Protection & Incident Response

- **Data Protection:** Quản lý khóa và mã hóa bằng **KMS** (Key Management Service) cho dữ liệu at-rest và in-transit (S3, RDS). Sử dụng **Secrets Manager** để lưu trữ và xoay vòng bí mật.
- **Incident Response (IR):** Quy trình IR lifecycle và các **Playbook** ứng phó cho các tình huống như compromised IAM key hay S3 public exposure, sử dụng **Lambda/Step Functions** để tự động hóa.

### Những Gì Học Được

#### Kiến thức Bảo mật Toàn diện

- **5 Pillar Bảo mật:** Nắm được cấu trúc bảo mật toàn diện trên Cloud, từ bảo vệ danh tính đến ứng phó sự cố.
- **IAM Hiện đại:** Hiểu cách thiết kế kiến trúc IAM không sử dụng quyền truy cập dài hạn (long-term credentials) để giảm thiểu rủi ro.
- **Bảo vệ Dữ liệu:** Nắm vững các tiêu chuẩn mã hóa và quản lý khóa bắt buộc đối với dữ liệu nhạy cảm.
- **Tự động hóa IR:** Hiểu vai trò của việc tự động hóa trong việc ứng phó nhanh với các sự cố bảo mật (Auto-response).

### Ứng Dụng Vào Công Việc

- **Kiểm tra Bảo mật:** Áp dụng các nguyên tắc của Security Pillar để rà soát (audit) và cải thiện cấu hình bảo mật hiện tại của các dự án đang làm việc.
- **Thiết lập GuardDuty & Security Hub:** Triển khai các dịch vụ này trong tài khoản AWS để thiết lập cơ chế phát hiện mối đe dọa liên tục.
- **Xử lý Secrets:** Sử dụng AWS Secrets Manager và Parameter Store để lưu trữ thông tin nhạy cảm thay vì hardcode, đồng thời thiết lập cơ chế xoay vòng.

### Trải nghiệm trong event

- **Tầm quan trọng của Bảo mật:** Sự kiện nhấn mạnh rằng bảo mật là trách nhiệm chung và phải được tích hợp ngay từ giai đoạn thiết kế (security by design).
- **Học thông qua Thực hành:** Các Mini Demo về cách validate IAM Policy và ứng phó sự cố rất thiết thực, cho thấy cách các công cụ AWS hoạt động.
- **Nâng cao Tư duy:** Giúp chuyển từ tư duy "chặn cửa" sang tư duy "phát hiện và ứng phó tự động".
  ![Event image](/public/images/z7308477584553_ecd987ff188f3d2d404cb60546d4b7bb.jpg)
  ![Event image](/images/4.jpg)
  > Sự kiện này là bắt buộc để tôi có thể xây dựng bất kỳ ứng dụng nào trên AWS một cách an toàn và tuân thủ các tiêu chuẩn cao nhất.

---
