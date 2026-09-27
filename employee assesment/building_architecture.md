# SkillForge AI — Complete Building Plan

## 1. Development Principle
Build independently, follow shared contracts, integrate in stages.

Do not wait for the entire backend or AI system before building the frontend.

## 2. Repository
```text
SkillForge-AI/
├── frontend/
├── backend/
├── ai-service/
├── docs/
├── data/
├── tests/
└── README.md
```

Branches:
```text
main
develop
feature/frontend
feature/auth
feature/competency
feature/recommendation
feature/ai-quiz
feature/database-integration
feature/testing
```

## 3. Shared Rules
Agree before coding:
- naming
- API response/error format
- roles
- competency levels
- IDs
- environment variables
- Git workflow
- formatting
- branch strategy

## 4. Phase 1 — Skeleton
Frontend:
React, TypeScript, Vite, Tailwind, Router, Zustand, TanStack Query, Axios, RHF, Zod, Recharts.

Backend:
FastAPI, Pydantic, MongoDB connection, auth skeleton, routers.

AI:
Python environment, document processing interface, embedding interface, LLM provider interface and quiz generator interface.

## 5. Phase 2 — Design System
Build:
- colors
- typography
- buttons
- inputs
- cards
- tables
- modal
- toast
- badges
- progress
- skeletons
- error states

Configure Storybook.

## 6. Phase 3 — API Contracts
Document each endpoint:
- method
- URL
- authentication
- request
- response
- errors
- example

Frontend can use mocks immediately.

## 7. Phase 4 — Authentication
Backend:
```text
POST /api/auth/register
POST /api/auth/login
POST /api/auth/logout
GET /api/auth/me
```
Frontend:
- login
- register
- auth state
- protected routes
- role routing
- logout

Checkpoint:
```text
Login → Dashboard
```

## 8. Phase 5 — Database
Create:
```text
users
roles
competencies
role_competencies
user_competencies
skill_gaps
courses
recommendations
documents
quizzes
questions
assessment_attempts
learning_progress
notifications
audit_logs
```
Seed 5–10 users, 3–5 roles, 30–50 competencies and 20–50 courses.

## 9. Phase 6 — Competency Engine
Implement:
```text
Role → Required Competencies
User → Current Competencies
Required - Current → Skill Gap
```
Example:
```json
{
  "competencyId": "sql",
  "currentLevel": 2,
  "requiredLevel": 4,
  "gap": 2,
  "priority": "high"
}
```

## 10. Phase 7 — Employee Dashboard
Implement:
- overall competency
- skill gaps
- recommendations
- learning progress
- recent assessment
- actions

Checkpoint:
```text
Login → Profile → Competency → Skill Gap → Dashboard
```

## 11. Phase 8 — Recommendation Engine
Start deterministic.

Example scoring:
```text
Skill relevance: 40%
Role relevance: 25%
Difficulty match: 15%
Learning history: 10%
Availability: 10%
```
Later add semantic similarity.

## 12. Phase 9 — Course Catalogue
Course fields:
```text
id
title
provider
description
skills
difficulty
duration
source
URL
availability
```
APIs:
```text
GET /api/courses
GET /api/courses/{id}
```
Add search/filter/sort/pagination.

## 13. Phase 10 — iGOT/NSSTA
Create:
```text
TrainingProvider
├── MockProvider
├── IGOTProvider
└── NSSTAProvider
```
Use MockProvider first. Do not block development on external access.

## 14. Phase 11 — Document Processing
Implement:
```text
Upload → Validation → Extraction → Cleaning → Chunking → Metadata
```
Support PDF, DOCX and PPTX.

## 15. Phase 12 — Semantic Search
```text
Chunks → Embeddings → FAISS/Vector Store
Question/Topic → Embedding → Similarity Search → Relevant Chunks
```

## 16. Phase 13 — AI Quiz Generation
```text
Context + Topic + Difficulty + Count
              ↓
             LLM
              ↓
       Structured MCQ
              ↓
          Validator
              ↓
      Source verification
              ↓
          Persistence
```

## 17. Phase 14 — Quiz Frontend
Build:
- upload
- configuration
- generation status
- question review
- quiz interface
- timer
- progress
- submit
- results

Use mock quiz JSON before AI integration.

## 18. Phase 15 — Assessment Analytics
```text
Score → Topic Analysis → Weak Areas → Competency Update → Recommendation Update
```

Example:
```text
SQL JOIN: 45%
Aggregation: 82%
Subqueries: 60%
```

