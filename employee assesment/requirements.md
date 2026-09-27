# SkillForge AI — Complete System Requirements

## 1. Project Overview
**Project:** SkillForge AI  
**SIH Problem Statement:** SIH26101  
**Tagline:** From Skill Gaps to Personalized Growth

SkillForge AI is an AI-powered Skill Intelligence and Adaptive Learning Platform for India's Official Statistical System. It builds employee competency profiles, identifies role-specific skill gaps, recommends relevant learning resources from the iGOT Karmayogi and NSSTA ecosystem, generates source-grounded quizzes from uploaded learning materials, evaluates performance, and continuously updates the learning path.

### Core Learning Loop
```text
Assess → Identify Skill Gaps → Recommend Learning → Learn → Test
      → Analyze Performance → Update Competency → Recommend Next Learning
```

## 2. Goals
- Build employee competency profiles.
- Determine current proficiency and role-required proficiency.
- Identify and prioritize competency gaps.
- Recommend personalized learning.
- Support iGOT and NSSTA through an integration layer.
- Generate MCQs from PDF/DOCX/PPTX materials.
- Provide source traceability for generated questions.
- Assess performance and adapt recommendations.
- Provide employee and admin analytics.
- Keep modules independently developable and integrable.

## 3. Users
### Employee
Registration/login, profile, assessment, competency view, skill gaps, recommendations, courses, learning progress, document upload, quiz generation, quizzes and results.

### Administrator
User management, competency analytics, skill-gap analytics, course/training monitoring, assessment analytics and reports.

### AI/System Services
Competency analysis, semantic matching, recommendation scoring, document processing, question generation/validation and performance analysis.

## 4. Functional Requirements

### FR-01 Authentication
- Registration, login, logout and session restoration.
- Password recovery flow.
- Employee/admin roles.
- Token/session expiry handling.
- Backend-enforced authorization.

### FR-02 Employee Profile
Fields:
- Name
- Email
- Employee ID
- Department
- Designation
- Role
- Experience
- Existing skills
- Previous training
- Learning interests

### FR-03 Competency Framework
Categories:
- Statistical: survey design, sampling, national accounts, price/labour/agricultural/industrial statistics, SDG indicators, metadata, data quality.
- Technical: Python, R, SQL, Stata, SPSS, SAS, GIS, visualization, AI/ML, cloud, APIs, open data.
- Digital governance: cybersecurity, privacy, digital signatures, government cloud, DPI.
- Behavioural/managerial: leadership, communication, project management, ethics, decision making, change management.

### FR-04 Proficiency
Use:
1 Beginner, 2 Basic, 3 Intermediate, 4 Advanced, 5 Expert.

Store current level, required level, confidence, evidence/source and assessment history.

### FR-05 Skill Gap Detection
```text
Gap = Required Level - Current Level
```
Priority should also consider role importance, assessment confidence, frequency of use and organizational priority.

### FR-06 Recommendations
Match:
Employee + Role + Gaps + Current Level + Learning History + Assessment Results + Training Catalogue

Return:
resource ID, title, provider, skill, match score, difficulty, duration, reason, source and priority.

### FR-07 iGOT Integration
Use an adapter/interface. If an official API is unavailable, use a clearly labelled mock provider. Never claim live integration unless actually authorized and implemented.

### FR-08 NSSTA Integration
Support training catalogue data including programme ID, title, topic, competency, eligibility, duration, delivery mode, schedule, provider and source.

### FR-09 Document Upload
Support PDF, DOCX and PPTX. Validate type/size and track processing.

Pipeline:
```text
Upload → Validate → Extract → Clean → Chunk → Embed → Index → Generate
```

### FR-10 AI Quiz Generation
Generate MCQs with:
- Question
- Options
- Correct answer
- Explanation
- Difficulty
- Topic
- Learning objective
- Source document/page/section where available

### FR-11 Source Grounding
Display source document, page, section or retrieved passage/reference whenever available.

### FR-12 Quiz Validation
Check exactly one correct answer, distinct options, understandable wording, source support, no duplicates, valid difficulty and no obvious ambiguity.

### FR-13 Assessments
Support initial competency assessment, course assessment, AI quiz and reassessment. Store attempts, answers, score, percentage, time, topic performance and timestamp.

### FR-14 Adaptive Learning
```text
Assessment → Topic Performance → Weak Areas → Competency Update → Recommendation Update
```

### FR-15 Learning Progress
Track enrolled/in-progress/completed courses, learning hours, assessment scores, quiz attempts and competency improvement.

### FR-16 Employee Dashboard
Show overall competency, category scores, top gaps, recommended learning, progress, recent assessment, upcoming actions and AI recommendations.

### FR-17 Admin Dashboard
Show employee count, active learners, average competency, common gaps, department competency, course completion, assessment performance and training demand.

### FR-18 Notifications
Support recommendation, quiz result, course completion, competency update and system notifications.

### FR-19 Search/Filtering
Courses: keyword, competency, category, difficulty, provider, duration and delivery mode. Admin: department, role, competency and date range.

## 5. Non-Functional Requirements

### Performance
Target:
- LCP < 2.5s
- INP < 200ms
- CLS < 0.1

Use lazy loading, code splitting, caching, pagination, debounced search and optimized assets.

### Accessibility
WCAG 2.1 AA. Use semantic HTML, keyboard navigation, visible focus, screen-reader labels, sufficient contrast and non-color-only indicators.

### Security
HTTPS, secure authentication, RBAC, input/file validation, rate limiting, audit logging, no secrets in frontend, no token/password logging and backend authorization.

### Scalability
Allow growth in users, competencies, courses, documents, AI requests and providers without major redesign.

### Reliability
Gracefully handle API, AI, file-processing and network failures.

## 6. Technology
### Frontend
React 18+, TypeScript, Vite, Tailwind CSS, React Router, Zustand, TanStack Query, Axios, React Hook Form, Zod, Recharts and Lucide React.

### Backend
FastAPI, Python, Pydantic, JWT/RBAC, MongoDB.

### AI/ML
NLP, Sentence Transformers/embeddings, semantic search, LLMs and recommendation/classification logic.

### Storage
MongoDB for core data, vector storage/FAISS for semantic retrieval and object/file storage for documents.

## 7. API Groups
```text
/api/auth
/api/users
/api/competencies
/api/skill-gaps
/api/recommendations
/api/courses
/api/documents
/api/quizzes
/api/assessments
/api/progress
/api/notifications
/api/admin
```

## 8. Database Collections
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

## 9. Testing
Frontend: Vitest, React Testing Library, Playwright.  
Backend: pytest.  
AI: extraction, retrieval, structure, grounding, duplicates and validation.

## 10. Definition of Done
Authentication, profile, assessment, competency, skill gaps, recommendations, course catalogue, upload, AI quiz, quiz-taking, results, adaptive update, dashboards, APIs, tests, production build and documentation must work.
