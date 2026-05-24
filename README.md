# TrendOps

**AI-Powered YouTube Trend Intelligence & Market Analysis Platform**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python 3.11+](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115+-green.svg)](https://fastapi.tiangolo.com/)
[![Gemini](https://img.shields.io/badge/AI-Google%20Gemini-orange.svg)](https://aistudio.google.com/)
[![UOE Summer of Code 2026](https://img.shields.io/badge/Hackathon-UOE%20Summer%20of%20Code%202026-purple.svg)](#built-for-uoe-summer-of-code-2026)

> TrendOps is an AI-powered trend intelligence platform that analyzes live YouTube trending data using NLP, clustering algorithms, and LLM-driven synthesis to generate actionable business insights, startup opportunities, audience intelligence, and emerging digital trend reports.

---

## Problem Statement

Trend research is broken for modern creators, brands, and investors:

- **Manual & Slow:** Scrolling trending pages provides no semantic depth or pattern analysis
- **Shallow Metrics:** Existing tools report view counts, not what the data *means*
- **Missed Opportunities:** Subculture spikes and niche market surges are invisible to traditional analytics
- **No Strategic Layer:** Raw data does not translate into content strategy or business insight

---

## Solution Overview

TrendOps automates the entire trend intelligence lifecycle:

1. **Ingest** live YouTube trending data via YouTube Data API v3
2. **Score** videos by normalized engagement metrics
3. **Extract** semantically meaningful keywords via TF-IDF
4. **Cluster** videos into thematic groups using K-Means
5. **Synthesize** executive insights, startup opportunities, and content strategies via Google Gemini
6. **Deliver** structured reports via REST API and an interactive web dashboard

---

## Key Features

| Feature | Description |
|---|---|
| Real-Time Ingestion | Fetches fresh trending data across regions and categories |
| NLP Keyword Extraction | TF-IDF over video titles and descriptions |
| Semantic Clustering | K-Means grouping to surface latent content themes |
| AI Insight Synthesis | Gemini-powered executive summaries and business briefs |
| Regional Intelligence | Switch between markets (US, IN, GB, CA, DE, JP, etc.) |
| Startup Opportunities | Auto-identified commercial gaps from viral waves |
| Content Strategy Blueprints | AI-generated hooks, angles, and format recommendations |
| Interactive Dashboard | Dark-mode, responsive analytics UI |
| Execution Tracing | Full observability into pipeline steps and API costs |

---

## Architecture Overview

```
+-----------------------------------------------------+
|              Interactive Web Dashboard              |
|          (Landing Page + Analytics UI)              |
+---------------------+-------------------------------+
                      |  HTTP / REST
                      v
+-----------------------------------------------------+
|                 FastAPI Backend                     |
|           Routing, Validation, Orchestration        |
+------+----------+-------------+--------------------+
       |          |             |
       v          v             v
+----------+  +----------+  +--------------------+
|Governance|  |  Data    |  |  Analytics Agent   |
|  Agent   |  |  Agent   |  |(TF-IDF + K-Means)  |
+----------+  +----+-----+  +----------+---------+
                   |                   |
                   +--------+----------+
                            v
               +-------------------------+
               |   Intelligence Agent    |
               |  (Google Gemini API)    |
               +-------------------------+
```

---

## AI/ML Pipeline

```
YouTube Trending Data
        |
        v
[Engagement Scoring]   <- Views, Likes, Comments normalized
        |
        v
[TF-IDF Vectorization] <- Extract keyword weights from titles/descriptions
        |
        v
[K-Means Clustering]   <- Group videos into N semantic theme clusters
        |
        v
[Gemini LLM Synthesis] <- Generate executive summaries, startup ideas,
                          content strategies, and market briefs
        |
        v
Structured JSON Report + Dashboard
```

### Why This Stack?

- **TF-IDF** captures domain-relevant terminology without requiring labeled training data
- **K-Means** provides deterministic, interpretable theme clusters at low compute cost
- **Gemini Flash** delivers fast, cost-efficient LLM inference for strategic synthesis
- Combined, these create a lightweight yet powerful unsupervised NLP pipeline

---

## Multi-Agent System

TrendOps decomposes the analytics lifecycle into four independent agents:

| Agent | Role | Output |
|---|---|---|
| **Governance Agent** | Validates input params (region, category, rate limits) | Sanitized params, audit trace |
| **Data Agent** | Fetches raw video metadata from YouTube API v3 | Structured video list |
| **Analytics Agent** | Runs TF-IDF + K-Means, scores engagement | Themes, clusters, scores |
| **Intelligence Agent** | Calls Gemini to generate strategic insight reports | Executive summary, opportunities |

Each agent is independently testable and replaceable, enabling modular, scalable, and maintainable architecture.

---

## Tech Stack

**Backend**
- Python 3.11+
- FastAPI + Uvicorn (async REST API)
- Pydantic v2 (data validation)
- python-dotenv (config management)

**AI / ML**
- Google Gemini API (gemini-flash-latest)
- TF-IDF vectorization (custom NumPy implementation)
- K-Means clustering (custom NumPy implementation)
- Engagement scoring pipeline

**Data Sources**
- YouTube Data API v3 (trending videos endpoint)

**Frontend**
- Jinja2 templating (server-side rendered)
- Vanilla HTML5 / CSS3 (dark mode, glassmorphism)
- Responsive dashboard UI

**Infrastructure**
- Docker (containerization)
- Nginx (reverse proxy)
- EC2 / Vercel (deployment targets)

---

## Folder Structure

```
TrendOps/
+-- app/
|   +-- agents/
|   |   +-- governance_agent.py    # Input validation & policy enforcement
|   |   +-- data_agent.py          # YouTube API data fetching
|   |   +-- analytics_agent.py     # TF-IDF + K-Means analytics pipeline
|   |   +-- intelligence_agent.py  # Gemini LLM insight synthesis
|   +-- tools/
|   |   +-- youtube_tool.py        # YouTube API wrapper
|   |   +-- clustering_tool.py     # K-Means clustering engine
|   |   +-- scoring_tool.py        # Engagement scoring
|   +-- utils/
|   |   +-- config.py              # Environment & app configuration
|   |   +-- logging.py             # Structured JSON logging
|   |   +-- cost_tracker.py        # LLM token & cost tracking
|   +-- main.py                    # FastAPI app entrypoint
+-- templates/
|   +-- landing.html               # Marketing landing page
|   +-- dashboard.html             # Analytics dashboard UI
+-- docs/                          # Additional documentation
+-- .env.example                   # Environment variable template
+-- requirements.txt               # Python dependencies
+-- Dockerfile                     # Container build config
+-- vercel.json                    # Vercel deployment config
+-- README.md
```

---

## Local Setup Guide

### Prerequisites

- **Python 3.11 or higher** - [Download here](https://www.python.org/downloads/)
- A **Google Cloud** account for YouTube API access
- A **Google AI Studio** account for Gemini API access

---

### Step 1 - Clone the Repository

```bash
git clone https://github.com/<your-username>/TrendOps.git
cd TrendOps
```

---

### Step 2 - Create a Virtual Environment

**Windows (PowerShell):**
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

**macOS / Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

---

### Step 3 - Install Dependencies

```bash
pip install -r requirements.txt
```

---

### Step 4 - Configure Environment Variables

Copy the example env file:

```bash
# Windows
copy .env.example .env

# macOS / Linux
cp .env.example .env
```

Open `.env` and fill in your credentials:

```env
# YouTube Data API v3 Key
# Get from: https://console.cloud.google.com/apis/credentials
YOUTUBE_API_KEY=your_youtube_api_key_here

# Google Gemini API Key
# Get from: https://aistudio.google.com/app/apikey
GOOGLE_API_KEY=your_google_api_key_here
```

#### How to Get Your API Keys

**YouTube Data API v3:**
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project (or select existing)
3. Navigate to **APIs & Services > Library**
4. Search and enable **YouTube Data API v3**
5. Go to **Credentials > Create Credentials > API Key**

**Google Gemini API:**
1. Go to [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Click **Create API Key**
3. Copy and paste into your `.env` file

---

### Step 5 - Run the Backend

```bash
# Using the module entrypoint (recommended):
python -m app.main

# Or directly with uvicorn:
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

The server starts at **http://localhost:8000**

---

### Step 6 - Open the Application

| Page | URL |
|---|---|
| Landing Page | http://localhost:8000 |
| Analytics Dashboard | http://localhost:8000/dashboard |
| Health Check | http://localhost:8000/health |
| API Docs (Swagger) | http://localhost:8000/docs |

---

## API Endpoints

### POST /analyze - Run Trend Analysis

**Request:**
```json
{
  "region_code": "US",
  "category_id": "10",
  "max_results": 25,
  "include_intelligence": true
}
```

**Supported Regions:** `US`, `IN`, `GB`, `CA`, `AU`, `DE`, `FR`, `JP`, `KR`, `BR`

**Supported Categories:**

| ID | Category |
|---|---|
| 10 | Music |
| 20 | Gaming |
| 24 | Entertainment |
| 25 | News & Politics |
| 28 | Science & Technology |
| 27 | Education |

**Response:**
```json
{
  "status": "success",
  "data": {
    "region_code": "US",
    "video_count": 25,
    "videos": []
  },
  "analytics": {
    "themes": [
      {
        "theme_id": 0,
        "keywords": ["music", "official", "video"],
        "video_count": 8,
        "engagement_score": 85.5,
        "top_videos": []
      }
    ],
    "total_themes": 3
  },
  "intelligence": {
    "executive_summary": "Music video launches dominate trending...",
    "emerging_patterns": [],
    "startup_opportunities": [],
    "content_strategies": []
  },
  "governance": {
    "request_id": "uuid",
    "execution_time_ms": 1240,
    "steps": []
  }
}
```

### GET /health - Health Check
### GET /config/regions - Valid Regions
### GET /config/categories - Valid Categories
### GET /governance/trace - Execution Trace

---

## Deployment Architecture

### Docker

```bash
docker build -t trendops .
docker run -p 8000:8000 --env-file .env trendops
```

### EC2 Production Deployment

```bash
# SSH into your EC2 instance and clone the repo
git clone https://github.com/<username>/TrendOps.git
cd TrendOps && cp .env.example .env

# Set up venv and install
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt

# Run as a systemd service
sudo systemctl enable trendops
sudo systemctl start trendops
```

**Nginx reverse proxy config:**
```nginx
server {
    listen 80;
    server_name your-domain.com;
    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### Vercel Deployment

Connect your GitHub repo to Vercel and set `YOUTUBE_API_KEY` and `GOOGLE_API_KEY` in the Vercel Dashboard. The `vercel.json` is pre-configured.

---

## Future Scope

- **Multi-Platform Expansion** - TikTok, Instagram Reels, Twitter/X cross-platform trend mapping
- **Temporal Tracking** - Time-series analysis of how clusters grow and decay over time
- **Custom Alert System** - Automated email/Slack notifications on trend spike detection
- **Fine-Tuned Models** - Domain-specific embeddings for improved clustering accuracy
- **Export Engine** - One-click PDF/PowerPoint report generation for stakeholders
- **User Authentication** - Multi-tenant SaaS with saved analyses and history

---

## Screenshots

Run locally and visit the URLs below to explore the UI:

| Page | URL |
|---|---|
| Landing Page | http://localhost:8000 |
| Analytics Dashboard | http://localhost:8000/dashboard |

---

## Built for UOE Summer of Code 2026

TrendOps was developed as a submission to the **UOE Summer of Code 2026** hackathon under the **AI & Machine Learning** and **Startup & Productivity Solutions** tracks.

**What makes it hackathon-ready:**
- Real-world problem with measurable impact for creators, brands, and investors
- Clean AI/ML pipeline (TF-IDF + K-Means + LLM synthesis)
- Modular, scalable multi-agent architecture
- Production-grade code with observability and error handling
- Beginner-friendly local setup with copy-paste commands
- Interactive web UI for immediate demo-ability

---

## Contributors

**Anish Maheshwari**
[![LinkedIn](https://img.shields.io/badge/LinkedIn-anish--maheshwarii-blue?logo=linkedin)](https://www.linkedin.com/in/anish-maheshwarii)

---

## License

Distributed under the MIT License. See `LICENSE` for details.
