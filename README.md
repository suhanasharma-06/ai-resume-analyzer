# AI Resume Analyzer — Candidate Evaluation Report

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

This project calls the Anthropic API directly from the browser. That only works out of the box inside a Claude.ai artifact, where the API key is handled for you — if you open `resume-analyzer.html` standalone or host it elsewhere, the API call will fail because there's no key configured (and a browser can't safely hold one anyway).

To make this a real standalone/deployable app:
1. Add a small backend (Node/Express or Python/Flask) with one `/analyze` route
2. Store your Anthropic API key server-side (e.g. in a `.env` file, **never committed to Git**)
3. Have the frontend call your backend instead of `api.anthropic.com` directly

## Disclaimer

Not affiliated with Anthropic beyond using their public API. Evaluation output is AI-generated and meant as a self-check/practice tool, not a substitute for actual recruiter feedback.
