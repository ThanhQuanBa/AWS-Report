---
title: "Proposal"
weight: 2
chapter: true
pre: " <b> 2. </b> "
---

# Proposal – Smart Resume Analyzer

_Một giải pháp AWS Serverless hợp nhất để phân tích CV so với JD và tạo ra Fit Score_

> **Lưu ý:** Proposal này giữ nguyên cách chia mục giống bản `_index.md` trước đó nhưng được viết lại dành riêng cho dự án Smart Resume Analyzer.

---

## 1) Executive Summary

**Smart Resume Analyzer** là nền tảng web serverless giúp đánh giá mức độ phù hợp giữa **CV của ứng viên** và **Job Description (JD)**. Hệ thống tính **Fit Score**, phát hiện **khoảng trống kỹ năng**, và đưa ra **gợi ý học tập cá nhân hóa**.  
Giải pháp được thực hiện bởi nhóm 5 thành viên trong **4 tuần** trên **AWS**, sử dụng các dịch vụ managed và pay-as-you-go để giữ chi phí ở mức cực thấp cho bản demo. Giao diện UI được xây dựng bằng **Next.js** và host trên **AWS Amplify**; backend sử dụng **API Gateway + Lambda**, kết hợp với **DynamoDB**, **S3**, **Comprehend**, **Textract**, và **Cognito**.

**Kết quả chính**

- Tốc độ screening CV nhanh hơn 90% trong môi trường demo.
- Fit Score khách quan, đi kèm báo cáo trực quan.
- Đưa ra lộ trình học tập phù hợp cho từng ứng viên.

---

## 2) Problem Statement

### 2.1 Vấn đề cần giải quyết

- Nhà tuyển dụng tốn nhiều thời gian để đọc CV và so sánh thủ công với JD.
- Ứng viên thiếu thông tin về các kỹ năng còn thiếu và cách cải thiện.
- Các công cụ sẵn có đắt đỏ hoặc chưa phù hợp với thị trường Việt Nam/SEA.

### 2.2 Giải pháp

- Upload CV (PDF/DOCX) và JD → hệ thống tự động trích xuất văn bản và xử lý NLP.
- Phát hiện **kỹ năng, kinh nghiệm, học vấn**; tính **Fit Score** so với JD.
- Gợi ý **lộ trình kỹ năng (skill pathway)** dựa trên **SkillOntology**.
- Đăng nhập bảo mật bằng **Cognito**; giao diện kết quả hiển thị bằng **Next.js**.

---

## 3) Solution Architecture (overview)

