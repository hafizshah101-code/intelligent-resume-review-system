# AI Resume Review Automation

An end-to-end AI-powered resume review system built with n8n that automatically analyzes uploaded resumes, generates brutally honest feedback using multiple AI agents, and emails a professional review back to the user.

Live website @ Gamma AI --> https://roast-your-resume-hd9d1dt.gamma.site/

---

## Features

- Resume upload via Tally.so - Choose 3 Severity Levels
- PDF text extraction using PDF.co API
- Multi-agent AI review
- Resume Roast
- Resume Writer
- Career improvement suggestions
- Automatic email delivery
- Hosted on Railway
- Fully automated workflow

---

## Architecture

![Architecture](docs/architecture-diagram.png)

---

## Workflow

1. User opens the Gamma landing page.
2. User uploads their resume using the embedded Tally.so form.
3. Tally.so triggers an n8n Webhook.
4. n8n sends the uploaded PDF to PDF.co for text extraction.
5. The extracted resume text is processed by two Gemini AI agents:
   - Resume Rewriter
   - Resume Roast
6. Both AI responses are combined.
7. Gmail automatically emails the final report back to the user.

---
## AI Workflow Design

The system adopts a multi-agent architecture where specialized AI agents perform different tasks using the same Google Gemini model.

- Resume Rewriter Agent
  - Improves wording
  - Enhances professional tone
  - Optimizes ATS compatibility

- Resume Roast Agent
  - Provides brutally honest feedback
  - Identifies weak bullet points
  - Detects vague or generic statements

This agent-based design allows each AI to focus on a dedicated responsibility while sharing a common language model.

---

## Tech Stack

| Technology | Purpose |
|------------|---------|
| n8n | Workflow Automation |
| Gamma.ai | Landing Page |
| Tally.so | Resume Upload Form |
| PDF.co API | PDF Text Extraction |
| Gemini AI | Resume Analysis |
| Gmail | Email Delivery |
| Railway | Cloud Hosting |

---

## AI Agents

### Resume Roast

Get user's input PDF from TallySo and re-direct to PDFCo API to convert-to-text

Get roast level from Webhook Value - input from User

Provides brutally honest feedback about the resume.

Examples:

-Resume Score (/100)  
-ATS Compatibility  
-Strengths
-Weaknesses  
-Missing Skills  
-Suggestions

---

### Resume Rewriter

Get user's input PDF from TallySo and re-direct to PDFCo API to convert-to-text

Evaluates the resume from a hiring manager perspective.

Scores:

- ATS Compatibility
- Professionalism
- Experience
- Skills
- Overall Impression

---

## Workflow Diagram

```
                    User
                      │
                      ▼
         Gamma Landing Page
                      │
                      ▼
          Tally.so Resume Upload
                      │
                 (Webhook)
                      │
                      ▼
             PDF.co HTTP Request
          (Extract PDF to Text)
                      │
          ┌───────────┴───────────┐
          │                       │
          ▼                       ▼
    Resume Rewriter         Resume Roast
      (Gemini AI)            (Gemini AI)
          │                       │
          └───────────┬───────────┘
                      ▼
               Gmail Node
                      │
                      ▼
         Resume Review Sent to User
```

---

## Deployment

Hosted using Railway.

Deployment includes:

- n8n Docker Image
- Persistent Storage
- Environment Variables
- Public Webhook URL

---

## Environment Variables

```

N8N\_HOST=
N8N\_PORT=
WEBHOOK\_URL=

GEMINI\_API\_KEY=
PDFCO\_API\_KEY=

GMAIL\_USER=
GMAIL\_PASSWORD=

```

---

## Example Output

The user receives an email containing:

Here's the brutally honest resume audit HR never gave you.
This review is based on your uploaded resume and is intended to help you improve your chances of landing interviews.
──────────────────────────
{{ $node["Resume Roast"].json.output }}
──────────────────────────
Here's the Rewrite of Your Resume
{{ $node["Resume Rewriter"].json.output }}
──────────────────────────
Remember: a resume doesn't get you the job — it gets you the interview.
The difference between an interview and silence is often just a few weak bullet points, missing keywords, or unclear achievements. Now you know exactly what to fix.

---

## Future Improvements

- GPT-5 Support
- Claude Support
- ATS Keyword Matching
- Job Description Comparison
- Cover Letter Generator
- LinkedIn Profile Review
- Interview Question Generator

---

## Skills Demonstrated

- Workflow Automation
- REST API Integration
- AI Prompt Engineering
- Multi-Agent AI Workflow
- Webhook Integration
- PDF Processing
- Cloud Deployment (Railway)
- Low-Code Automation
- Event-Driven Architecture
- Email Automation

---

## Author

Shah

Portfolio:
https://hafizshah.com

GitHub:
https://github.com/hafizshah101-code
