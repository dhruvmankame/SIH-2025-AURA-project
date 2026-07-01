# AURA - Advanced Unified Response Analyzer

<div align="center">

![AURA Banner](https://img.shields.io/badge/SIH-Grand%20Finale%202025-blue?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.10+-green?style=for-the-badge&logo=python)
![React](https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react)
![Django](https://img.shields.io/badge/Django-REST-092E20?style=for-the-badge&logo=django)

**🏆 Smart India Hackathon (SIH) 2025 - Grand Finale Project**

*Next-Gen IPDR & PCAP Forensics Platform*

</div>

---

## 🎯 Problem Statement

Traditional network security tools generate overwhelming alerts for every detected attack pattern, regardless of whether the attack was successful or blocked. Security teams waste valuable time investigating false positives and blocked attempts instead of focusing on actual breaches.

**AURA solves this by distinguishing between "Attack Attempts" and "Successful Breaches"** using Response Analysis Rules.

---

## 🚀 Features

### Core Detection Capabilities

| Threat Type | Description |
|-------------|-------------|
| 🌐 **Typosquatting** | Analyzes domain variations for phishing/spoofing risks |
| 💉 **SQL Injection** | Detects unauthorized database access attempts via URL parameters |
| ⚡ **XSS Detection** | Identifies reflected and stored cross-site scripting vectors |
| 📁 **Directory Traversal** | Flags attempts to access unauthorized file system paths |
| 💻 **Command Injection** | Identifies OS command execution payloads in vectors |
| 🔄 **SSRF** | Detects server-side request forgery attempts to internal services |
| 📂 **LFI / RFI** | Monitors for local and remote file inclusion patterns |
| 🔐 **Credential Stuffing** | Correlates high-frequency login attempts and failures |
| 🔧 **HTTP Param Pollution** | Detects duplicate parameters used to bypass WAF rules |
| 📄 **XXE Injection** | Flags XML external entity processing attempts |
| 🚪 **Web Shells** | Identifies backdoor upload attempts (jsp, php, asp) |

### Key Highlights

- **🧠 ML-Powered Detection**: BERT-based URL classification and traditional ML models
- **📊 Response Analysis**: Correlates Request + Response Size + Status Code
- **🎯 Breach Confirmation**: Distinguishes blocked attempts from successful breaches
- **🗺️ Attack Visualization**: Interactive geographic attack mapping
- **📈 Real-time Dashboard**: Live threat monitoring and statistics
- **🔍 XAI (Explainable AI)**: Provides explanations and mitigation advice for detected threats

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        AURA Architecture                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   ┌──────────────┐    ┌──────────────┐    ┌──────────────┐     │
│   │   PCAP/CSV   │───▶│    Parser    │───▶│   Analyzer   │     │
│   │    Upload    │    │  (tshark)    │    │  (ML/Regex)  │     │
│   └──────────────┘    └──────────────┘    └──────────────┘     │
│                                                   │              │
│                                                   ▼              │
│   ┌──────────────┐    ┌──────────────┐    ┌──────────────┐     │
│   │   Frontend   │◀───│  Django API  │◀───│   Response   │     │
│   │   (React)    │    │   (REST)     │    │   Analysis   │     │
│   └──────────────┘    └──────────────┘    └──────────────┘     │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

### Frontend
- **React 19** - UI Framework
- **Vite** - Build Tool
- **Tailwind CSS** - Styling
- **Framer Motion** - Animations
- **Recharts** - Data Visualization
- **Three.js / React Three Fiber** - 3D Graphics
- **Lucide React** - Icons

### Backend
- **Django** - Web Framework
- **Django REST Framework** - API
- **Pandas** - Data Processing
- **PyTorch** - ML Models (BERT)
- **tshark** - PCAP Parsing

---

## 📦 Installation

### Prerequisites

- Python 3.10+
- Node.js 18+
- Wireshark/tshark (for PCAP parsing)

### Backend Setup

```bash
# Navigate to backend directory
cd server/backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# Windows
venv\Scripts\activate
# Linux/Mac
source venv/bin/activate

# Install dependencies
pip install django djangorestframework pandas torch transformers tqdm

# Run migrations
python manage.py migrate

# Start server
python manage.py runserver
```

### Frontend Setup

```bash
# Navigate to frontend directory
cd auraa-frontend

# Install dependencies
npm install

# Start development server
npm run dev
```

---

## 🖥️ Usage

1. **Start the Backend Server**
   ```bash
   cd server/backend
   python manage.py runserver
   ```

2. **Start the Frontend**
   ```bash
   cd auraa-frontend
   npm run dev
   ```

3. **Access the Application**
   - Frontend: `http://localhost:5173`
   - API: `http://localhost:8000/api/`

4. **Upload PCAP/CSV Files**
   - Navigate to the Scan page
   - Upload your `.pcap`, `.pcapng`, or `.csv` file
   - View analysis results on the Dashboard

---

## 📊 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/upload-capture/` | POST | Upload PCAP/CSV for analysis |
| `/api/attacks/` | GET | Get detected attacks |
| `/api/stats/` | GET | Get analysis statistics |
| `/api/traffic/` | GET | Get traffic data for visualization |
| `/api/analyze_attack/` | POST | Get XAI explanation for an attack |

---

## 🔬 How It Works

### 1. Data Collection
- Accepts PCAP, PCAPNG, or CSV files
- Parses network traffic using tshark

### 2. Multi-Layer Analysis
- **Regex Patterns**: Fast pattern matching for known attack signatures
- **ML Models**: Traditional machine learning for anomaly detection
- **BERT Classification**: Deep learning for sophisticated URL analysis

### 3. Response Analysis
- Correlates HTTP status codes with attack patterns
- Analyzes response sizes for data exfiltration indicators
- Distinguishes between blocked attempts (4xx/5xx) and successful breaches (2xx with large responses)

### 4. Threat Classification
- Categorizes threats by type and severity
- Provides evidence and detection method for each alert
- Generates actionable mitigation advice

---

## 📁 Project Structure

```
sih-aura/
├── auraa-frontend/          # React Frontend
│   ├── src/
│   │   ├── components/      # UI Components
│   │   ├── pages/           # Page Components
│   │   └── lib/             # Utilities
│   └── package.json
│
├── server/backend/          # Django Backend
│   ├── api/
│   │   ├── views.py         # API Endpoints
│   │   ├── threat_analyzer.py   # Core Analysis Engine
│   │   ├── bert_predictor.py    # BERT Model Integration
│   │   ├── ml_predictor.py      # ML Model Integration
│   │   ├── xai_bert.py          # Explainable AI
│   │   └── parsers.py           # PCAP Parsing
│   └── manage.py
│
└── README.md
```

---

## 🏆 Smart India Hackathon 2025

This project was developed for the **Smart India Hackathon (SIH) 2025 Grand Finale**.

### Team RuntimeTerrors
Building next-generation cybersecurity solutions for India.

---

## 📄 License

This project is developed for educational and hackathon purposes.

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

<div align="center">

**Built with ❤️ for SIH 2025**

*Silence the Noise. Confirm the Breach.*

</div>