## 19. Phase 16 — Adaptive Learning
```text
Assessment
 ↓
Performance
 ↓
Competency Update
 ↓
Skill Gap Recalculation
 ↓
Recommendation Re-ranking
```
This is the primary differentiator.

## 20. Phase 17 — Admin
Build:
- employee count
- competency distribution
- skill gaps
- department comparison
- course completion
- assessment performance

APIs:
```text
GET /api/admin/analytics
GET /api/admin/employees
GET /api/admin/skill-gaps
GET /api/admin/reports
```

## 21. Phase 18 — Notifications
Fields:
```text
id
userId
type
title
message
read
createdAt
```

## 22. Phase 19 — Testing
Frontend:
- Vitest
- React Testing Library
- Playwright

Backend:
- pytest

AI:
- extraction
- retrieval
- output structure
- grounding
- duplicate detection
- validation

Golden E2E:
```text
Login → Dashboard → Skill Gap → Recommendation → Quiz → Submit → Results
```

## 23. Phase 20 — Integration Checkpoints

### Checkpoint 1
Login → Dashboard

### Checkpoint 2
Profile → Competency → Skill Gap

### Checkpoint 3
Skill Gap → Recommendation → Course

### Checkpoint 4
Upload → AI → Quiz

### Checkpoint 5
Quiz → Assessment → Competency Update

### Final
```text
Login
 ↓
Assessment
 ↓
Skill Gap
 ↓
Recommendation
 ↓
Learning
 ↓
Upload
 ↓
AI Quiz
 ↓
Assessment
 ↓
Updated Skill Gap
 ↓
Updated Recommendation
```

## 24. Six-Member Work Allocation

### Member 1 — Frontend
UI, routing, dashboard, profile, competency, skill gaps, recommendations, courses, quiz, admin.

### Member 2 — Backend
FastAPI, authentication, users, APIs, RBAC, assessments and progress.

### Member 3 — AI/LLM
Document processing, embeddings, retrieval, LLM, MCQ generation and validation.

### Member 4 — Competency/Recommendation
Competency framework, role mapping, gap calculation, recommendation scoring and adaptive learning.

### Member 5 — Database/Integration
MongoDB, indexes, seed data, iGOT/NSSTA adapters and course catalogue.

### Member 6 — QA/DevOps/Product
Testing, CI/CD, deployment, documentation, demo data, PPT and demo script. Coordinates integration.

## 25. Shared Data Contracts
Create:
```text
docs/api-contracts.md
```
Core shared types:
```text
User
Role
Competency
SkillGap
Course
Recommendation
Document
Quiz
Question
Assessment
Progress
Notification
```

Prefer OpenAPI as the source of truth for frontend/backend contracts.

## 26. Mock-First Development
Maintain:
```text
mock-user.json
mock-competencies.json
mock-skill-gaps.json
mock-courses.json
mock-recommendations.json
mock-quiz.json
```
Never hardcode fake data inside UI components.

## 27. Integration-Ready Checklist
A module is ready only if:
- API/interface is documented
- Input/output schemas exist
- Errors are defined
- Mock data exists
- Unit tests pass
- README exists
- Environment variables are documented
- No secrets are committed
- Unfinished dependencies are mocked

## 28. Suggested 30-Day Plan

### Days 1–2
Architecture, Git, contracts, DB schema, wireframes.

### Days 3–5
Frontend shell, backend shell, MongoDB, authentication, design system.

### Days 6–9
Profile, competency, skill gaps, dashboard, course catalogue.

### Days 10–13
Recommendations, mock iGOT/NSSTA, document upload, extraction.

### Days 14–17
Embeddings, retrieval, MCQ generation, quiz UI.

### Days 18–20
Assessment, results, adaptive recommendations.

### Days 21–23
Admin dashboard, analytics, notifications.

### Days 24–26
Full integration, bug fixing, API/E2E testing.

### Days 27–28
Performance, accessibility, security, deployment.

### Days 29–30
Demo, PPT, architecture explanation, judge Q&A, rehearsal.

## 29. Golden Demo Scenario
Use a Statistical Officer.

Current:
```text
SQL = Intermediate
Python = Advanced
GIS = Beginner
```

Required:
```text
SQL = Advanced
Python = Advanced
GIS = Intermediate
```

System detects SQL and GIS gaps, recommends learning, accepts an SQL PDF, generates 10 MCQs, records an 8/10 result, detects weak SQL JOIN performance and updates the next recommendation.

This single journey should demonstrate the entire SkillForge AI intelligence loop.

## 30. Final Rule
Always:
```text
Code → Run → Test → Commit → Integrate
```
Never accumulate large amounts of unintegrated code. The final demo should show one complete working journey rather than many disconnected features.
