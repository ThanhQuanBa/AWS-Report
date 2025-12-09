# Proposal – Smart Resume Analyzer

_A Unified AWS Serverless solution to analyze CVs vs JDs and generate Fit Scores_

> **Note:** This proposal follows the sectioning style of your previous `_index.md` but is rewritten for the Smart Resume Analyzer project.

---

## 1) Executive Summary

**Smart Resume Analyzer** is a serverless web platform that evaluates the match between a candidate’s **CV** and a **Job Description (JD)**. It calculates a **Fit Score**, detects **skill gaps**, and provides **personalized learning suggestions**.

The solution is implemented by a 5-member team in **4 weeks** on **AWS**, using managed, pay-as-you-go services to keep demo costs near zero. The UI is built with **Next.js** and hosted on **AWS Amplify**; the backend runs on **API Gateway + Lambda**, together with **DynamoDB**, **S3**, **Comprehend**, **Textract**, and **Cognito**.

**Key outcomes:**

- 90% faster CV screening for demo scenarios
- Objective Fit Score with visualized reports
- Actionable learning roadmap for each candidate

---

## 2) Problem Statement

### 2.1 What’s the problem?

- Recruiters spend significant time manually reading CVs and comparing them to JDs.
- Candidates lack insight into which skills they are missing and how to improve.
- Existing tools are costly or not optimized for Vietnamese/SEA use cases.

### 2.2 The solution

- Upload CV (PDF/DOCX) and JD → automated text extraction + NLP.
- Detect **skills, experience, education** → compute **Fit Score** vs JD.
- Recommend **learning pathways** using a custom **SkillOntology** stored in DynamoDB.
- Secure login with **Cognito** and results shown in a responsive **Next.js** dashboard.

---

## 3) Solution Architecture (overview)

![Solution Architecture Diagram](https://i.ibb.co/ZR0VcspJ/Solution-Architecture.png)

A fully serverless, event-driven architecture built on AWS.

**Main components:**

- **Frontend**: Next.js UI (Amplify Hosting) for upload and results dashboard
- **API Layer**: Amazon API Gateway → AWS Lambda functions
- **Processing pipeline**:
  - `parseResume`: Uses Textract (for scanned PDFs) → normalized text
  - `nlpAnalyze`: Uses Comprehend → entity and skill detection
  - `recommendSkills`: Compares against JD + ontology in DynamoDB
- **Data**: DynamoDB (results, ontology), S3 (uploaded CV/JD)
- **Identity**: Cognito (JWT-based authentication)
- **Ops**: AWS SAM for IaC, CI/CD with CodePipeline + CodeBuild, monitoring via CloudWatch

---

## 4) Technical Implementation

### 4.1 Tech stack

- **Backend**: .NET 8 (C# Minimal API on Lambda)
- **Frontend**: Next.js + TailwindCSS (Amplify Hosting)
- **AWS Services**: Lambda, API Gateway, DynamoDB, S3, Cognito, Comprehend, Textract
- **Infrastructure as Code**: AWS SAM
- **CI/CD**: AWS CodeBuild + CodePipeline

### 4.2 End-to-end flow

1. User signs in via **Cognito** and receives JWT.
2. Frontend requests a **presigned upload URL** for S3 → uploads CV/JD.
3. API Gateway triggers **Lambda `parseResume`**:
   - If scanned PDF → use Textract
   - Otherwise use direct text extraction
   - Store processed text in S3
4. **Lambda `nlpAnalyze`** uses Comprehend to detect entities/skills → saves to DynamoDB
5. **Lambda `recommendSkills`** retrieves SkillOntology → computes Fit Score + skill gaps
6. Frontend fetches results through API → visualizes data

### 4.3 DynamoDB data model (simplified)

- **Profiles**

  - PK: `userId`
  - SK: `profileId`
  - Stores latest CV parse data

- **Analyses**

  - PK: `analysisId`
  - Fit score, skills matched, skill gaps, timestamps

- **SkillOntology**
  - PK: `skillId`
  - Attributes: `name`, `tags`, `learningPath[]`

### 4.4 High-level API design

- `POST /upload-url` → get presigned S3 URL
- `POST /analyze` → trigger complete analysis pipeline
- `GET /analyses/{id}` → retrieve Fit Score & recommendations
- `GET /skills/{id}` → optional skill detail endpoint

---

## 5) Timeline & Milestones (4 weeks)

| Week | Milestone                    | Deliverables                                        |
| ---- | ---------------------------- | --------------------------------------------------- |
| 1    | Foundation                   | SAM template, DynamoDB tables, Cognito, base UI     |
| 2    | Parsing & NLP                | `parseResume`, `nlpAnalyze`, JD parsing, unit tests |
| 3    | Recommender & FE integration | `recommendSkills`, dashboard, charts                |
| 4    | Demo & optimization          | E2E tests, logging, cost tuning, presentation deck  |

---

## 6) Budget Estimation (demo scale)

Estimated for **< 500 requests/month**:

- **Lambda**: ~$0.02
- **API Gateway**: ~$0.01
- **S3**: ~$0.10
- **DynamoDB**: ~$0.05
- **Amplify Hosting**: ~$0.30
- **Comprehend + Textract**: ~$0.40
- **Cognito**: $0.00

**Total ≈ $0.9 per month (~$10 per year).**

---

## 7) Security, Risks & Mitigations

### Security

- Private S3 buckets with **SSE-KMS** encryption
- **IAM least privilege**
- Backend protected by **Cognito JWT**
- **PII masking** in logs
- Lifecycle rules to auto-delete raw files after analysis

### Risks & mitigations

- **NLP accuracy issues** → fallback rules, guided input formats
- **Large/unformatted CVs** → sanitize + file size validation
- **Unexpected cost increases** → AWS Budget alarms & page caps

---

## 8) Expected Outcomes

- Automated CV–JD comparison with transparent **Fit Score**
- Detailed visualization of **matched skills, missing skills, and learning path**
- Serverless, low-ops architecture suitable for demos, scaling, or localization

---

## Proposal Document (Google Docs)

Link: https://docs.google.com/document/d/1ALFieRvZWl1Azg3C8a7L8Z-iL6-chpzS/edit?usp=sharing
