# AI Resume Analyzer — Candidate Evaluation Report

## 🚧 Project Status: UI/Design Only — Live AI Analysis NOT Working Yet

**This is currently a frontend/design showcase, not a fully functional tool.** The interface, resume upload (PDF/DOCX), and layout all work — but clicking **"Submit for Review"** will fail right now because the AI backend has not been deployed and connected yet.

A backend (`/backend` folder in this repo) exists to fix this, but as of now it has **not been deployed**, so there is no live server for the frontend to talk to. Until that's done:
- ✅ UI, styling, and file upload work fully
- ❌ "Submit for Review" will show an error — this is expected, not a bug
- 📌 See `backend/README.md` for the deployment steps needed to make analysis work end-to-end

---

A single-file HTML tool that reviews a resume against a job description the way a recruiting panel would — scoring skills, certifications, internships, projects, CGPA/eligibility, and achievements, then returning a verdict (Strong / Moderate / Weak Match) with evidence and a recommendation.

Styled as a formal black-and-white "case file" — Times New Roman throughout, a stamped verdict, and a scored breakdown by category.

## ⚠️ A Note on How This Was Built

Full transparency: this is a **prompt-engineered project**, not hand-written line by line. I designed the concept, the UI direction (black & white, Times New Roman, recruiter-dossier aesthetic), the evaluation categories, and the JSON schema for the AI output — then used **Claude (Anthropic)** to generate and iterate on the actual HTML/CSS/JS through a series of prompts, including debugging a JSON-parsing bug and adding PDF/DOCX upload support.

I'm sharing it as-is rather than passing it off as something it isn't. If you're evaluating this for a portfolio, treat it as a demonstration of **product thinking + AI-assisted development**, not raw coding-from-scratch — that distinction matters, and I'd rather be upfront about it than have someone assume otherwise from a code review.

## Features

- **Two-panel intake** — paste a job description (Exhibit A) and a resume (Exhibit B)
- **Resume upload** — accepts `.pdf` and `.docx` files directly (parsed client-side with pdf.js and mammoth.js), or plain paste
- **AI-scored evaluation** across six categories: Skills, Certifications, Internships & Experience, Projects, Eligibility & CGPA, Achievements
- **Verdict stamp** (Strong / Moderate / Weak Match) plus an overall fit score
- **Strengths, gaps, and a recommendation** — written the way a hiring panel would phrase it
- Handles truncated/malformed AI responses gracefully instead of crashing

## Tech Stack

- Vanilla HTML, CSS, JavaScript — no build step, no framework
- [pdf.js](https://mozilla.github.io/pdf.js/) for PDF text extraction
- [mammoth.js](https://github.com/mwilliamson/mammoth.js) for DOCX text extraction
- Anthropic Claude API for the actual evaluation/reasoning

## Running It

This tool calls a backend (`/backend`) at `/analyze`, which holds the Anthropic API key server-side and forwards requests to Claude. The frontend never talks to Anthropic directly, so no key is exposed in the browser.

**Right now that backend is not deployed**, so `BACKEND_URL` in `index.html` is still a placeholder and the live GitHub Pages link cannot run real analysis yet.

To make it work end-to-end:
1. Get an Anthropic API key from [console.anthropic.com](https://console.anthropic.com)
2. Deploy the `/backend` folder (e.g. on Render — free tier works) — full steps in `backend/README.md`
3. Paste the deployed backend URL into `BACKEND_URL` near the top of `index.html`
4. Push the change — GitHub Pages rebuilds automatically

## Disclaimer

Not affiliated with Anthropic beyond using their public API. Evaluation output is AI-generated and meant as a self-check/practice tool, not a substitute for actual recruiter feedback.
