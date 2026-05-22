# Distributor-Scorecard-AI-Agent

<img width="1265" height="378" alt="Distributor Scorecard AI Agent" src="https://github.com/user-attachments/assets/80f93ef7-285c-4569-a467-c63018b1161c" />

## Overview

The **Distributor Performance Scorecard Bot** is an intelligent workflow automation system designed for FMCG companies managing distributor networks at scale.

Every Monday at 8:00 AM, the system automatically:

* Reads weekly distributor sales submissions from Google Sheets
* Validates and enriches data
* Calculates KPI-based performance scores
* Ranks all distributors network-wide
* Generates AI-powered coaching commentary
* Sends personalized HTML scorecards via email
* Delivers an executive leaderboard report to management
* Logs every activity for auditing and analytics

The solution replaces manual spreadsheet reporting workflows that typically consume **3–5 hours every week** and transforms them into a fully automated decision-support system.

---

# Key Features

## Automated Weekly Reporting

* Scheduled execution every Monday at 8 AM
* Zero manual intervention required

## KPI-Based Distributor Ranking

Weighted scoring model using:

* Volume Achievement
* Outlet Coverage
* Week-on-Week Growth
* Returns Rate

## AI Coaching Commentary

LLM-generated:

* Performance observations
* Actionable recommendations
* Executive-level sales summaries

## Personalized HTML Scorecards

Each distributor receives:

* KPI breakdown
* Rank badge
* Performance tier
* AI coaching insights
* Motivational messaging

## National Sales Dashboard Email

Management receives:

* Full distributor leaderboard
* Top and bottom performers
* AI-generated executive brief
* Network health analysis

## Built-In Logging & Audit Trail

* Error tracking
* Delivery logs
* Historical performance archive
* Validation reporting

---

# Business Problem

FMCG companies often manage **10–50+ distributors** using fragmented spreadsheet processes.

This creates several operational issues:

* Manual reporting consumes valuable management time
* Performance comparisons are inconsistent
* Poor performers avoid accountability
* High performers receive no recognition
* Sales leadership lacks data-driven visibility

The Distributor Performance Scorecard Bot solves this by introducing:

* standardized scoring,
* transparent benchmarking,
* automated communication,
* and AI-assisted sales intelligence.

---

# Tech Stack

| Technology                  | Purpose                  |
| --------------------------- | ------------------------ |
| n8n                         | Workflow orchestration   |
| Google Sheets               | Database & configuration |
| Gmail                       | Email delivery           |
| OpenAI GPT-4o mini / Claude | AI commentary generation |
| Google Cloud Console        | OAuth credentials        |

---

# System Architecture

```text
┌────────────────────┐
│ Weekly Sales Data  │
│   Google Sheets    │
└─────────┬──────────┘
          │
          ▼
┌────────────────────┐
│  n8n Schedule      │
│ Trigger (Monday)   │
└─────────┬──────────┘
          │
          ▼
┌────────────────────┐
│ Validation & KPI   │
│ Score Calculation  │
└─────────┬──────────┘
          │
          ▼
┌────────────────────┐
│ AI Commentary      │
│ (GPT-4o / Claude)  │
└─────────┬──────────┘
          │
          ▼
┌────────────────────┐
│ HTML Scorecards    │
│ + Leaderboards     │
└─────────┬──────────┘
          │
          ▼
┌────────────────────┐
│ Gmail Delivery     │
└─────────┬──────────┘
          │
          ▼
┌────────────────────┐
│ Logging & Archive  │
└────────────────────┘
```

---

# Workflow Pipeline

## 1. Schedule Trigger

* Executes every Monday at 8:00 AM
* Timezone: `Asia/Karachi`

## 2. Read Weekly Sales Data

Fetches distributor submissions from Google Sheets.

## 3. Filter Reporting Week

Processes only the previous reporting week.

## 4. Validation Engine

Checks:

* Required fields
* Numeric formats
* Distributor existence
* Active status

## 5. KPI Calculation

Calculates:

* Volume Achievement %
* Coverage Rate %
* Week-on-Week Growth %
* Returns Rate %

## 6. Composite Scoring

Weighted scoring model:

* Volume → 40%
* Coverage → 30%
* Growth → 20%
* Returns → 10%

## 7. AI Commentary

LLM generates:

* Personalized coaching
* Recommendations
* Executive summary

## 8. HTML Scorecard Generation

Creates professional distributor reports.

## 9. Email Delivery

* Individual distributor scorecards
* National sales leaderboard

## 10. Logging & Historical Archive

Writes:

* Report logs
* Error logs
* Historical KPI data

---

# Google Sheets Database Structure

## Tabs Used

| Tab Name           | Purpose                      |
| ------------------ | ---------------------------- |
| Weekly Sales Data  | Raw weekly submissions       |
| Distributor Config | Email/configuration settings |
| System Config      | Global system settings       |
| Report Log         | Execution logs               |
| Error Log          | Validation & email failures  |
| Historical Data    | KPI history archive          |

---

# KPI Formula Logic

## Volume Achievement

\text{Volume Achievement %} = \frac{\text{Sales Value}}{\text{Weekly Target}} \times 100

