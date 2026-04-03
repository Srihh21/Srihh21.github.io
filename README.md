# Srihitha Reddy Betelly — Portfolio Website

[![Live Site](https://img.shields.io/badge/Live%20Site-srihh21.github.io-00d4c8?style=flat-square&logo=github)](https://srihh21.github.io)
[![HTML](https://img.shields.io/badge/Built%20With-HTML%2FCSS%2FJS-0099ff?style=flat-square)](https://github.com/Srihh21/Srihh21.github.io)

Personal portfolio website for **Srihitha Reddy Betelly**, Senior Data Engineer based in Chicago, IL. Built as a single-page static site hosted on GitHub Pages.

---

## Live URL

**[https://srihh21.github.io](https://srihh21.github.io)**

---

## About

This site highlights Srihitha's background, expertise, and open-source projects as a Senior Data Engineer with 5+ years of experience building large-scale data pipelines across healthcare and financial services. The portfolio is designed to be fast, fully responsive, and easy to maintain.

---

## Sections

| Section | Description |
|---|---|
| **Hero / About** | Introduction, key stats, and call-to-action |
| **Impact** | Quantified performance achievements from professional experience |
| **Experience** | Timeline of roles at ZS, Fidelity Investments, and Optum |
| **Projects** | Featured open-source data engineering projects with architecture details |
| **Skills** | Full tech stack organized by category |
| **Education** | UMass Dartmouth (MS) and JNTU Hyderabad (BE) |
| **Contact** | Email, LinkedIn, and phone |

---

## Featured Projects

### [Real-Time Fraud Detection System](https://github.com/Srihh21/fraud-detection-system)
End-to-end streaming pipeline using Kafka, Spark Structured Streaming, scikit-learn, MinIO/S3, Snowflake, and Streamlit. Processes live card transactions through an ML model and surfaces fraud alerts on a real-time dashboard.

### [Video Streaming Pipeline](https://github.com/Srihh21/video-streaming-pipeline)
Large-scale data pipeline for ingesting and processing video streaming event data — currently in active development.

---

## Tech Stack

The site is a single `index.html` file with no external dependencies beyond Google Fonts. No frameworks, no build step.

- **HTML5 / CSS3** — semantic markup, CSS custom properties, grid & flexbox layout
- **Vanilla JavaScript** — Intersection Observer API for scroll animations, active nav highlighting
- **Google Fonts** — Inter (body) + JetBrains Mono (code accents)
- **Hosting** — GitHub Pages (served from `main` branch root)

---

## Local Development

No build tooling required. Just open the file:

```bash
# Clone the repo
git clone https://github.com/Srihh21/Srihh21.github.io.git
cd Srihh21.github.io

# Open in browser
open index.html
# or on Linux:
xdg-open index.html
```

---

## Updating the Site

1. Edit `index.html` locally.
2. Commit and push to the `main` branch:

```bash
git add index.html
git commit -m "Update portfolio content"
git push origin main
```

GitHub Pages automatically rebuilds and deploys within ~1 minute.

---

## Design

- **Color scheme:** Dark navy background (`#0a0e1a`) with teal/cyan accent (`#00d4c8`) and blue gradient (`#0099ff`)
- **Typography:** Inter for body text, JetBrains Mono for code and numeric labels
- **Animations:** Fade-in on scroll via Intersection Observer (no external animation library)
- **Responsive:** Fully mobile-friendly with a collapsible nav on small screens

---

## Contact

- **Email:** rsrihitha248@gmail.com
- **LinkedIn:** [Srihitha Reddy](https://www.linkedin.com/in/srihitha-reddy21/)
- **Location:** Chicago, Illinois
