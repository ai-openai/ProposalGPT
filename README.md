## ProposalGPT - Technical Software Specification  

### **Project Overview**  
ProposalGPT is an AI-powered sales workflow and proposal automation platform that streamlines the sales process from lead capture to project kickoff. It leverages **OpenAI's GPT-based models (ChatGPT o3-mini-high)** for generating tailored proposals, integrates an **AI-driven calling system** for outbound client interactions, and consolidates all sales-related activities into a centralized dashboard. The platform is built on **React, Vite, TypeScript, TailwindCSS, shadcn/ui**, and **Supabase for authentication and backend management**.  

## 📂 **GitHub Repository File Architecture - ProposalGPT**  

Here’s the structured repository architecture for **ProposalGPT**, ensuring a clean, scalable, and maintainable codebase using **React (Vite) + TypeScript + TailwindCSS + shadcn/ui** on the frontend, and **Supabase (PostgreSQL, Auth, Storage, Edge Functions)** for the backend.  

---

### **📁 Root Directory Structure**
```
proposal-gpt/
│── public/                      # Static assets (favicon, logos, etc.)
│── src/                         # Main source code directory
│   ├── components/              # UI Components
│   ├── pages/                   # Page views
│   ├── hooks/                   # Custom React hooks
│   ├── context/                 # Context Providers (Auth, State)
│   ├── services/                # API & Supabase interactions
│   ├── utils/                   # Utility functions
│   ├── types/                   # TypeScript type definitions
│   ├── config/                   # Configurations (API keys, env variables)
│── supabase/                    # Supabase edge functions & database setup
│── scripts/                     # Deployment and setup scripts
│── .env                         # Environment variables
│── package.json                 # Dependencies and scripts
│── tailwind.config.js           # TailwindCSS configuration
│── tsconfig.json                # TypeScript configuration
│── vite.config.ts               # Vite configuration
│── README.md                    # Project documentation
```
---

## **1. Tech Stack**  

- **Frontend:** React (Vite), TypeScript, TailwindCSS, shadcn/ui  
- **Backend & Database:** Supabase (PostgreSQL, Auth, Storage, Edge Functions)  
- **AI Services:** OpenAI API (ChatGPT o3-mini-high) for proposal generation  
- **Telephony:** Twilio (or a similar VoIP API) for AI-driven outbound calls  
- **Real-time Data Processing:** Supabase Edge Functions for handling call transcription and AI insights  
- **Authentication:** Supabase Auth (Email/Password, SSO, OAuth)  
- **Integrations:** CRM & Project Management APIs (HubSpot, Salesforce, Asana, Monday.com)  
- **Deployment:** Vercel or Netlify for frontend, Supabase for backend hosting  

---

## **2. Core Features & Functional Requirements**  

### **2.1 User Authentication & Access Control**  
- **Signup/Login:** Email & Password, OAuth (Google, LinkedIn)  
- **Role-Based Access:** Admin, Sales Rep, Manager  
- **Session Management:** Secure JWT-based authentication via Supabase  

### **2.2 Centralized Sales Dashboard**  
- **Real-time Lead Pipeline:** Track leads from capture to conversion  
- **Proposal Status Tracking:** Draft, Pending Approval, Sent, Accepted, Rejected  
- **Call Logs & Transcriptions:** AI-processed summaries and extracted key details  
- **Client Profiles:** Company information, key decision-makers, past interactions  

### **2.3 AI-Driven Proposal Generation**  
- **GPT-Generated Proposals:** Synthesizing client input, call transcripts, and templates  
- **Template Library:** Pre-built proposal templates with customizable sections  
- **Live Editing & Collaboration:** Real-time proposal editing with team members  
- **Version History:** Track proposal iterations and modifications  

### **2.4 AI-Driven Outbound Calls & Data Capture**  
- **Automated Call Scheduling:** Triggered by new lead creation or follow-up reminders  
- **AI Speech-to-Text Transcription:** Convert call recordings to text  
- **Key Data Extraction:** AI highlights pain points, budget constraints, and timelines  
- **CRM Sync:** Automatically update lead details in connected CRM systems  

