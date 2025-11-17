![image alt](https://github.com/abimoussagnes/ai-agent-for-cybersecurity/blob/main/workflow.png?raw=true)

 
 # 🛡️ AI Agent for Cybersecurity
A fully automated AI-powered cybersecurity threat analysis system built with n8n, combining threat-intelligence APIs and multiple LLMs to enrich, classify, and report on security events. Designed for SOC analysts, students, blue teams, and automation enthusiasts.

## 🧭 Overview
This project automates the cybersecurity alert analysis process by orchestrating log ingestion, enrichment, threat scoring, AI-driven classification, and report generation. It integrates:


Threat-intelligence APIs (AbuseIPDB, VirusTotal, IPinfo, Shodan, etc.)


Multiple LLMs for threat reasoning (OpenAI, Groq, DeepSeek)


A consensus engine combining several AI outputs


Automated HTML + CSV reporting


Originally created for the 42 Beirut x Technologia Hackathon, this system now serves as a scalable foundation for automated SOC pipelines.

## 🚀 Key Features


CSV Log Ingestion – accepts logs from any SIEM, firewall, proxy, or manual upload


Threat-Intel Enrichment – IP reputation, geolocation, ASN, ISP, malware indicators


Multi-Model AI Analysis – runs each event through several LLMs


Consensus Classification – merges AI outputs for unbiased, reliable decisions


Detailed Reports – human-readable HTML + machine-friendly CSV


Fully Automated n8n Workflow – included in this repository



## 🏗️ Architecture
### 1. Ingestion Layer
Reads and normalizes CSV logs.
### 2. Enrichment Layer
Uses several data sources to collect:


Reputation score


Abuse reports


Geolocation and ASN


Malware checks


Exposure and service details


### 3. AI Analysis Layer
Each LLM predicts:


Malicious vs. benign


Threat category


Severity


Full reasoning


### 4. Consensus Engine
Aggregates all AI outputs via majority voting and weighted scoring.
### 5. Reporting Layer
Produces:


A full HTML report


An enriched CSV dataset

## ⚡ Quick Start


Clone the repository
git clone [https://github.com/abimoussagnes/ai-agent-for-cybersecurity.git](https://github.com/abimoussagnes/ai-agent-for-cybersecurity.git)
cd ai-agent-for-cybersecurity


Import the workflow into n8n


Open n8n


Go to Workflows → Import


Select workflow.json




Configure environment variables
(See the Configuration section below.)


Upload a CSV log file
Or connect the workflow to your log source.


Run the workflow
Manually, by schedule, or via webhook.



## 🔧 Installation
### Requirements


n8n 1.x or later


Node.js 18+ (for local installations)


Docker (optional)


API keys for threat intelligence and LLMs


### Install n8n locally
npm install -g n8n
n8n start
### Run n8n using Docker
docker run -it --rm -p 5678:5678 n8nio/n8n

## 🔑 Configuration
Create a .env file or configure environment variables directly inside n8n.



Variable
Description




OPENAI_API_KEY
OpenAI models for threat reasoning


GROQ_API_KEY
Groq models for secondary analysis


DEEPSEEK_API_KEY
Optional additional AI engine


ABUSEIPDB_API_KEY
Reputation + abuse reports


VIRUSTOTAL_API_KEY
Malware / IP / URL checks


IPINFO_TOKEN
Geolocation + ASN


SHODAN_API_KEY
Exposure lookup (optional)


N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS
Usually set to false




## 🖥️ Usage
### 1. Prepare your CSV file
Expected fields typically include:
source_ip, timestamp, destination, port, event_type, raw_message
### 2. Trigger the workflow


Upload your CSV manually


Or fetch logs automatically


Or trigger via webhook


### 3. Automated processing
n8n will perform:


Enrichment


Multi-LLM analysis


Consensus reasoning


Report generation


### 4. Retrieve results
Generated output files include:


analysis.csv


final-report.html



## 📄 Output Reports
### HTML Report Includes


Summary of malicious events


AI reasoning from each LLM


Confidence levels


IP metadata and threat enrichment


IOC highlights


### CSV Report Includes


Parsed log data


Every enrichment field


Each LLM’s classification


Final consensus verdict


## 🤝 Contributing
Contributions are welcome!


Fork this repository


Create a feature branch
git checkout -b feature/my-feature


Commit changes


Open a pull request


Please keep style consistent and include clear descriptions of changes.


## 📬 Contact
GitHub: [https://github.com/abimoussagnes](https://github.com/abimoussagnes)
Email: agnes.abimoussa@hotmail.com
