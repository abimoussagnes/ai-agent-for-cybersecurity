![image alt](https://github.com/abimoussagnes/ai-agent-for-cybersecurity/blob/main/workflow.png?raw=true)
# Automated Cybersecurity Threat Analysis System  
### Built during the **42 Beirut x Technologia Hackathon**

---

## Overview  
This repository contains a fully automated **cybersecurity threat analysis system** built using **n8n**.  
It was developed during the **42 Beirut x Technologia Hackathon** to showcase how automation and AI can significantly enhance threat detection, triage, and reporting workflows inside modern SOC environments.

The system ingests attack logs from CSV files, enriches each event with external threat-intelligence services, performs multi-model AI analysis, computes a consensus classification, assigns alert priority levels, and finally generates professional HTML and CSV reports.

---

## Project Goals  
- Automate repetitive SOC enrichment tasks  
- Minimize manual investigation effort  
- Improve threat classification accuracy  
- Use multiple AI models to avoid single-model bias  
- Deliver instant, professional-quality threat analysis reports  
- Demonstrate advanced automation with n8n in a hackathon setting  
- Integrate cybersecurity, machine learning, and data engineering concepts

---

## Key Features  

### **1. Log Ingestion**  
The workflow begins by reading attack logs from a CSV file containing fields such as:  
- Source IP  
- Destination IP  
- Attack type  
- Timestamp  

---

### **2. Automated Threat-Intel Enrichment**  
Each IP is automatically enriched using multiple intelligence APIs:

| API | Purpose |
|-----|---------|
| **AbuseIPDB** | Reputation metrics, abuse categories, confidence scores |
| **VirusTotal** | Community detections, malware relationships |
| **IPinfo** | Geolocation, ASN, ISP/organization |
| **Shodan** | Open ports, exposed services, vulnerabilities |

This provides a complete intelligence profile for each event.

---

### **3. Multi-Model AI Analysis**  
To provide deep reasoning and reduce bias, every event is evaluated by **five AI models**:

- ChatGPT  
- DeepSeek  
- Claude  
- Mistral  
- Groq (Llama)

Each AI generates its own threat analysis.

---

### **4. AI Consensus Classification Engine**  
A custom code module analyzes all AI outputs and determines:

- TRUE_POSITIVE  
- FALSE_POSITIVE  
- UNKNOWN  

It computes:  
- Model vote counts  
- Confidence levels  
- Classification consensus  
- Complete result breakdown  
- Number of models in agreement  

---

### **5. Automated Alert Prioritization**  
If **3 or more models** classify an event as a **TRUE_POSITIVE**, the workflow flags it as:


This makes threat triage faster and more consistent.

---

### **6. Professional Reporting**  

#### CSV Output  
- Machine-readable  
- SIEM-ready  
- Contains all enriched and classified data  

#### HTML Threat Intelligence Report  
- Clean and modern UI  
- Summary statistics  
- Per-event breakdown  
- Geolocation insights  
- AI model explanations  
- Highlighted high-priority alerts  

---

## Architecture Overview  

### **1. Ingestion Layer**
- Manual Trigger  
- Read/Write File  
- Extract From File  

### **2. Enrichment Layer**
- AbuseIPDB API  
- VirusTotal API  
- IPinfo API  
- Shodan API  

### **3. Consolidation Layer**
- Merge (combineAll)  
- Format Output  

### **4. AI Layer**
- ChatGPT analysis  
- DeepSeek analysis  
- Claude analysis  
- Mistral analysis  
- Groq (Llama) analysis  

### **5. Consensus Layer**
- Custom code node calculates:  
  - Consensus classification  
  - Confidence summary  
  - Alert priority  

### **6. Reporting Layer**
- CSV generation  
- HTML report generation  
- Save to disk  

---

## Achievements  
- Fully automated threat-analysis system built during the hackathon  
- Successful integration of four threat-intel APIs  
- Combined reasoning from five AI models  
- Designed a robust consensus voting system  
- Generated clean, professional HTML & CSV reports  
- Demonstrated strong synergy between automation, AI, and cybersecurity  
- Delivered a working solution addressing real SOC challenges  

---

## Credits  
This project was created by the **42 Beirut x Technologia Hackathon team**, combining expertise in automation, AI, and cybersecurity.

---

## License  
This project is available for educational and research use.  
For commercial deployment, please request permission.

---
