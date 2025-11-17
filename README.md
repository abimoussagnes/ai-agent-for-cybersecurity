# 🛡️ AI Agent for Cybersecurity

![workflow](https://github.com/abimoussagnes/ai-agent-for-cybersecurity/blob/main/workflow.png?raw=true)

A fully automated, AI‑powered cybersecurity alert analysis pipeline built with n8n. It enriches logs with threat-intel, runs multi-LLM analysis, aggregates model outputs with a consensus engine, and generates human-readable HTML and machine-friendly CSV reports.

Badges: (add CI, license, repo badges here)

Table of contents
- Overview
- Features
- Architecture
- Quick Start
- Installation
- Configuration (Environment variables)
- Usage
- Outputs
- Examples
- Contributing
- Troubleshooting
- Roadmap
- License & Contact

Overview
This project automates alert analysis by orchestrating:
- CSV log ingestion and normalization
- Threat-intel enrichment (AbuseIPDB, VirusTotal, IPinfo, Shodan, etc.)
- Multi-model AI analysis (OpenAI, Groq, DeepSeek)
- Consensus-driven classification and scoring
- Automated HTML + CSV reports
Originally built for the 42 Beirut x Technologia Hackathon; now a reusable foundation for SOC automation.

Key features
- CSV ingestion from any SIEM, firewall, proxy, or manual upload
- Enrichment: IP reputation, abuse reports, geolocation, ASN, malware indicators
- Multi-LLM reasoning and consensus classification (majority + weighted scoring)
- Output: enriched CSV + full HTML report
- Fully automated n8n workflow (workflow.json included)

Architecture (brief)
1. Ingestion: reads and normalizes CSV logs
2. Enrichment: calls multiple intel sources for metadata and reputation
3. AI Analysis: runs several LLMs to classify and explain events
4. Consensus Engine: aggregates outputs for final verdict and confidence
5. Reporting: generates analysis.csv and final-report.html

Quick Start (fastest way to try)
Clone:
git clone https://github.com/abimoussagnes/ai-agent-for-cybersecurity.git
cd ai-agent-for-cybersecurity

Option A — n8n cloud / n8n desktop
1. Open your n8n instance
2. Workflows → Import → select workflow.json
3. Configure credentials and environment variables (see below)
4. Upload a sample CSV and run

Option B — Run n8n locally
npm install -g n8n
n8n start
Import workflow.json as above.

Option C — Docker
docker run -it --rm -p 5678:5678 -v ~/.n8n:/home/node/.n8n n8nio/n8n

Installation / Requirements
- n8n 1.x or later
- Node.js 18+ (for local installations)
- Docker (optional)
- API keys for threat intelligence providers and LLMs

Configuration (environment variables)
Create a .env file or configure values inside n8n. Marked required vs optional:

| Variable | Required | Purpose | Example |
|---|---:|---|---|
| OPENAI_API_KEY | Yes | OpenAI models for threat reasoning | sk-... |
| GROQ_API_KEY | Optional | Groq models for secondary analysis | groq-... |
| DEEPSEEK_API_KEY | Optional | Additional AI engine | ds-... |
| ABUSEIPDB_API_KEY | Optional | IP reputation / abuse reports | ... |
| VIRUSTOTAL_API_KEY | Optional | Malware / IP / URL checks | ... |
| IPINFO_TOKEN | Optional | Geolocation & ASN | ... |
| SHODAN_API_KEY | Optional | Exposure lookup | ... |
| N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS | Optional | n8n setting (usually false) | false |

Security note
- Do not commit API keys or .env files to the repo.
- Use n8n credential stores, environment variables, or a secrets manager (Vault, AWS Secrets Manager).
- Limit API key scopes where possible and rotate keys periodically.

Usage: prepare a CSV
Expected fields (common minimum): source_ip, timestamp, destination, port, event_type, raw_message
Minimal example row:
source_ip,timestamp,destination,port,event_type,raw_message
203.0.113.45,2025-11-17T12:00:00Z,example.com,443,connection,failure on TLS handshake

Triggering the workflow
- Upload CSV file node in n8n and execute
- Schedule the workflow to run periodically
- Configure an incoming webhook to send logs automatically

Automated processing steps performed
- Data normalization and parsing
- Threat-intel enrichment across multiple providers
- Multi-LLM reasoning (malicious/benign, category, severity, full reasoning)
- Consensus scoring and final verdict
- Report generation (CSV + HTML)

Outputs
- analysis.csv — enriched row for every input event (includes per-LLM outputs + consensus)
- final-report.html — human-friendly report with summaries, evidence, model explanations, and IOC highlights

Examples
- Add a small samples/ folder with a sample input CSV and a sample final-report.html to help users validate the setup quickly.

Workflow JSON
- The n8n workflow definition is shipped as workflow.json at the repo root (or specify the exact path). Import this into n8n as described in Quick Start.

Contributing
- Fork -> branch (feature/name) -> push -> open PR
- Include tests or reproduction steps for bugfixes
- Keep changes atomic and well-documented
- Add yourself to CONTRIBUTORS.md if making substantial contributions

Troubleshooting (common issues)
- Missing API key errors: verify .env and n8n credential nodes
- Rate limits: many intel providers throttle requests; implement caching or reduce volume
- Unexpected LLM outputs: check prompt templates or reduce temperature in model config

Roadmap / Known limitations
- Add optional support for streaming LLM responses
- Add more threat intel connectors (Censys, AlienVault OTX)
- Improve scoring (machine learned weighted consensus)
- Add integration tests and example outputs

Contact
- GitHub: https://github.com/abimoussagnes
- Email: agnes.abimoussa@hotmail.com

Acknowledgements
- 42 Beirut x Technologia Hackathon — initial inspiration and prototype

---