### **2.5 Proposal Management & Client Interaction**  
- **Proposal Approval Workflow:** Internal review before sending to clients  
- **Client Engagement Portal:** Clients can view, comment, and approve proposals  
- **E-Signature Integration:** Digital signing via DocuSign or similar APIs  

### **2.6 Integrations with CRM & Project Management Tools**  
- **CRM Sync:** Auto-update leads and deals in HubSpot, Salesforce  
- **Project Kickoff:** Convert approved proposals into project tasks in Asana, Monday.com  

---

## **3. System Architecture**  

### **3.1 Frontend Architecture (React + TypeScript + TailwindCSS)**  
- Component-based UI with **shadcn/ui**  
- Context & State Management via **Zustand or React Query**  
- API Communication via **Supabase Client & REST APIs**  

### **3.2 Backend Architecture (Supabase + OpenAI + Twilio)**  
- **Database:** PostgreSQL (Supabase) with tables for Users, Leads, Proposals, Calls  
- **Authentication:** Supabase Auth (Role-based)  
- **Edge Functions:** Handle AI-based text processing & CRM sync  
- **Storage:** Proposal PDFs stored in Supabase Storage  

---

## **4. API Design**  

### **4.1 Authentication API (Supabase Auth)**  
- `POST /auth/signup` – Register new users  
- `POST /auth/login` – Authenticate users  
- `POST /auth/logout` – Logout endpoint  

### **4.2 Proposal API**  
- `GET /proposals` – Fetch proposals by user  
- `POST /proposals` – Generate a new AI-powered proposal  
- `PUT /proposals/:id` – Update an existing proposal  
- `DELETE /proposals/:id` – Delete a proposal  

### **4.3 AI-Calling API (Twilio + OpenAI)**  
- `POST /calls/initiate` – Trigger an AI-powered call  
- `GET /calls/transcriptions` – Fetch call transcriptions  
- `POST /calls/analyze` – Process transcription with GPT for insights  

### **4.4 CRM Integration API**  
- `POST /crm/sync` – Sync lead data to connected CRM  
- `GET /crm/leads` – Fetch leads from CRM  

---

## **5. Database Schema (Supabase PostgreSQL)**  

### **Users Table**  
| Column       | Type         | Description                     |  
|-------------|------------|---------------------------------|  
| id          | UUID       | Primary Key                     |  
| email       | TEXT       | User Email (Unique)             |  
| role        | TEXT       | Role (Admin, Sales, Manager)    |  
| created_at  | TIMESTAMP  | Timestamp of registration       |  

### **Leads Table**  
| Column       | Type         | Description                     |  
|-------------|------------|---------------------------------|  
| id          | UUID       | Primary Key                     |  
| user_id     | UUID       | Foreign Key to Users Table      |  
| name        | TEXT       | Lead Name                       |  
| status      | TEXT       | Status (New, In Progress, Won)  |  

### **Proposals Table**  
| Column       | Type         | Description                     |  
|-------------|------------|---------------------------------|  
| id          | UUID       | Primary Key                     |  
| user_id     | UUID       | Foreign Key to Users Table      |  
| lead_id     | UUID       | Foreign Key to Leads Table      |  
| content     | TEXT       | AI-generated Proposal           |  
| status      | TEXT       | Status (Draft, Sent, Approved)  |  

### **Calls Table**  
| Column       | Type         | Description                     |  
|-------------|------------|---------------------------------|  
| id          | UUID       | Primary Key                     |  
| user_id     | UUID       | Foreign Key to Users Table      |  
| lead_id     | UUID       | Foreign Key to Leads Table      |  
| transcript  | TEXT       | AI-generated Call Transcript    |  
| summary     | TEXT       | AI-generated Call Summary       |  

---

## **6. UI Components (React + shadcn/ui)**  

### **Dashboard Page (`/dashboard`)**  
- **Lead Pipeline Widget**  
- **Active Proposal List**  
- **Recent Calls & AI Summaries**  

### **Proposal Editor (`/proposals/:id`)**  
- **AI Proposal Generation Button**  
- **Rich Text Editor with Versioning**  

