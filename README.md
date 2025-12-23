## 🤖 AI-Powered Lead Qualification Engine (n8n + PostgreSQL + OpenAI)

A production-grade automation system that handles 24/7 lead intake via SMS, qualifies prospects using an LLM-driven verification loop, and maintains stateful conversation history in a PostgreSQL database.



## 🎯 The Problem
Home service businesses (Plumbers, HVAC, etc.) lose potential revenue due to:
* **Response Latency:** Leads go cold if not answered within 5 minutes.
* **Incomplete Data:** Back-and-forth texting to get addresses or job details is time-consuming.
* **Data Silos:** Leads trapped in SMS threads instead of a centralized CRM.

## ✨ The Solution
This engine acts as a 24/7 virtual office assistant. It doesn't just "chat"; it follows a logical business process to qualify a lead and push "Ready-to-Quote" data directly to the business owner.

## 🛠️ Technical Stack
* **Orchestration:** [n8n](https://n8n.io/) (Self-hosted/Cloud)
* **LLM:** OpenAI GPT-4o (State-of-the-art reasoning)
* **Database (Memory):** PostgreSQL (Supabase) for long-term session persistence.
* **Communication:** Twilio API (SMS)
* **CRM:** Airtable
* **Security:** SSL/TLS encrypted database connections.

## 🏗️ System Architecture & Logic
I implemented a **Parallel Branching Architecture** to ensure clean user experience and reliable internal triggers:

1.  **Stateful Memory:** Unlike basic bots, this system uses a PostgreSQL-backed memory node. It retrieves the last 10 messages based on the sender's phone number, allowing for multi-day conversations without "context amnesia."
2.  **Verification Loop:** The AI is programmed to summarize gathered details (Problem, Address, Urgency) and ask for explicit user confirmation before finalizing.
3.  **The "Hidden Tag" Trigger:** I used a custom termination signal `[[SUMMARY_COMPLETE]]`.
    * **The User Path:** The system strips this tag using JavaScript regex so the customer never sees "code."
    * **The Internal Path:** A logic gate detects this tag to trigger high-priority email alerts and update the CRM status to `Qualified`.



## 🚀 Key Technical Features
* **Atomic Logging:** Every message (Human and AI) is logged to Postgres with a unique Session ID.
* **Custom Prompt Engineering:** System prompts include strict constraints on SMS character limits and professional tone.
* **Error Handling:** Implemented "Always Output Data" settings to ensure the workflow doesn't break on new leads with zero history.

## 📸 Demo
| User Experience (SMS) | Internal CRM (Airtable) |
| :--- | :--- |
| ![SMS Demo](./assets/sms_demo.gif) | ![Airtable Record](./assets/airtable_record.png) |

## 📁 Repository Structure
* `workflow.json`: The full n8n blueprint (Import into your instance).
* `assets/`: Technical diagrams and screenshots.

---
*Developed by [Your Name] - Specialist in AI Automation & Systems Architecture.*

## Setup (optional)
How someone could run it.

## Notes
Edge cases, rate limits, costs, privacy considerations.