## Coverage Rate

\text{Coverage Rate %} = \frac{\text{Outlets Covered}}{\text{Outlet Target}} \times 100

## Week-on-Week Growth

\text{WoW Growth %} = \frac{\text{Current Week Sales} - \text{Historical Sales}}{\text{Historical Sales}} \times 100

## Returns Rate

\text{Returns Rate %} = \frac{\text{Returns Cases}}{\text{Sales Volume Cases}} \times 100

---

# Performance Tiers

| Tier     | Score Range |
| -------- | ----------- |
| Elite    | 80+         |
| On Track | 60–79       |
| At Risk  | 40–59       |
| Critical | Below 40    |

---

# AI Intelligence Layer

The system uses an LLM as a virtual FMCG sales coach.

### AI Generates:

* Distributor performance observations
* Tactical improvement recommendations
* Executive summaries for leadership

### Example Output

#### Observation

> “Ahmed Distributors achieved 118% of volume target while expanding outlet coverage significantly across the North region.”

#### Recommendation

> “Focus on reducing returns in the DHA territory where return rates exceeded the network average by 3×.”

---

# Error Handling

## Validation Errors

Logged automatically to the `Error Log` tab.

## Gmail Failures

* Logged individually
* Workflow continues processing remaining distributors

## AI API Failure

Fallback commentary is automatically used.

## No Data Scenario

Workflow exits safely without sending emails.

---

# Scalability

Designed to scale across:

* 10 distributors
* 50 distributors
* 100+ distributors

### Scaling Features

* Batch processing
* Config-driven scoring
* Region-based filtering
* Duplicate-run prevention
* Dynamic onboarding

---

# Installation Guide

## 1. Clone Repository

```bash
git clone https://github.com/yourusername/distributor-scorecard-bot.git
cd distributor-scorecard-bot
```

---

## 2. Setup Google Sheets

Create a spreadsheet with the following tabs:

```text
- Weekly Sales Data
- Distributor Config
- System Config
- Report Log
- Error Log
- Historical Data
```

---

## 3. Configure Google Cloud

Enable:

* Google Sheets API
* Gmail API

Create OAuth credentials.

---

## 4. Setup n8n

Import the workflow JSON into n8n.

Required credentials:

* Google Sheets
* Gmail
* OpenAI / Anthropic

---

## 5. Configure Environment Variables

```env
OPENAI_API_KEY=your_api_key
GOOGLE_SHEETS_CREDENTIALS=your_credentials
GMAIL_APP_PASSWORD=your_password
```

---

# Example Workflow Output

## Distributor Email

* Composite Score
* Rank Badge
* KPI Cards
* AI Coaching
* Motivational Footer

## Executive Email

* Full leaderboard
* Top 3 distributors
* Bottom 3 distributors
* National trend analysis

---

# Demo Scenario

| Distributor  | Sales PKR | Target PKR | Expected Tier |
| ------------ | --------- | ---------- | ------------- |
| Omar Dist    | 520,000   | 400,000    | Elite         |
| Ahmed Dist   | 450,000   | 400,000    | Elite         |
| Fatima Corp  | 280,000   | 300,000    | On Track      |
| Malik Bros   | 185,000   | 350,000    | At Risk       |
| Raza Traders | 95,000    | 350,000    | Critical      |

---

# Business Impact

## Time Savings

* Eliminates 150–250 manual reporting hours annually

## Revenue Impact

* Improves distributor accountability
* Encourages healthy competition
* Identifies weak territories earlier

## Strategic Decision-Making

* Data-driven territory reviews
* Automated benchmarking
* Faster intervention cycles

---

# Monetization Model

| Offering         | Pricing             |
| ---------------- | ------------------- |
| Pilot Deployment | PKR 80,000–120,000  |
| Full Deployment  | PKR 250,000–400,000 |
| Monthly Retainer | PKR 25,000–40,000   |

---

# Future Enhancements

Planned upgrades:

* WhatsApp alerts
* Power BI dashboard integration
* Monthly trend analytics
* Territory heatmaps
* Distributor mobile portal
* Predictive churn scoring

---

# Security Considerations

* OAuth-secured Google APIs
* Credential isolation in n8n
* Config-driven access control
* Audit logging for all executions

---

# Repository Structure

```text
.
├── workflows/
│   └── distributor-scorecard-workflow.json
├── docs/
│   └── architecture-diagram.png
├── templates/
│   └── distributor-email-template.html
├── samples/
│   └── sample-sales-data.csv
├── README.md
└── LICENSE
```

---

# Why This Project Matters

This project demonstrates how modern AI automation can transform traditional FMCG operations by combining:

* workflow automation,
* AI-generated intelligence,
* analytics,
* and automated communication

into a single scalable business system.

It is not just an automation workflow — it is an operational intelligence platform for distributor management.

---

# Author

**Your Name**
AI Automation Developer | n8n Systems Builder | AI Workflow Consultant

---

# License

This project is licensed under the MIT License.

---

# Support

For deployment support, workflow customization, or enterprise implementation:

* Open an issue
* Submit a pull request
* Contact via LinkedIn or email

---
