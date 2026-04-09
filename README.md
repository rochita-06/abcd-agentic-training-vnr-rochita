# abcd-agentic-training-vnr-rochita
<div align="center">
  <h1>🚀 NextGen AI Resume Screening</h1>
  <p>An intelligent recruitment platform connecting a modern Next.js applicant portal to an AI-powered n8n automation engine to automatically assess, score, and manage applicant resumes.</p>
</div>

<br />

## 1. Business Problem
Manual screening of candidate resumes is extremely time-consuming for Human Resources departments. It often results in human bias, slow candidate response times, and the potential to overlook highly qualified candidates buried deep within a large applicant pool. A slow screening pipeline ultimately leads to delayed hiring timelines and a poor candidate experience.

## 2. Possible Solution
By introducing Artificial Intelligence into the initial screening layer, companies can automatically parse, read, and score candidate resumes against specified job criteria the moment they are uploaded. This drastically speeds up the shortlisting process, letting HR professionals focus only on high-quality matches.

## 3. Implemented Solution
We built an end-to-end "NextGen Recruiter" AI-powered candidate screening platform. 
1. **Candidate Portal**: A premium, responsive interface where applicants can securely drag-and-drop their resumes and enter their emails.
2. **AI Automation**: The frontend passes this data securely to a cloud-based **n8n Automation Sandbox** via a webhook trigger. The n8n engine evaluates the resume using an LLM.
3. **HR Tracking Pipeline**: Once evaluation is complete, n8n sends a webhook back to our system to update the local database. The HR team is provided with an integrated `/hr` administrative dashboard containing real-time candidate scores, target roles, and automated accept/reject statuses.

## 4. Tech Stack Used
- **Frontend Core**: Next.js 14, React 18, TypeScript
- **Styling**: Tailwind CSS, PostCSS, Glassmorphism aesthetics
- **Animations & Icons**: Framer Motion, Lucide React
- **Upload Utility**: React Dropzone
- **Backend API**: Next.js App Router API Routes (`/api/upload`, `/api/update-status`)
- **Database**: Local JSON storage mechanism for uncoupled prototyping ([db.json](cci:7://file:///C:/Users/rochi/OneDrive/Desktop/agentic%20ai/resume-app/src/data/db.json:0:0-0:0))
- **Automation / AI Engine**: n8n Cloud Webhooks

## 5. Architecture Diagram
```mermaid
graph TD;
    Applicant([Applicant]) -->|Submit Resume & Email| Frontend[Next.js App Portal]
    Frontend -->|POST formData| UploadAPI[/api/upload]
    UploadAPI -->|Multipart Webhook Request| n8n([n8n Cloud Engine])
    n8n -->|Parse & AI Match Resume| n8n
    n8n -->|HTTP POST Match Score| UpdateAPI[/api/update-status]
    UploadAPI -.->|Init Pending Status| Database[(Local db.json)]
    UpdateAPI -.->|Push AI Status Result| Database
    Database -.->|Read Sync| Dashboard[Next.js HR Dashboard]
    Recruiter([HR Recruiter]) -->|Review Pipeline| Dashboard