![Solution Architecture Diagram](https://i.ibb.co/ZR0VcspJ/Solution-Architecture.png)

Kiến trúc serverless, event-driven trên AWS.

**Các thành phần chính**

- **Frontend**: Next.js UI (Amplify Hosting) để upload và xem kết quả phân tích.
- **API Layer**: Amazon API Gateway → AWS Lambda.
- **Processing**:
  - `parseResume` → Textract (nếu PDF scan) → chuẩn hóa văn bản.
  - `nlpAnalyze` → Comprehend → trích xuất entity/kỹ năng/cụm từ.
  - `recommendSkills` → so sánh CV với JD + `SkillOntology` trong DynamoDB.
- **Data**: DynamoDB (kết quả phân tích, ontology), S3 (lưu CV/JD tạm thời).
- **Identity**: Cognito (JWT).
- **Ops**: IaC bằng AWS SAM, CI/CD với CodeBuild + CodePipeline, logging bằng CloudWatch.

**(Sơ đồ kiến trúc Mermaid sẽ được cung cấp riêng.)**

---

## 4) Technical Implementation

### 4.1 Tech stack

- **Backend**: .NET 8 (C# Minimal API chạy trên Lambda)
- **Frontend**: Next.js + TailwindCSS (Amplify Hosting)
- **AWS**: Lambda, API Gateway, DynamoDB, S3, Cognito, Comprehend, Textract
- **IaC**: AWS SAM
- **CI/CD**: CodeBuild + CodePipeline

### 4.2 End-to-end flow

1. Người dùng đăng nhập bằng **Cognito** và nhận JWT.
2. Frontend yêu cầu **presigned URL** để upload CV/JD lên **S3**.
3. API Gateway gọi **Lambda `parseResume`**:
   - Nếu PDF scan → xử lý bằng **Textract** để trích xuất text.
   - Chuẩn hóa text → lưu artefact tạm thời trên S3.
4. **Lambda `nlpAnalyze`** dùng **Comprehend** để phân tích entity/kỹ năng → ghi vào **DynamoDB**.
5. **Lambda `recommendSkills`** tải **SkillOntology** từ DynamoDB → so sánh CV với JD → tính **Fit Score** và kỹ năng còn thiếu.
6. Frontend gọi API lấy kết quả → hiển thị bằng bảng và biểu đồ.

### 4.3 Data model (DynamoDB – simplified)

- **Table `Profiles`** (PK: `userId`, SK: `profileId`) – lưu kết quả parse CV mới nhất.
- **Table `Analyses`** (PK: `analysisId`) – Fit Score, skill gaps, timestamps.
- **Table `SkillOntology`** (PK: `skillId`, gồm các trường: `name`, `tags`, `learningPath[]`).

### 4.4 API (high level)

- `POST /upload-url` → tạo presigned URL để upload CV/JD.
- `POST /analyze` → chạy pipeline phân tích cho bộ file tương ứng.
- `GET /analyses/{id}` → trả về Fit Score & danh sách kỹ năng đề xuất.
- `GET /skills/{id}` → tùy chọn, lấy lộ trình học của một kỹ năng.

---

## 5) Timeline & Milestones (4 weeks)

| Week | Milestone                    | Deliverables                                           |
| ---- | ---------------------------- | ------------------------------------------------------ |
| 1    | Foundation                   | SAM template, bảng DynamoDB, Cognito, UI cơ bản        |
| 2    | Parsing & NLP                | `parseResume`, `nlpAnalyze`, parser JD, unit tests     |
| 3    | Recommender & FE integration | `recommendSkills`, dashboard, biểu đồ                  |
| 4    | Demo & hardening             | E2E tests, logging, tối ưu chi phí, slide thuyết trình |

---

## 6) Budget Estimation (demo scale)

_Ước tính, với < 500 yêu cầu/tháng_

- **Lambda**: ~$0.02
- **API Gateway**: ~$0.01
- **S3** (vài GB, traffic thấp): ~$0.10
- **DynamoDB** (on-demand, R/W thấp): ~$0.05
- **Amplify Hosting**: ~$0.30
- **Comprehend + Textract (ít trang)**: ~$0.40
- **Cognito**: $0.00

**Tổng ≈ $0.9 / tháng (~$10 / năm)**

---

## 7) Security, Risks & Mitigations

**Security**

- Bucket S3 private + mã hóa **SSE-KMS**, chỉ cho phép upload bằng presigned URL.
- **IAM least privilege**; API yêu cầu **JWT Cognito**.
- **Masking PII** trong logs; giám sát bằng **CloudWatch Alarms**.
- Tuỳ chọn: lifecycle rule xoá CV/JD sau khi phân tích.

**Risks & mitigations**

- _Độ chính xác NLP_: yêu cầu đúng định dạng + fallback bằng rule từ khóa.
- _CV nặng hoặc lỗi_: kiểm tra size/format; sanitize trước khi NLP.
- _Chi phí tăng bất thường_: thiết lập AWS Budget + giới hạn số trang Textract.

---

## 8) Expected Outcomes

- Tự động đối chiếu CV–JD với **Fit Score** minh bạch.
- Biểu đồ trực quan về **kỹ năng trùng khớp vs thiếu** và **lộ trình học tập**.
- Kiến trúc serverless, chi phí thấp, dễ mở rộng và tối ưu cho demo.

---

## 📄 Proposal Document (Google Docs)

👉 **Xem Proposal tại đây:**  
[GOOGLE DOC LINK](https://docs.google.com/document/d/1ALFieRvZWl1Azg3C8a7L8Z-iL6-chpzS/edit?usp=sharing&ouid=100398969873071071371&rtpof=true&sd=true)
