# Karigar Connect

**Make practical skills easier to prove.**

Karigar Connect is a bilingual (English and Urdu) skilled-services platform designed for Pakistan. It helps customers discover skilled professionals using practical competency assessments, verified work evidence, customer feedback, and transparent trust indicators.

**Live application:** https://karigar-connect-gray.vercel.app/

> **Verification disclaimer:** A verified badge represents an assessment recorded by an authorized assessor against the platform's competency rubric. It does not represent government accreditation, a professional licence, or a government-issued qualification.

---

## Table of contents

- [What the platform does](#what-the-platform-does)
- [User roles](#user-roles)
- [Main features](#main-features)
- [Technology stack](#technology-stack)
- [Application architecture and data storage](#application-architecture-and-data-storage)
- [Getting started](#getting-started)
- [Environment configuration](#environment-configuration)
- [Demo data](#demo-data)
- [Deployment notes](#deployment-notes)
- [Important limitations](#important-limitations)
- [Project structure](#project-structure)

## What the platform does

Karigar Connect focuses on more than listing workers as available. It gives workers ways to demonstrate their abilities and gives customers several signals to consider before requesting a service.

The platform brings together:

1. **Skills evidence:** workers can add evidence for practical competencies.
2. **Structured assessment:** authorized assessors review evidence using a defined scoring rubric.
3. **Verified work history:** customers can confirm completed work and submit reviews linked to jobs.
4. **Worker discovery:** customers can search and filter public worker profiles.
5. **Trust and growth tools:** workers can track their trust score, tier progress, badges, earnings records, and public QR passport.
6. **Service guidance:** customers can browse service categories and indicative price guides in PKR.

The application includes seeded demonstration data so its main workflows can be explored without first creating a complete real-world network of workers, customers, and assessors.

## User roles

The application has role-specific registration, authentication, dashboards, and protected routes.

| Role | Main responsibilities |
| --- | --- |
| **Worker / Karigar** | Create and manage a professional profile, select trades, maintain a competency matrix, submit evidence, manage job requests, view assessments and badges, respond to reviews, and track growth. |
| **Customer / Employer / Hirer** | Discover workers, filter profiles, shortlist professionals, send contact requests, manage jobs, confirm completed work, and submit reviews. |
| **Assessor** | Apply for assessor access, manage an assessment queue, review submitted evidence, score competencies using the rubric, and issue verification outcomes where authorized. |
| **Administrator** | Manage users, assessor applications, trades, competencies, tier rules, disputes, reports, moderation, and audit records. |

Access to role-specific areas is controlled through protected application routes and role checks.

## Main features

### 1. Worker discovery and public profiles

- Browse public worker profiles.
- Search by worker name, trade, service group, city, skills, and profile information.
- Filter by location, experience, rating, competency, and female-professional availability.
- View profile details, skills, verified competencies, ratings, completed-job information, trust score, and tier status.
- Open public worker portfolio pages.

### 2. Competency matrix and evidence assessment

- Workers can view competencies associated with their selected trade.
- Workers can submit supporting evidence for assessment.
- Assessors work through a verification queue and review submitted evidence.
- Competencies use a structured rubric with score levels from 0 to 3.
- Safety-critical criteria are included in the assessment workflow.
- Successful assessments can result in time-limited verification badges.
- Workers can review their assessment history and issued badges.

A badge is evidence of an in-platform assessment; it should not be presented as government accreditation.

### 3. Jobs and service requests

The job workflow supports these statuses:

`REQUESTED → ACCEPTED → SCHEDULED → IN_PROGRESS → COMPLETED`

It also supports `CANCELLED` and `DISPUTED` states.

Customers can request a worker, while workers can manage incoming requests and update job progress. The application includes contact-request handling and keeps certain contact details restricted until the worker accepts a request.

### 4. Verified reviews and work proof

- Customers can submit reviews associated with completed jobs.
- The review experience includes an overall rating and additional rating dimensions.
- Workers can respond to eligible reviews.
- Review moderation and reporting tools are available to administrators.
- Customers can confirm completed work and its supporting photo evidence.
- Before-and-after job media is stored separately from ordinary structured browser data.

### 5. Trust score and worker tiers

The platform calculates a worker trust score on a 0–100 scale and includes four tier levels:

- Bronze
- Silver
- Gold
- Platinum

Workers can view a trust-score breakdown and tier progress. Administrators can configure tier rules and review tier applications. The application also includes rating-health checks and an administrative dispute workflow.

### 6. QR Karigar Passport and growth tools

- Worker passport identifiers can be used for public verification lookup.
- QR codes provide a scannable route to a worker's verification information.
- Workers can access growth-related information, including earnings records and leaderboard features.
- Public verification pages allow visitors to check available badge information.

### 7. Service catalogue and price guides

The service catalogue is organized into service groups and includes a broad range of skilled-trade categories, including:

- Electrical work
- Plumbing
- Air conditioning and HVAC
- Appliances
- Carpentry and painting
- Masonry and welding
- Solar and generators
- Women-focused home services

Price guides are expressed in Pakistani rupees (PKR). The application includes administrative tools for managing trade information and price guidance. These values are indicative guides, not guaranteed quotations.

### 8. AI-assisted home problem finder

The Problem Finder accepts a written description and can also accept an image. It attempts to suggest a relevant service category, urgency level, likely cause, indicative PKR range, and safety guidance.

- The online analysis path uses Google's GenAI SDK.
- If the AI request is unavailable or no API key is configured, the application has a deterministic keyword-based offline fallback.
- Results are estimates and should not be treated as a confirmed diagnosis or final service quotation.

The AI integration is implemented through middleware in the Vite configuration. See [Environment configuration](#environment-configuration) and [Deployment notes](#deployment-notes) before expecting this endpoint to work in a production hosting environment.

### 9. Demand insights and analytics

The application includes public and role-specific demand-insights pages. Available views include demand information based on service categories, cities, and selectable time periods, alongside charts and summary metrics.

### 10. English and Urdu interface

- English and Urdu interface content is supported.
- Urdu pages support right-to-left layout.
- The interface includes voice input controls using browser speech-recognition capabilities where supported by the browser.

### 11. Administrative governance

The administrator area includes tools for:

- User management
- Assessor application review
- Trade and competency management
- Tier rules and tier review queue
- Dispute handling
- Reports and moderation
- Audit-log review
- Demand insights

## 🛠️ Tech Stack

### Frontend
![React](https://img.shields.io/badge/React_19-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Vite](https://img.shields.io/badge/Vite_8-646CFF?style=for-the-badge&logo=vite&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS_4-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)

### Routing & UI Libraries
![React Router](https://img.shields.io/badge/React_Router_7-CA4245?style=for-the-badge&logo=reactrouter&logoColor=white)
![Motion](https://img.shields.io/badge/Motion-FFFFFF?style=for-the-badge&logo=framer&logoColor=black)
![Lucide React](https://img.shields.io/badge/Lucide_React-F56565?style=for-the-badge&logo=lucide&logoColor=white)

### AI & APIs
![Google Gemini](https://img.shields.io/badge/Google_Gemini-8E75B2?style=for-the-badge&logo=googlegemini&logoColor=white)
![Web Crypto API](https://img.shields.io/badge/Web_Crypto_API-2563EB?style=for-the-badge)
![Web Speech API](https://img.shields.io/badge/Web_Speech_API-00897B?style=for-the-badge)

### Browser Storage & Utilities
![LocalStorage](https://img.shields.io/badge/LocalStorage-7952B3?style=for-the-badge)
![IndexedDB](https://img.shields.io/badge/IndexedDB-4479A1?style=for-the-badge)
![QRCode](https://img.shields.io/badge/QR_Code-000000?style=for-the-badge&logo=qrcode&logoColor=white)

### Development Tools
![NPM](https://img.shields.io/badge/NPM-CB3837?style=for-the-badge&logo=npm&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)



### Development and build tools

- Node.js and npm (or Bun) for dependency management and scripts.
- TypeScript compiler for type checking.
- `@vitejs/plugin-react` for React integration.
- `@tailwindcss/vite` for Tailwind CSS integration.
- `autoprefixer` and Tailwind CSS tooling.

## Application architecture and data storage

Karigar Connect currently uses a **browser-local storage architecture**. It does not connect to a shared external database in this project version.

### Structured records: localStorage

The application stores its structured database under the `kc_db_v1` key. The schema includes records for users, worker and employer profiles, assessor profiles, trades, competencies, rubric criteria, evidence metadata, assessment requests, badges, jobs, reviews, disputes, tier applications, earnings records, notifications, and audit logs.

The application includes database initialization and migration logic for its current schema version.

The browser session is stored separately under `kc_session_v1`. Passwords are hashed with PBKDF2-SHA256 through the Web Crypto API rather than being stored as plain-text passwords.

### Uploaded files: IndexedDB

Evidence uploads and job photo files are stored in an IndexedDB database named `karigar_connect_files`. The application stores file metadata alongside the structured records and creates browser object URLs for previews.

### What browser-local storage means

Because the current implementation stores application data in the browser:

- Data is local to the browser profile and device where it was created.
- Different users or devices do not automatically share the same records.
- Clearing browser site data can remove locally stored application data and uploaded files.
- This implementation is suitable for a demonstrator/prototype, but it is not a substitute for a production multi-user backend with centralized storage, server-side authentication, authorization, backups, and security controls.

## Getting started

### Prerequisites

- Node.js (use a current LTS release).
- npm, or Bun if you prefer the included `bun.lock` workflow.
- A modern browser.

### Install dependencies

```bash
npm install
```

Or, with Bun:

```bash
bun install
```

### Start the development server

```bash
npm run dev
```

Open:

```text
http://localhost:3000
```

### Available scripts

| Command | Description |
| --- | --- |
| `npm run dev` | Starts the Vite development server on port 3000. |
| `npm run build` | Creates the production build in `dist/`. |
| `npm run preview` | Serves the production build locally for preview. |
| `npm run start` | Runs the Vite preview server on port 3000. |
| `npm run lint` | Runs the TypeScript compiler without emitting files. |
| `npm run clean` | Removes the `dist/` build directory. |

## Environment configuration

The optional AI Problem Finder integration reads the `GEMINI_API_KEY` environment variable on the server side.

For local development, configure the variable in your shell before starting Vite, or use a local environment file that is excluded from version control:

```bash
GEMINI_API_KEY=your_api_key_here
```

Do not commit API keys, credentials, or private environment files to GitHub.

If `GEMINI_API_KEY` is not configured, the Problem Finder is designed to use its offline keyword-based fallback.

## Demo data

The project initializes demonstration records in the browser on first use. These records are intended to help explore the platform's role-based workflows and sample profiles.

Use the demo credentials and account details supplied within the application/project's demonstration data only in a local or otherwise controlled demo environment. Do not reuse demo passwords for real accounts, and do not publish real personal information or credentials.

## Deployment notes

The live application is available at:

**https://karigar-connect-gray.vercel.app/**

The repository contains a Vite client application and a custom Problem Finder middleware registered in `vite.config.ts`. Vite development and preview middleware are not automatically deployed as Vercel serverless functions. Therefore, the deployed frontend should not be assumed to have a working live Gemini endpoint unless the `/api/problem-finder` route has separately been configured on the hosting platform.

For a production deployment, configure the AI endpoint as a server-side function or API service, keep `GEMINI_API_KEY` in the hosting provider's environment settings, and ensure the frontend calls that deployed endpoint. Never expose the API key in client-side code.

Also note that the current localStorage/IndexedDB architecture does not provide shared cross-device data. A production multi-user release would require a centralized backend and database, along with server-side access controls and appropriate data protection.

## Important limitations

- Verification badges are platform assessment records, not government accreditation.
- AI Problem Finder outputs are estimates and are not professional inspections or guaranteed quotations.
- Price guides are indicative and can vary by location, materials, and job conditions.
- Browser-local records are not synchronized across devices or users.
- Browser speech recognition depends on browser support and permissions.
- The current Vite middleware setup requires a separate production API implementation if the AI endpoint is to be available on Vercel.

## Project structure

```text
karigar-connect/
├── public/
│   └── images/                 # Public images used by the application
├── src/
│   ├── assets/                 # Application assets
│   ├── components/
│   │   ├── analytics/          # Demand insights and chart components
│   │   ├── layouts/            # Public and dashboard layouts
│   │   └── ui/                 # Shared UI components
│   ├── context/                # Authentication and toast contexts
│   ├── data/                   # Pakistan cities and service catalogue
│   ├── i18n/                   # English/Urdu translations
│   ├── pages/
│   │   ├── admin/              # Administrator screens
│   │   ├── assessor/           # Assessor screens
│   │   ├── employer/           # Customer/employer screens
│   │   ├── public/             # Public-facing screens
│   │   └── worker/             # Worker screens
│   ├── routes/                 # Protected route handling
│   └── services/
│       └── storage/            # Local API, data engine, auth and file storage
├── index.html
├── package.json
├── tsconfig.json
├── vite.config.ts
└── README.md
```

---

Built to make practical skills easier to demonstrate, assess, and trust.
