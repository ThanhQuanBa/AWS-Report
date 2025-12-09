---
title: "Event 4: AWS Cloud Mastery Series #2 - DevOps on AWS"
date: 2025-09-09
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---

# Bài thu hoạch “AWS Cloud Mastery Series #2: DevOps on AWS”

### Thời gian và Chủ đề

- **Thời gian:** Thứ Hai, 17 tháng 11, 2025 (1:00 PM – 4:30 PM)
- **Chủ đề:** DevOps on AWS

### Mục Đích Của Sự Kiện

- Cung cấp hiểu biết sâu sắc về các nguyên tắc, quy trình và thực tiễn tốt nhất của **DevOps** trên nền tảng AWS.
- Giới thiệu và hướng dẫn sử dụng bộ công cụ **AWS Developer Tools** (CodeCommit, CodeBuild, CodeDeploy, CodePipeline) để xây dựng **CI/CD pipeline** tự động.
- Tập trung vào các chiến lược triển khai tiên tiến như **Blue/Green Deployment** và **Canary Release** để giảm thiểu rủi ro.
- Khám phá cách tích hợp **Security (DevSecOps)** và **Monitoring** vào chu trình DevOps.

### Danh Sách Diễn Giả

- Thông tin chi tiết về diễn giả không có trong dữ liệu gốc, giả định là các chuyên gia giải pháp (Solution Architects) của AWS Vietnam.

### Nội Dung Nổi Bật

#### 1. DevOps Principles and AWS Developer Tools

- **Văn hóa & Nguyên tắc DevOps:** Tập trung vào tự động hóa, theo dõi và cải tiến liên tục.
- **Xây dựng CI/CD:** Hướng dẫn sử dụng AWS CodePipeline để tạo ra một luồng triển khai liên tục từ code commit đến production.
- **Infrastructure as Code (IaC):** Giới thiệu AWS CloudFormation và AWS CDK để quản lý tài nguyên hạ tầng bằng code.

#### 2. Advanced Deployment Strategies

- **Zero-Downtime Deployment:** Phân tích các kỹ thuật triển khai tiên tiến:
  - **Blue/Green Deployment:** Triển khai phiên bản mới song song với phiên bản cũ, sau đó chuyển đổi lưu lượng truy cập.
  - **Canary Release:** Triển khai phiên bản mới cho một lượng nhỏ người dùng trước khi triển khai rộng rãi.
- **AWS Services in Action:** Cách sử dụng AWS services như Amazon ECS, Amazon EKS, và AWS Lambda để hỗ trợ các chiến lược này.

#### 3. Monitoring, Logging, and DevSecOps

- **Quan sát (Observability):** Sử dụng Amazon CloudWatch và AWS X-Ray để thu thập metrics, logs và traces, giúp nhanh chóng phát hiện và giải quyết vấn đề.
- **DevSecOps:** Tích hợp các công cụ bảo mật (ví dụ: Amazon Inspector, Amazon GuardDuty) vào giai đoạn Build và Deploy để phát hiện sớm các lỗ hổng.

### Những Gì Học Được

#### Kỹ năng DevOps cốt lõi

- **Thiết kế CI/CD chuyên nghiệp:** Nắm được cách thiết kế một Pipeline CI/CD mạnh mẽ, có khả năng phục hồi (resilient) sử dụng bộ công cụ AWS.
- **Giảm thiểu rủi ro triển khai:** Hiểu rõ ưu và nhược điểm của Blue/Green và Canary Release, và khi nào nên áp dụng từng chiến lược để đảm bảo **Zero Downtime**.

#### Bảo mật và Quan sát

- **DevSecOps Mindset:** Nắm được tầm quan trọng của việc "Shift Left" - đưa bảo mật vào càng sớm càng tốt trong chu kỳ phát triển.
- **Observability:** Hiểu sự khác biệt giữa Monitoring (theo dõi) và Observability (quan sát), và cách sử dụng **Logs, Metrics, Traces** để có cái nhìn toàn diện về hiệu suất hệ thống.

### Ứng Dụng Vào Công Việc

- **Tự động hóa Deployment:** Triển khai các **CodePipeline** cho các dự án mới để tự động hóa toàn bộ quá trình Build, Test và Deploy.
- **Cải thiện chiến lược Go-Live:** Đề xuất và áp dụng các chiến lược **Canary Release** cho các tính năng quan trọng để đảm bảo sự ổn định và thu thập phản hồi sớm từ người dùng.
- **Tăng cường Observability:** Tích hợp X-Ray để theo dõi end-to-end các request, giúp gỡ lỗi các ứng dụng phân tán (microservices) nhanh hơn.

### Trải nghiệm trong event

Sự kiện này là một buổi học thực tế, nhấn mạnh vào việc chuyển từ lý thuyết sang thực hành trong môi trường AWS.

- **Giá trị Thực tế:** Việc đi sâu vào các chiến lược triển khai tiên tiến mang lại kiến thức trực tiếp có thể áp dụng ngay vào môi trường production.
- **Hệ sinh thái Công cụ:** Tôi hiểu rõ hơn về cách các công cụ trong hệ sinh thái AWS (Code\* services, CloudWatch, X-Ray) hoạt động cùng nhau để tạo ra một quy trình DevOps hoàn chỉnh.
  ![Event image](/images/2.jpg)
  ![Event image](/images/3.jpg)
  > Sự kiện này củng cố kiến thức của tôi về việc xây dựng, triển khai và vận hành phần mềm một cách hiệu quả, an toàn và tự động trên AWS.

---
