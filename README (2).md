<div align="center">

# 🏦 AI Loan Eligibility Checker (BFSI)

**An AI-powered web platform for smarter financial decisions**

Dark glassmorphism UI · Claude AI · Google Sheets storage

</div>

---

## 📑 Contents
[Features](#-features) · [Setup](#-setup) · [Deploy](#️-deploy-github-pages-cant-run-node) · [Project Report](#-project-report)

## ✨ Features

| Module | Description |
|---|---|
| ✅ **Loan Eligibility Checker** | Eligibility, approval score, interest rate, EMI and maximum loan |
| 📊 **Credit Score Analyzer** | Estimated score (300–900) with risk band and AI improvement tips |
| 🧮 **EMI Calculator** | Real-time EMI, total interest and total payable with sliders |
| 🤖 **AI Financial Tips** | Ask Claude any question about loans, savings, credit or insurance |

## 🧱 Tech Stack
**Frontend:** HTML, CSS, JavaScript · **Backend:** Node.js, Express · **AI:** Anthropic Claude API · **Database:** Google Sheets (Apps Script)

## 📁 Structure
- `public/` frontend (HTML, CSS, JS)
- `server.js` Node/Express backend (Claude proxy + Sheets proxy; keys stay server-side)
- `apps-script/Code.gs` Google Sheets backend

## 🚀 Setup
1. Google Sheet > Extensions > Apps Script > paste `Code.gs`, set `SECRET` > Deploy > Web app (Execute as: Me, Access: Anyone) > copy URL.
2. `cp .env.example .env` and fill in `ANTHROPIC_API_KEY` (console.anthropic.com), `SHEET_URL`, `SHEET_SECRET`.
3. `npm install && npm start` then open http://localhost:3000

> Quick look without setup: double-click `public/index.html`. The calculators work; AI and Sheets need the server.

## 📤 Push to GitHub
```
git init && git add . && git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/ai-loan-checker.git
git push -u origin main
```
`.env` is git-ignored, so never commit keys.

## ☁️ Deploy (GitHub Pages can't run Node)
Render.com > New Web Service > connect repo > Build `npm install`, Start `npm start` > add the 4 env vars.

---

# 📄 Project Report

**Domain:** BFSI (Banking, Financial Services & Insurance)
**Technologies:** HTML, CSS, JavaScript, Node.js, Express, Anthropic Claude API, Google Sheets (Apps Script)

## 1. Abstract
The AI Loan Eligibility Checker is a web platform that helps users make quick personal-finance decisions. It combines four tools in one interface: a Loan Eligibility Checker, a Credit Score Analyzer, an EMI Calculator and AI Financial Tips. Results are generated instantly in the browser, Claude AI adds personalized recommendations, and user records are stored in Google Sheets.

## 2. Problem Statement
Many people do not know whether they qualify for a loan, what their credit health looks like, or what their monthly repayment will be until they visit a bank. This causes failed applications, unnecessary credit enquiries and poor borrowing decisions. A free, instant, easy-to-use tool can fix this.

## 3. Objectives
- Build modules for loan eligibility, credit score analysis, EMI calculation and AI tips
- Design a responsive dark glassmorphism interface
- Validate all user inputs with JavaScript
- Predict loan eligibility from income, age, credit score and employment
- Calculate EMI in real time using the standard financial formula
- Integrate the Claude AI API for intelligent guidance
- Store and retrieve records using Google Sheets
- Keep API keys and data private through a secure backend

## 4. System Architecture

```
 Browser (HTML/CSS/JS)
        │
        ▼
 Node.js + Express server  ──►  Anthropic Claude API   (AI advice)
        │
        └──────────────────►  Google Apps Script  ──►  Google Sheet (records)
```

The browser never talks to Claude or Google directly. The Express server holds the secrets and forwards requests, which protects the API key.

## 5. Modules

| # | Module | What it does |
|---|--------|--------------|
| 1 | **Loan Eligibility Checker** | Takes name, age, income, employment, credit score, existing EMIs and loan details. Returns eligibility, approval score, estimated rate, EMI and maximum loan. Saves each check to Google Sheets. |
| 2 | **Credit Score Analyzer** | Estimates a score from 300 to 900 and a risk band using payment history, utilization, history length, enquiries and accounts. |
| 3 | **EMI Calculator** | Live sliders for amount, rate and tenure. Shows monthly EMI, total interest and total payable. |
| 4 | **AI Financial Tips** | Free-text questions answered by Claude, plus automatic tips after each eligibility check and credit analysis. |

## 6. Methodology and Formulas

**EMI formula**

`EMI = P × r × (1 + r)^n / ((1 + r)^n − 1)`

where P = principal, r = monthly rate (annual rate / 12 / 100), n = number of months.

**Maximum loan** (reverse of EMI): `P = EMI × ((1 + r)^n − 1) / (r × (1 + r)^n)`

**Eligibility rules**
- Age between 21 and 60, and not unemployed
- Credit score of 650 or more
- Total EMIs must stay within **50% of monthly income** (FOIR rule)

**Interest rate by credit score**

| Credit score | Estimated rate |
|---|---|
| 750 and above | 9.5% |
| 700 to 749 | 11% |
| 650 to 699 | 13% |
| Below 650 | 16% |

**Credit score weights:** payment history 35%, utilization 30%, history length 15%, enquiries 10%, account mix 10%.

## 7. Implementation Highlights
- **Frontend:** single-page layout with tabs, glass cards, animated background and smooth transitions; responsive for desktop and mobile
- **Validation:** regex for names, range checks for age, score, percentages and amounts
- **Backend:** `server.js` exposes `/api/ai` and `/api/records`
- **Storage:** `Code.gs` runs as a Google Apps Script web app and appends rows to a Sheet
- **Security:** secrets live in `.env` (git-ignored); the Sheet endpoint requires a shared secret; output is HTML-escaped to prevent XSS

## 8. Testing

| Test | Input | Expected | Result |
|---|---|---|---|
| EMI calculation | ₹5,00,000, 10.5%, 5 years | about ₹10,748 per month | Pass |
| Age validation | Age 17 | Error shown | Pass |
| Score validation | Credit score 1000 | Error shown | Pass |
| Empty form | No inputs | Error shown | Pass |
| Low score | Score 600 | Not eligible | Pass |
| Unemployed | Employment: Unemployed | Not eligible | Pass |
| Real-time EMI | Move sliders | Values update instantly | Pass |
| AI tips | Question submitted | Claude response shown | Needs API key |
| Sheets storage | Run an eligibility check | New row in Sheet | Needs Sheet setup |

## 9. Results
The platform delivers instant eligibility decisions, EMI figures and credit insights, then adds plain-language AI guidance. Every eligibility check is saved and shown in the "Recent checks" table.

## 10. Limitations
- The eligibility and credit score logic is a simplified model, not a real bank or credit-bureau algorithm
- Results are estimates only and are not financial advice
- No user login; the Sheet stores all checks together
- AI answers depend on the Anthropic API key and account credit

## 11. Future Scope
- User accounts and login
- Charts and amortization schedule for EMI
- Real credit bureau integration
- Multiple loan types (home, car, education) with different rules
- Multi-language support and PDF download of results

## 12. Conclusion
The project shows how simple web technologies and AI can make financial decisions easier. It meets the stated objectives: four working modules, validated forms, a modern responsive interface, Claude AI integration and persistent storage in Google Sheets.

## 13. References
- Anthropic API documentation: https://docs.claude.com
- Google Apps Script documentation: https://developers.google.com/apps-script
- Express.js: https://expressjs.com
- MDN Web Docs: https://developer.mozilla.org

---

<div align="center">Made as a college project · Estimates only, not financial advice</div>
