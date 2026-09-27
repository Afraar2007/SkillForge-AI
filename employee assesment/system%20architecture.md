# SkillForge AI — System Architecture

## 1. Architecture Goal
SkillForge AI uses a modular, API-first architecture so six team members can work independently and integrate later.

```text
Independent Modules
      ↓
Stable API Contracts
      ↓
Shared Data Models
      ↓
Integration Layer
      ↓
Complete Platform
```

## 2. High-Level Architecture
```text
Users
  ↓
React Web Portal
  ↓ HTTPS/REST
FastAPI API
  ├── Auth/RBAC
  ├── Core Learning Services
  ├── Admin Analytics
  ├── Competency Engine
  ├── Recommendation Engine
  └── Assessment/Quiz Engine
          ↓
       AI/NLP Layer
          ├── LLM
          ├── Embeddings
          └── Semantic Retrieval
          ↓
     MongoDB / Vector Store / File Storage
          ↑
     Integration Layer
       ├── iGOT Adapter
       └── NSSTA Adapter
```

## 3. Frontend
```text
frontend/src/
├── app/
├── components/
│   ├── ui/
│   ├── layout/
│   ├── charts/
│   └── navigation/
├── features/
│   ├── auth/
│   ├── profile/
│   ├── competency/
│   ├── skill-gap/
│   ├── recommendations/
│   ├── courses/
│   ├── learning/
│   ├── assessments/
│   ├── quiz-generator/
│   ├── notifications/
│   └── admin/
├── hooks/
├── lib/
│   ├── api/
│   ├── auth/
│   └── utils/
├── stores/
├── types/
└── main.tsx
```

Data flow:
```text
Component → Feature Hook → TanStack Query → API Service → Axios → FastAPI
```
Zustand is for client/UI state, not as the main server-state store.

## 4. Backend
```text
backend/
├── app/
│   ├── main.py
│   ├── api/
│   ├── models/
│   ├── schemas/
│   ├── services/
│   ├── repositories/
│   ├── ai/
│   ├── integrations/
│   ├── middleware/
│   ├── core/
│   └── workers/
├── tests/
└── .env.example
```

Layers:
- API: HTTP, validation and response formatting.
- Service: business logic.
- Repository: persistence.
- AI: LLM, embeddings and retrieval.
- Integrations: iGOT/NSSTA adapters.

## 5. Competency Engine
```text
User Profile + Role + Assessment
          ↓
Required Competencies
          ↓
Current Competencies
          ↓
Gap Calculation
          ↓
Priority
          ↓
Stored Skill Gaps
```

## 6. Recommendation Engine
```text
Role + Gaps + History + Assessment + Catalogue
                  ↓
          Candidate Generation
                  ↓
          Semantic Matching
                  ↓
          Rule-Based Filtering
                  ↓
               Ranking
                  ↓
             Explanation
```
Use deterministic rules for eligibility, availability and required level; use AI for semantic matching/explanations where appropriate.

## 7. Document-to-Quiz
```text
Upload
 ↓
File Validator
 ↓
PDF/DOCX/PPTX Extraction
 ↓
Cleaning
 ↓
Chunking
 ↓
Embeddings
 ↓
Vector Store
 ↓
Relevant Context Retrieval
 ↓
LLM Generation
 ↓
Question Validator
 ↓
Source Verification
 ↓
Quiz Database
 ↓
Frontend
```

## 8. Assessment
```text
Assessment → Questions → Answers → Scoring → Topic Analysis
          → Competency Update → Recommendation Update
```

## 9. Adaptive Learning
```text
Initial Assessment
 ↓
Skill Gap
 ↓
Learning Recommendation
 ↓
Learning
 ↓
Quiz
 ↓
Topic Performance
 ↓
Competency Update
 ↓
New Recommendation
```

## 10. Database
Core collections:
```text
users
roles
competencies
role_competencies
user_competencies
skill_gaps
courses
training_providers
recommendations
documents
document_chunks
quizzes
questions
assessment_attempts
learning_progress
notifications
audit_logs
```

## 11. External Integrations
Use provider interfaces:
```text
Recommendation Engine
       ↓
TrainingProvider Interface
       ├── MockProvider
       ├── iGOTProvider
       └── NSSTAProvider
```
This prevents external providers from being tightly coupled to core business logic.

## 12. API Contract
Examples:
```text
GET  /api/competencies
GET  /api/users/me/competencies
GET  /api/users/me/skill-gaps
GET  /api/recommendations
GET  /api/courses
POST /api/documents/upload
POST /api/quizzes/generate
GET  /api/quizzes/{id}
POST /api/quizzes/{id}/submit
GET  /api/assessments
POST /api/assessments/{id}/submit
GET  /api/progress
GET  /api/admin/analytics
```

Standard response:
```json
{
  "success": true,
  "data": {},
  "message": "Success"
}
```

Standard error:
```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid request"
  }
}
```

## 13. Authentication
```text
Login → FastAPI → Validate → Token/Session → Frontend Auth → Protected Routes
```
Backend enforces:
- employee permissions
- admin permissions

## 14. Background Processing
For large AI/document jobs:
```text
Frontend → API → Job Queue → Worker → AI Processing → Database → Poll/Notify
```
Small MVP jobs may run synchronously.

## 15. Security
```text
HTTPS
 ↓
Authentication
 ↓
RBAC
 ↓
Request Validation
 ↓
Business Authorization
 ↓
Database Access
 ↓
Audit Logging
```
Never log passwords, tokens or sensitive document contents.

## 16. Deployment
Prototype:
```text
Browser → Frontend Hosting → FastAPI → MongoDB
```

Production extension:
```text
CDN → Frontend → Load Balancer → FastAPI Instances
                                   ├→ MongoDB
                                   ├→ Vector Store
                                   ├→ Queue/Workers
                                   └→ Object Storage
```

## 17. Team Ownership
| Member | Module |
|---|---|
| 1 | React frontend/UI |
| 2 | FastAPI/backend/auth |
| 3 | AI/LLM/document/quiz |
| 4 | Competency/recommendation |
| 5 | MongoDB/integrations |
| 6 | QA/DevOps/docs/product |

Every module must expose documented inputs, outputs, errors, mocks and tests.
