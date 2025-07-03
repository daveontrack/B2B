
```
# B2B Tender Platform - Internship Submission

## Deliverables Checklist
- [x] GitHub Repository
- [x] Database Schema (ER Diagram)
- [x] Architecture Overview
- [x] Loom Video Walkthrough

---

## Database Schema (ER Diagram)

```
erDiagram
    users ||--o{ companies : "1:1"
    users {
        int id PK
        string email
        string password_hash
        string role
        timestamp created_at
    }
    
    companies ||--o{ tenders : "1:N"
    companies {
        int id PK
        int user_id FK
        string name
        string industry
        text description
        string logo_url
    }
    
    tenders ||--o{ applications : "1:N"
    tenders {
        int id PK
        int company_id FK
        string title
        text description
        decimal budget
        date deadline
    }
    
    applications {
        int id PK
        int tender_id FK
        int company_id FK
        text proposal
    }
    
    companies }o--o{ services : "M:N"
    services {
        int id PK
        int company_id FK
        string name
        text description
    }
```

---

## Architecture Overview (ARCHITECTURE.md)

### Authentication Flow

```
sequenceDiagram
    Frontend->>Backend: POST /signup (email, password)
    Backend->>DB: Hash password & create user
    Backend->>Frontend: 201 Created
    Frontend->>Backend: POST /login (credentials)
    Backend->>Frontend: JWT Token
    Frontend->>Backend: Subsequent requests (with JWT)
    Backend->>Frontend: Authorized data
```

### Key Design Decisions

1. Modular Routing:
   - Auth: /routes/auth.ts
   - Companies: /routes/companies.ts
   - Tenders: /routes/tenders.ts

2. Storage Integration:

```typescript
// Supabase upload example
const uploadLogo = async (companyId: string, file: File) => {
  const { data, error } = await supabase.storage
    .from('company-logos')
    .upload(`logos/${companyId}`, file);
  return { data, error };
}
```

3. Error Handling:
   - Input validation with Zod
   - Centralized error middleware
   - Standardized API error responses

---

## Loom Video Script Template

Title: "B2B Tender Platform Walkthrough - dawit mengesha"

Introduction (0:00-0:30):
"Hello, I'm dawit mengesha, presenting my Full-Stack Developer Internship submission.
I've built a B2B tender platform using Next.js, Express, and PostgreSQL in five days."

Key Features Demo (0:30-1:30):
1. Company Registration:
   - Demonstrate the signup process with validation
   - Show logo upload functionality

2. Tender Management:
   - Walk through creating a new tender
   - Display paginated tender listings

3. Search Functionality:
   - Perform a company search by industry
   - View complete company profiles

Technical Highlights (1:30-2:30):
"The backend implements JWT authentication with role-based access controls.
I used PostgreSQL full-text search for efficient company discovery.
Docker containers ensure consistent environments across deployments."

Challenges & Learnings (2:30-end):
"File upload handling required careful error state management.
Structuring the monorepo taught me about shared type definitions.
Future improvements could include real-time notifications."

---

## Quick Start

```bash
# Using Docker
docker-compose up -d

# Local development
cd backend && npm run migrate
npm run dev # in both frontend and backend folders
```

---

## Submission Links
- GitHub: https://github.com/[yourname]/tender-platform
- Loom Video: https://loom.com/share/b234

---

"This project significantly improved my full-stack development skills and time management. I look forward to discussing how I can contribute to your team."

- dawit mengesha
```

Tips for submission:
1. Use the Mermaid Live Editor to adjust the ER diagram as needed
2. Keep the Loom video concise (under 3 minutes) with clear demonstrations
3. Highlight your most creative technical solutions in the architecture overview"# B2B" 