### **Call Management (`/calls`)**  
- **Call History with AI Insights**  
- **AI-Driven Follow-up Recommendations**  

### **Client Portal (`/client/:id`)**  
- **Proposal Viewer & E-Signature Support**  
- **Commenting & Approval System**  

---

## **7. Deployment & Hosting Strategy**  
- **Frontend:** Hosted on Vercel (React + Vite)  
- **Backend:** Supabase managed PostgreSQL & Edge Functions  
- **AI Services:** OpenAI API for proposal & transcription analysis  
- **Telephony:** Twilio (VoIP for AI-driven calls)  

---

## 📂 **Detailed File Breakdown**
Below is a breakdown of all important files and directories:

### **📂 `src/components/` - Reusable UI Components**
```
components/
│── Navbar.tsx                   # Navigation bar
│── Sidebar.tsx                  # Sidebar menu
│── Button.tsx                   # Reusable button component
│── Modal.tsx                    # Generic modal component
│── Loader.tsx                   # Loading spinner
│── Card.tsx                      # Generic card component
│── Input.tsx                     # Custom input component
│── ProposalEditor.tsx            # AI-powered proposal editor
│── CallTranscript.tsx            # AI-generated call transcript viewer
│── CRMIntegration.tsx            # CRM integration widget
```

### **📂 `src/pages/` - Page Views**
```
pages/
│── Dashboard.tsx                 # Main dashboard
│── Login.tsx                     # User login page
│── Signup.tsx                    # Signup page
│── Proposals.tsx                 # List of AI-generated proposals
│── ProposalDetail.tsx            # Proposal details & editing
│── Calls.tsx                      # Call logs & AI transcription analysis
│── CRM.tsx                        # CRM integration settings
│── Settings.tsx                   # User settings
│── NotFound.tsx                   # 404 Page
```

### **📂 `src/hooks/` - Custom Hooks**
```
hooks/
│── useAuth.ts                     # Authentication logic using Supabase
│── useProposals.ts                 # Fetch and manage AI-generated proposals
│── useCalls.ts                     # Handle AI-driven call logs
│── useCRM.ts                        # CRM API integration
```

### **📂 `src/context/` - Context Providers**
```
context/
│── AuthContext.tsx                 # Provides authentication state
│── ProposalContext.tsx             # Manages proposal-related state
│── CallContext.tsx                  # Handles AI call logs & summaries
```

### **📂 `src/services/` - API & Supabase Interactions**
```
services/
│── authService.ts                  # User authentication API (Supabase)
│── proposalService.ts               # AI-based proposal management
│── callService.ts                   # AI-driven call logs and transcriptions
│── crmService.ts                    # CRM integration API calls
│── supabaseClient.ts                 # Supabase client configuration
```

### **📂 `src/utils/` - Utility Functions**
```
utils/
│── formatDate.ts                    # Helper function to format dates
│── apiHelper.ts                      # Fetch wrapper with error handling
│── aiParser.ts                        # AI-based response processing
```

### **📂 `src/types/` - TypeScript Type Definitions**
```
types/
│── authTypes.ts                      # Types for authentication
│── proposalTypes.ts                   # Proposal-related types
│── callTypes.ts                        # AI call log types
│── crmTypes.ts                         # CRM integration types
```

### **📂 `supabase/` - Edge Functions & Database**
```
supabase/
│── functions/
│   ├── generateProposal.ts            # AI-powered proposal generation (GPT-4)
│   ├── transcribeCall.ts               # AI call transcription processing
│   ├── analyzeCall.ts                  # Extract key data from transcriptions
│── migrations/
│   ├── 001_create_users.sql             # User table schema
│   ├── 002_create_proposals.sql         # Proposals table schema
│   ├── 003_create_calls.sql             # Calls table schema
│── storage/
│   ├── proposals/                        # PDF & document storage
```

### **📂 `scripts/` - Deployment & Setup Scripts**
```
scripts/
│── deploy.sh                           # Deployment script for Vercel/Supabase
│── dbSetup.sql                         # Initial database setup script
```
