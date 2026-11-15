

https://github.com/user-attachments/assets/87623ee3-cc46-4157-b851-57e5fd03adc1

# 🚀 Enterprise B2B AI Lead Engine & Autonomous CRM Agent (n8n + Supabase + Gemini)

A production-ready, fault-tolerant B2B data ingestion, web enrichment, AI scoring, and autonomous CRM system built on self-hosted **n8n**, **PostgreSQL (Supabase)**, and **Google Gemini LLM**.

---

## 🏗️ System Architecture & Blueprints Overview

| Module | File Name | Core Technologies | Primary Engineering Function | Fault Tolerance / Pattern |
| :--- | :--- | :--- | :--- | :--- |
| **00** | `00_GLOBAL_ERROR_HANDLER.json` | Error Trigger, Centralized Logging | Captures runtime exceptions across all production pipelines | Global Fail-Safe Catch |
| **01** | `01_B2B_Lead_Sanitizer.json` | Webhook, JavaScript (`Code`), Google DNS API | Normalizes raw payloads, blocks free/disposable domains, verifies active `MX` records | Strict Input Gatekeeping |
| **02** | `02_B2B_Company_Scraper.json` | HTTP Request, HTML Extraction | Scrapes live corporate websites from verified lead email domains | `On Error: Continue` (HTTP 403/Anti-Bot Bypass) |
| **03** | `03_B2B_AI_Lead_Qualifier.json` | Google Gemini LLM, Structured Output Parser | Extracts industry vertical, B2B fit, and company profile into strict JSON schema | Deterministic JSON Enforcement |
| **04** | `04_B2B_AI_Scoring_Engine.json` | Gemini LLM, Custom Scoring Prompt | Calculates numerical `lead_score` (1–100) and generates personalized B2B `icebreaker` | `Retry On Fail` (3x / 5000ms for HTTP 503 resilience) |
| **05** | `05_B2B_VIP_Lead_Router.json` | Conditional Router (`If`), Supabase (PostgreSQL) | Routes high-value leads (`lead_score >= 92`) directly into cloud PostgreSQL `vip_leads` table | Dual-Path Routing (`true` / `false`) |
| **06** | `06_B2B_AI_CRM_Agent.json` | AI Agent, Window Buffer Memory, Supabase Tools | Conversational AI Assistant capable of querying and inserting SQL records via natural language | Dynamic AI Field Mapping (`✨`) |
| **07** | `07_B2B_VIP_Instant_Outreach.json` | End-to-End Pipeline + Automated Outreach Composer | Assembles hyper-personalized outbound B2B emails immediately upon PostgreSQL insertion | Sub-4-Second Speed-to-Lead Execution |

---

## 💼 Business Problem & ROI Impact

* **Sub-4-Second Speed-to-Lead:** Replaces 15–20 minutes of manual SDR research (domain checking, website reading, CRM entry, and email drafting) with a **3.71-second** automated execution pipeline.
* **Zero API Crash Downtime:** Built-in fallback paths ensure that Cloudflare/403 blocks on target websites or temporary LLM API overloads (503) never halt lead ingestion.
* **Natural Language SQL Interface:** Non-technical sales executives can query top-performing leads or insert unstructured meeting notes directly into PostgreSQL via the Autonomous AI Agent (`Module 06`).

---

## 🛠️ Tech Stack

* **Orchestration & Logic:** n8n (Self-Hosted), JavaScript (ES6 in Code Nodes)
* **Database & Storage:** Supabase (Managed PostgreSQL)
* **AI & Agentic Framework:** Google Gemini (`gemini-3.1-flash-lite-preview`), LangChain Tool Calling, Structured Output Parsing, Window Buffer Memory
* **Network & Validation:** REST APIs, Google Public DNS (`dns.google/resolve` for MX verification)
