#🎯 PROJECT OVERVIEW

SYSTEM INSTRUCTION FOR SETUP AGENTS: > Read this document thoroughly. Use the "Technical Stack" and "Core Features" to populate the [PROJECT_OVERVIEW_PLACEHOLDER] and [PROJECT_OBJECTIVES_PLACEHOLDER] in the agent templates. Use the "Constraints" to add strict rules to the @Security_Lead and @Architect files.

1. Project Identity

- Project Name: [e.g., "Chronos Task Manager"]
- One-Sentence Pitch: [e.g., "A real-time, offline-first task manager for ADHD professionals."]
- Target Audience: [e.g., "Desktop web users who need high-speed keyboard navigation."]

2. Technical Stack
   Do not leave these blank. If undecided, explicitly state "Architect to decide".

- Frontend Framework: [e.g., React 18, Next.js 14 App Router, Vue 3]
- Styling / UI Library: [e.g., Tailwind CSS, Material UI, Shadcn/ui]
- Backend / API: [e.g., Node.js with Express, Python FastAPI, Supabase, Firebase]
- Database: [e.g., PostgreSQL via Prisma, MongoDB, Firestore]
- Authentication: [e.g., NextAuth, Firebase Auth, Custom JWT]
- Hosting / DevOps: [e.g., Vercel, AWS EC2, Docker]

3. Core Features (The MVP)
   What are the absolute minimum features required for Version 1.0?

- [Feature 1: e.g., "User registration with email/password and Google OAuth."]
- [Feature 2: e.g., "CRUD operations for tasks with categories and due dates."]
- [Feature 3: e.g., "Real-time sync across multiple browser tabs."]
- [Feature 4: e.g., "Dark/Light mode toggle stored in local user preferences."]

4. Strict Project Constraints
   What are the hard boundaries the AI team must never cross?

- Coding Standard 1: [e.g., "Strict TypeScript only. No 'any' types allowed."]
- Performance Rule: [e.g., "No heavy client-side rendering for static content."]
- Security Rule: [e.g., "All API routes must check for a valid session token before executing."]
- Formatting Rule: [e.g., "All components must be functional components using React Hooks. No class components."]

5. Required AI Team (The Roster)
   Instruct the @Team_Assembler on which agent templates to pull from the /agents_library for this specific project.

- [x] @Architect (Required for initial file structure and database schema)
- [x] @Senior_Dev (Required for writing the core application code)
- [x] @Security_Lead (Required for reviewing Auth and database queries)
- [x] @QA_Specialist (Required for writing unit tests and edge-case checking)
- [x] @Project_Manager (Required for maintaining state and documentation)
- [ ] [Add Custom Specialist if needed, e.g., @UX_Designer or @DevOps_Engineer]

6. Current Status & Initial Task
   Where is this project starting from?

- Status: [e.g., "Brand new repository, completely empty."]
- First Desired Action Post-Setup: [e.g., "Have the @Architect design the database schema and folder structure."]
