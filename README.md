# 🌿 Digital Green Evaluation Platform (DGEP)

**How green is your business? Now there's a number for that.**

DGEP is Pakistan's first environmental scoring platform built specifically for retail and culinary SMEs. Answer a structured survey, get an instant **Green Score (0–100)** — computed through an AHP-weighted, research-validated framework grounded in international sustainability standards and Pakistani environmental regulation.

**🔗 Live Platform:** [dgep-taffy-8fdb7b.netlify.app](https://dgep-taffy-8fdb7b.netlify.app)

---

## 🎯 The Problem

Pakistan's State Bank requires commercial banks to assess **environmental risk** in lending decisions (Green Banking Guidelines, 2017). The SECP publishes ESG disclosure guidelines. NEQS sets legally binding environmental limits.

But here's the gap: **large firms publish glossy sustainability reports — SMEs publish nothing.** Not because they don't care, but because no accessible, sector-calibrated assessment tool exists for them. Banks can't measure what firms can't report. Green finance stays locked out of the SME economy.

DGEP closes that gap with a free, browser-based assessment any registered business can complete in minutes.

---

## ⚡ What It Does

| For Firms | For Researchers & Banks |
|---|---|
| 📋 Complete a guided environmental survey (8 dimensions, 30+ questions) | 📊 Password-protected admin dashboard with live analytics |
| 🎯 Instant Green Score (0–100) with performance band | 📈 Band distribution, sector means, per-firm dimension breakdowns |
| 📉 Dimension-by-dimension breakdown showing exactly where to improve | ☁️ All responses auto-saved to Google Sheets in real time |
| 🔍 Transparent AHP weights displayed on every result | 🔄 Cross-device sync — see every submission from anywhere |

---

## 🧮 The Science Behind the Score

The Green Score isn't a vibe — it's a weighted composite across **six primary dimensions**, with weights derived through the **Analytic Hierarchy Process** (Saaty, 1980):

| Dimension | Weight | Grounding |
|---|---|---|
| ♻️ Waste & Food Waste | **28.71%** | GRI 306 + GRASS Framework |
| ✅ Compliance & Governance | **28.71%** | GRI 307 + SECP + NEQS |
| ⚡ Energy Management | **16.98%** | GRI 302 |
| 💧 Water Management | **9.82%** | GRI 303 + NEQS effluent standards |
| 🌫️ Emissions & Carbon | **9.82%** | GRI 305 + IFRS S2 |
| 🛒 Sustainable Procurement | **5.94%** | GRI 308 + GRASS |

**Consistency Ratio: 0.0066** — well within Saaty's 0.10 threshold, confirming internally coherent expert judgments.

Two supplementary dimensions (🧪 Chemical Use, 👥 Customer Engagement) are tracked separately, and every variable is calibrated to the Pakistani operational reality — load-shedding generators, WAPDA billing tiers, EPA NOC requirements, open-drain discharge risks.

### Performance Bands

```
🏆 Leading Green   76–100   Best-in-class, formal EMS, measurable outcomes
🌱 Established     51–75    Systematic management, documented practices
🌾 Developing      26–50    Basic practices, no systematic tracking
🌰 Emerging         0–25    Minimal environmental management
```

---

## 📊 Pilot Findings (N = 20 verified firms, Rawalpindi/Islamabad)

- **Mean Green Score: 52.76** (range 31.2 → 79.5, SD 11.97)
- **1 firm** achieved Leading Green · **9** Established · **10** Developing · **0** Emerging
- ⚠️ **Only 35% of firms hold a valid EPA license** — the single most actionable compliance finding for green banking
- 💚 **85% of respondents** expressed interest in using the platform — including one firm planning to use its score for an **SBP green financing application**

---

## 🏗️ Architecture

```
┌─────────────────┐     POST (no-cors)     ┌──────────────────┐
│  React 18 SPA   │ ─────────────────────► │ Google Apps      │
│  (single HTML,  │                        │ Script Web App   │
│  Netlify-hosted)│                        └────────┬─────────┘
└────────┬────────┘                                 │ openById()
         │ localStorage                             ▼
         │ (instant save)                  ┌──────────────────┐
         ▼                                 │  Google Sheets   │
┌─────────────────┐     CSV fetch (gviz)   │ "DGEP            │
│ Admin Dashboard │ ◄──────────────────────│  Submissions"    │
│ (password-gated)│                        └──────────────────┘
└─────────────────┘
```

**Zero servers. Zero build tools. Zero cost.** One HTML file + one Apps Script = a fully functional research data platform.

- **Frontend:** Single-file React 18 app (CDN-loaded, no bundler)
- **Storage:** localStorage (instant) + Google Sheets (permanent, shared)
- **Sync:** Multi-URL fallback CSV fetch via Google's gviz endpoint — CORS-safe, no publishing required
- **Auth:** Password-gated admin dashboard, survey stays public
- **Anti-gaming:** Scoring values hidden from survey options to prevent anchoring bias

---

## 🚀 Deploy Your Own

1. **Google Sheet** — create one, set sharing to *"Anyone with the link — Viewer"*, copy the Sheet ID from its URL
2. **Apps Script** — paste `dgep_apps_script.js` at [script.google.com](https://script.google.com), set your `SHEET_ID`, deploy as Web App (*Execute as: Me · Access: Anyone*), copy the deployment URL
3. **Platform** — open `index.html`, set `API` (your Apps Script URL) and `SHEET_ID`/`CSV_URL` in the config block at the top
4. **Ship it** — drag `index.html` onto [netlify.com/drop](https://app.netlify.com/drop). Done. 🎉

> ⚠️ **Gotcha that will save you an hour:** after editing Apps Script code, you must **Deploy → Manage deployments → ✏️ → New version → Deploy**. Saving alone does *not* update the live URL.

---

## 📁 Repository Contents

| File | What it is |
|---|---|
| `index.html` | The complete platform — survey, scoring engine, results, admin dashboard |
| `dgep_apps_script.js` | Google Apps Script backend — receives submissions, writes formatted rows |
| `test_apps_script.html` | Standalone diagnostic tool for testing the backend connection |
| `DGEP_Dynamic_Analytical_Workbook_v3_Final.xlsx` | Live-formula Excel workbook — full scoring chain, AHP calculation, 60-firm capacity |
| `BRP_Final_Report_DGEP.docx` | Complete research report — methodology, framework, findings, validation |

---

## 🎓 Academic Context

Developed as a **Business Research Project** at **NUST Business School**, National University of Sciences & Technology, Islamabad, under the supervision of **Dr. Romana Bangash**.

**Research Team:** Asif Sabir · Syed M. Shozeb Naqvi · Aleeza Amna · Muhammad Inaam

Built on Design Science Research methodology (Hevner et al., 2004). Framework grounded in GRI 300-Series standards, the GRASS Framework (Maynard et al., 2021), SBP Green Banking Guidelines, SECP ESG Guidelines, and Pakistan's NEQS.

---

## 📜 Citation

```
Sabir, A., Naqvi, S. M. S., Amna, A., & Inaam, M. (2026).
Digital Green Evaluation Platform: An AHP-Weighted Environmental Scoring
Framework for Retail and Culinary SMEs in Pakistan.
Business Research Project, NUST Business School, Islamabad.
```

---

<p align="center">
🌿 <em>Making environmental performance measurable — one SME at a time.</em> 🌿
</p>
