# 🎯 PROJECT OVERVIEW

> **Instructions for the user:** Fill every field. If a field is genuinely undecided, write `"Architect to decide"` or `"User to confirm"` — but never leave it blank. Blank fields cause agents to make assumptions that will cost you time later. The more specific you are here, the less the AI team will need to ask.

---

## 1. Project Identity

- **Project Name:** [e.g., "Chronos Task Manager"]
- **One-Sentence Pitch:** [What does it do and for whom? e.g., "A real-time, offline-first task manager for ADHD professionals."]
- **Target Audience:** [Who uses this? Be specific. e.g., "Desktop web users who need high-speed keyboard navigation."]
- **Success Criteria:** [How do you know version 1.0 is done? e.g., "User can register, create a task, and sync it across two tabs without data loss."]

---

## 2. Technical Stack

> Do not leave these blank. If undecided, write `"Architect to decide"`. The `@Architect` can only decide implementation details — they cannot decide your hosting budget, your existing infrastructure, or your team's language preference. Those must come from you.

- **Language / Runtime:** [e.g., Python 3.11, Node.js 20, Go 1.22]
- **Frontend Framework:** [e.g., React 18, Next.js 14, Vue 3, or "N/A — CLI tool"]
- **Styling / UI Library:** [e.g., Tailwind CSS, Material UI, or "N/A"]
- **Backend / API Layer:** [e.g., FastAPI, Express, Django REST, or "N/A — scripts only"]
- **Database:** [e.g., PostgreSQL via Prisma, SQLite, MongoDB, or "None"]
- **Authentication:** [e.g., NextAuth, Firebase Auth, Custom JWT, or "None"]
- **External APIs / Services:** [e.g., OpenWeatherMap API, Stripe, or "None"]
- **Hosting / Deployment Target:** [e.g., Vercel, AWS EC2, local execution only]
- **Package Manager / Build Tool:** [e.g., pip, npm, poetry, or "Architect to decide"]

---

## 3. Core Features (The MVP)

> List only what is required for version 1.0. Do not add nice-to-haves here — those go in Section 7.

- **Feature 1:** [e.g., "Accept a city name as a CLI argument using argparse."]
- **Feature 2:** [e.g., "Fetch current weather via HTTP and print temperature and condition."]
- **Feature 3:** [e.g., "Handle errors gracefully: city not found, no internet, invalid API key."]
- **Feature 4:** [Add more as needed]

---

## 4. Strict Project Constraints

> These are hard rules the AI team must never violate. Be specific. Vague constraints get ignored.

- **Coding Standard:** [e.g., "Strict Python PEP 8. Type hints on all functions. No `any` types."]
- **Dependency Rule:** [e.g., "Standard library only where possible. No heavy frameworks like Click or Typer."]
- **Security Rule:** [e.g., "No hardcoded API keys. All secrets loaded from a `.env` file via `python-dotenv`."]
- **Formatting Rule:** [e.g., "Docstrings on every function. Google-style format."]
- **Architecture Rule:** [e.g., "Business logic and I/O must be in separate modules. No mixing."]
- **Other Constraints:** [Any other hard boundaries — licensing restrictions, performance requirements, etc.]

---

## 5. Pre-Existing Decisions

> Use this section to capture anything already decided before the AI team was assembled. This prevents agents from re-litigating settled choices or making conflicting decisions.

- **Decision 1:** [e.g., "We are using OpenWeatherMap API, not WeatherAPI. This is final."]
- **Decision 2:** [e.g., "The project must run on Python 3.9+ for compatibility with the target environment."]
- **Decision 3:** [Add more as needed, or write "None — greenfield project."]

---

## 6. Known Constraints and Anti-Patterns to Avoid

> What has already been tried and rejected? What is explicitly off-limits?

- [e.g., "Do not use `requests-cache`. It caused issues with the previous version."]
- [e.g., "Do not implement a database layer in v1. It is out of scope."]
- [Write "None" if this is a fresh start.]

---

## 7. Future Scope (Out of v1.0)

> List features that are intentionally deferred. This prevents scope creep during the build phase.

- [e.g., "Multi-city comparison view."]
- [e.g., "Hourly forecast support."]
- [Write "None defined yet" if unknown.]

---

## 8. Required AI Team

> Mark the agents needed for this project. Only check agents whose work is genuinely required for v1.0.

- [ ] `@Architect` — Required if the system has more than one module or file.
- [ ] `@Senior_Dev` — Required for all implementation work.
- [ ] `@Security_Lead` — Required if the project handles user data, secrets, authentication, or external API calls.
- [ ] `@QA_Specialist` — Required for all projects.
- [ ] `@Project_Manager` — Required for all projects.
- [ ] `@[Custom Agent]` — [Describe the role if adding a non-standard agent.]

---

## 9. Current Status and First Action

- **Status:** [e.g., "Brand new project, no files exist yet." or "Existing codebase in `/src`, needs a refactor plan."]
- **First Action Post-Setup:** [e.g., "Have `@Architect` design the folder structure and module boundaries."]
- **Deadline or Time Constraint:** [e.g., "MVP needed in 2 weeks." or "No deadline."]
