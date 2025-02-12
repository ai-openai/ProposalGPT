## ProposalGPT - Technical Software Specification  

### **Project Overview**  
ProposalGPT is an AI-powered sales workflow and proposal automation platform that streamlines the sales process from lead capture to project kickoff. It leverages **OpenAI's GPT-based models (ChatGPT o3-mini-high)** for generating tailored proposals, integrates an **AI-driven calling system** for outbound client interactions, and consolidates all sales-related activities into a centralized dashboard. The platform is built on **React, Vite, TypeScript, TailwindCSS, shadcn/ui**, and **Supabase for authentication and backend management**.  

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

### **Next Step**  
Reply with **"build"** to receive the complete GitHub repository structure and detailed file architecture.


# ProposalGPT

## Description

ProposalGPT is an AI-powered sales workflow and proposal automation platform designed to streamline the entire sales process from lead capture to project kickoff. It leverages advanced GPT-based models (OpenAI's flagship ChatGPT o3-mini-high) to generate highly tailored proposals by synthesizing customer inputs, expert feedback, and real-time call transcriptions. The platform employs an AI-driven calling system that autonomously gathers critical client data during outbound calls, transcribing and analyzing responses to ensure all key details are captured. With an integrated, centralized dashboard, ProposalGPT consolidates project details, call logs, and generated content, providing sales teams with a comprehensive view of each opportunity. Built on a cloud-based tech stack that includes Supabase for backend management and React with TailwindCSS for a dynamic user interface, it ensures scalability and robust data security. Its tiered subscription model targets mid-size to enterprise customers while offering extensibility to integrate with popular CRMs and project management tools. Overall, ProposalGPT transforms traditional proposal development into an efficient, automated, and data-driven process that significantly reduces manual intervention.

## Final Recommendations
Based on the above research and analysis, here are our recommendations for building ProposalGPT efficiently with the given constraints:

### Adopt Twilio for AI Calling (Primary Recommendation)
Twilio’s rich feature set and reliable API make it a strong fit for our voice component. It integrates well with our stack – we can handle call logic server-side and use Supabase to log and trigger events. Twilio’s quickstart examples (calling OpenAI GPT on a call) will accelerate development​. While Vonage offers cost savings, Twilio’s ecosystem and support may shorten our dev time, which is critical in early stages. We recommend using Twilio Programmable Voice with Media Streams for real-time transcription, combined with OpenAI’s API for understanding/responding to the user. This combo has been proven to work (Twilio’s demo integration with ChatGPT) and will let us achieve natural conversations. We should budget for Twilio’s higher call costs; if scale grows and cost becomes an issue, we can later optimize (e.g., switch to Vonage or negotiate volume discounts). For now, Twilio’s developer experience and Supabase integration examples (even Supabase docs show Twilio usage)​ outweigh the pure cost concern.

### Leverage OpenAI's flagship ChatGPT o3-mini-high for Proposal Generation, with an option to incorporate Claude for large contexts
OpenAI o3-mini-high should be our default engine for generating proposal content due to its superior output quality and reasoning​. We can use o3-mini-high for the core proposal narrative and important sections that require nuance. However, we should also utilize o3-mini-low for faster, smaller tasks (like creating an outline or summarizing call notes) to optimize cost. Additionally, we recommend integrating Anthropic Claude specifically for cases where a very large input (like a detailed requirements document or lengthy call transcript) must inform the proposal. Claude can ingest it in one go with its 100k context, then either produce a draft or feed key info to o3-mini-high. By combining the strengths of both (maybe an ensemble approach), ProposalGPT can handle a variety of scenarios robustly. Technically, this means building a layer in our app that decides which model to use based on input size or perhaps user preference (e.g., a “fast mode” using cheaper models vs “premium mode” with o3-mini-high). In terms of workflow automation, we should create a template structure for proposals (even if just in markdown) and prompt the AI to fill sections (executive summary, scope, timeline, pricing, etc.). This will yield more organized output than a free-form essay. Because hallucination is a risk, we must implement verification steps – e.g., the AI should explicitly state any assumptions it’s making, and we then either verify via data or prompt the user to confirm.

### Start with Built-In Project Management (Phase 1) and Plan for Integrations (Phase 2)
To get an MVP out quickly and keep users in one platform, we recommend implementing a basic project management module within ProposalGPT initially. This could be as simple as a Kanban board of tasks derived from the proposal. Supabase can handle this easily (a tasks table with fields like title, status, assignee). We can use ShadCN UI components to build a clean task board. This addresses the immediate need (“I got the project, now what are the next steps?”) without requiring the user to use another tool. However, we should design it in a way that an external integration can be added later or in parallel. For instance, when a proposal is accepted, show the tasks in our UI and offer a button “Send to Asana” or “Create in Monday.com”. Given the popularity and capabilities of Asana and Monday, and the fact that competitors integrate with PM tools, providing those options will be important for users who already have established workflows.  Our recommendation is to prioritize an Asana integration after the MVP, since Asana strikes a balance of robust features and wide adoption. Monday.com can follow if demanded by users (or if we find mid-market clients preferring it). Technically, this means building an integration service within our app that handles OAuth and project creation when triggered. By phasing it this way, we keep initial development simple but leave room to cater to power users. Over time, if our user base gravitates toward using external PM exclusively, we can choose to either keep the internal PM minimal or drop it. But having it at start ensures no user is left hanging if they don’t use a PM tool.

### Emphasize Integration and Extensibility
Ensure that from day one, ProposalGPT can plug into CRMs (at least import contacts or company info) and export data to other systems. Even if not fully implemented at launch, architect the system with integration in mind. For example, design our data models similar to common CRM/PM concepts (so mapping fields is easier), and keep the code modular (e.g., a service for “on proposal win” that can have multiple handlers – one for internal tasks, one to call Asana API, etc.). This will make it easier to add connections to HubSpot, Salesforce, or others. The reason is twofold: it de-risks competition from the big CRM players (we complement them rather than fight outright) and it adds value for users by fitting into their existing sales stack. Recommendation: Use Supabase Functions or a backend router to create a small integration layer (possibly use libraries or services like Zapier or n8n for quick wins, though for core features native integration is better). Possibly we can use an approach like Trigger.dev or Work OS for orchestrating external calls in response to events, which could simplify building those links.

### Quality and Testing with Real Use-Cases
We should pilot the platform in a specific domain initially (perhaps IT services proposals, marketing proposals, etc.) to fine-tune the AI prompts and calling scripts. This will help us curate prompt templates and fallback answers for the AI call (for example, if the prospect asks something the AI doesn’t know, have a strategy like scheduling a human follow-up). Recommendation: Use a small group of friendly users to run through a full cycle and gather feedback. Compare the proposals generated by ProposalGPT vs. ones written by humans or competitors. Identify gaps (did the AI omit a section that is standard? did it over-promise something?). This will guide prompt engineering and possibly some business logic (like a “sanity check” on the proposal content). Also, test the voice agent thoroughly – measure call success, look at where it fails. This could involve plugging the call transcripts into something like Gong for analysis to see how customers react (an ironic but useful idea).

## Differentiating Features to Develop

To stand out, we recommend a couple of features building on our tool choices:

### Call-Proposal Linkage
Because we have both call transcription and proposal generation, we can do smart things like highlight in the proposal key phrases or requirements that were mentioned by the client on the call (this shows attentiveness). Perhaps even include a “Here’s what you told us:” section that the AI populates from the call transcript – that personalizes the proposal. This leverages the integration of Twilio (transcript) and GPT (text generation) in a way competitors likely don’t.

### AI-assisted Task Breakdown
After a proposal is accepted, use GPT to break down the project into tasks (maybe using the function calling as mentioned). Then either create them in our PM module or external tool. This saves project managers time and is a slick innovation beyond just the proposal. It uses the same tech stack pieces we have, just in another creative way.
Analytics and Continuous Learning: Use Supabase to log outcomes – e.g., whether proposals were won or lost, and feed that back into improving the AI. Over time, we might discover patterns (“proposals that include a certain case study have higher close rate”) and the AI could learn to incorporate those or suggest improvements. Euraiqa touts analytics to optimize the sales process, and we should too. Early on, this could simply be tracking metrics and making them visible to the team (time saved, call durations, proposal acceptance rate). Eventually, an ML layer could adjust the AI’s behavior based on these metrics.

### Focus on User Experience and Trust
From content tone to hand-off points, ensure the AI feels like a helpful assistant, not a clippy-esque annoyance. For calls, we likely have the AI qualify and gather info, but a human may still close the deal – so maybe the AI schedules a meeting with a human rep at the end of the call for complex questions. In proposals, allow the salesperson to edit anything before sending, and maybe even include a sidebar with “AI suggestions” rather than directly sending if the user prefers control. These options can reduce the fear and actually become a selling point (“you’re always in control, but you have a super-assistant doing the heavy lifting”). Given our tools, implementing an edit interface (React, with a Tailwind UI) and a toggle for AI suggestions is doable.

In summary, our plan is to use Twilio + o3-mini-high + Supabase as the backbone for a powerful MVP, with Claude and others as supporting tools for special cases, and an initial simple project tracker to complete the workflow loop. This combination covers all PRD requirements with the least friction and highest chance of delivering a “wow” factor to users. We should keep an eye on direct competitors like Euraiqa and established players adding AI, but by moving fast and focusing on the integrated experience, ProposalGPT can carve out a strong position in the AI-driven sales automation space.
