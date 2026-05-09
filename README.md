# COVID-19 Anomaly Detection AI Agent

An autonomous AI agent that detects, classifies, and responds to anomalies in live COVID-19 time-series data using statistical methods and a GroqCloud LLM.

---

## Overview

This project fetches real-time COVID-19 case data, identifies statistical anomalies, assigns severity levels, and uses an LLM-powered agent (via GroqCloud) to autonomously decide the appropriate action for each anomaly.

---

## Pipeline

```
Fetch Live Data → Detect Anomalies → Classify Severity → AI Agent Decision → Visualize
```

| Step | Description |
|------|-------------|
| 1️.Data Ingestion | Fetches daily case data from the [disease.sh](https://disease.sh) API |
| 2. Anomaly Detection | Flags outliers using **Z-score** (>3σ) and **day-over-day growth rate** (>40%) |
| 3. Severity Classification | Labels each anomaly as `CRITICAL`, `WARNING`, or `MINOR` using a 7-day rolling baseline |
| 4. AI Agent Decision | LLM (Llama3 via Groq) decides: `FIX_ANOMALY`, `KEEP_ANOMALY`, or `FLAG_FOR_REVIEW` |
| 5. Visualization | Plots the time-series with annotated anomalies and decisions |

---

## ⚙️ Configuration

```python
COUNTRY        = 'India'   # Any country supported by disease.sh
DAYS           = 90        # Historical days to analyze
ROLLING_WINDOW = 7         # Baseline window (days)
MIN_ABS_INCREASE = 500     # Minimum case increase to flag
```

---

##  Getting Started

### 1. Clone the repo
```bash
git clone https://github.com/your-username/covid19-anomaly-detection-agent.git
cd covid19-anomaly-detection-agent
```

### 2. Install dependencies
```bash
pip install phidata groq python-dotenv tabulate requests numpy pandas matplotlib
```

### 3. Set your GroqCloud API Key

In **Google Colab**, add your key to Colab Secrets as `GROQ_API_KEY`.  
Locally, create a `.env` file:
```
GROQ_API_KEY=your_key_here
```
Get a free key at [console.groq.com](https://console.groq.com).

### 4. Run the notebook
Open `COVID19_Anomaly_Detection_Agent.ipynb` in Jupyter or Google Colab and run all cells.

---

## Agent Decisions

| Decision | Meaning |
|----------|---------|
| `FIX_ANOMALY` | Likely reporting noise — auto-corrected using 3-day rolling mean |
| `KEEP_ANOMALY` | Real outbreak signal — preserved as-is |
| `FLAG_FOR_REVIEW` | Critical or ambiguous — escalated for human review |

---

## Tech Stack

- **Python** — pandas, numpy, matplotlib
- **disease.sh API** — live COVID-19 data
- **GroqCloud** — fast LLM inference (Llama3-8b)
- **Google Colab** — recommended runtime

---

##  Project Structure

```
├── COVID19_Anomaly_Detection_Agent.ipynb   # Main notebook
├── README.md
└── .env.example                            # API key template
```

---

##  License

MIT License — free to use and modify.
