# 🌱 CropMind

**An integrated AI digital operating system for smart agriculture in Egypt.**

CropMind unifies farm operations, financial administration, and market sales in one platform. A web dashboard serves farm managers, a mobile app serves field workers, and an AI engine with ML models and IoT telemetry supports daily decisions.

> Built as a team project for the Digilians 9-Month Professional Diploma in Applied AI and Data Analytics (Military Technical College).

<!-- TODO: add 2-3 screenshots (web dashboard, mobile scanner, Farm DNA score) -->

---

## The Problem

Egyptian agriculture faces water scarcity, a large crop-yield gap, climate uncertainty, and volatile market prices. Most farm management tools solve one task only (disease diagnosis, or sensor logging), so farmers have no single view of their operation.

## The Solution

CropMind is built around three pillars: **Farm**, **Business**, and **Market**.

| Pillar | What it covers |
|---|---|
| Farm | Field tasks, plant disease scanning, soil and weather telemetry, irrigation insight |
| Business | Finance, inventory, workforce management |
| Market | Commodity price forecasting and sales intelligence |

## Key Features

- **Farm DNA Score:** one weighted index of farm status across Crop Health, Soil Health, Water Efficiency, Operational Efficiency, Market Readiness, and Risk Exposure.
- **7 AI agents** (Farm Intelligence, Resource Optimization, Finance, Market Intelligence, Inventory, Workforce, and an **Arabic Farm Copilot**) built with LangChain and Groq (Llama 3).
- **4 ML models:**
  - CNN (TensorFlow Lite) for plant disease diagnosis on mobile
  - XGBoost for crop yield estimation
  - Prophet / LSTM for commodity price forecasting
  - Isolation Forest for telemetry anomaly detection
- **IoT telemetry** from ESP32 sensors over MQTT.
- **5 n8n automation workflows:** Daily Health Check, Weather Alert, Disease Outbreak, Price Spike, Weekly Report.
- **Two user roles:** Manager (web dashboard) and Worker (mobile app).

## Architecture

Five-layer design:

| Layer | Technology |
|---|---|
| Frontend | React 18 (web), React Native + Expo (mobile) |
| Backend API | Python 3.11, FastAPI, Pydantic, SQLAlchemy, JWT auth |
| Database | PostgreSQL 15 |
| AI Engine | LangChain, Groq API (Llama 3 70B) |
| ML / Vision | XGBoost, Prophet, scikit-learn, TensorFlow Lite |
| IoT | ESP32, MQTT (Mosquitto) |
| Automation | n8n |

Example API routes:

```
POST /api/v1/auth/login           # authenticate, returns JWT
POST /api/v1/telemetry/submit     # ingest ESP32 sensor payload
POST /api/v1/vision/scan          # leaf photo -> disease prediction
GET  /api/v1/farm-dna/{farm_id}   # composite Farm DNA score
POST /api/v1/agents/query         # route a prompt to the agent bus
```

## Repository Structure

```
backend/          FastAPI application
frontend/         React web dashboard (manager)
mobile/           React Native app (worker)
ai_engine/        LangChain multi-agent system
ml_models/        Yield, price, and anomaly models
computer_vision/  Plant disease classification
iot/              ESP32 firmware and MQTT setup
automation/       n8n workflows
analytics/        Farm DNA scoring and analytics
data/             Datasets
infrastructure/   Deployment and configuration
docs/             Project documentation
```

## Documented Results

Reported in the project thesis (demonstration setup):

- **94%** classification accuracy for the TFLite disease scanner (23 classes, 34,500 images from a PlantVillage subset)
- **R² = 0.91** for XGBoost yield prediction
- **< 10% MAE** for commodity price forecasting
- Demonstration Farm DNA score of **84%**

## Getting Started

Prerequisites: Python 3.11+, Node.js, PostgreSQL 15.

```bash
git clone https://github.com/Goda-Emad/<repo-name>.git
cd <repo-name>
```

On Windows, use the included scripts:

```
run_backend.bat     # start the FastAPI backend
run_frontend.bat    # start the web dashboard
start.bat           # start the full project
```

<!-- TODO: add .env variables (database URL, Groq API key, MQTT broker) and mobile app run steps -->

## Team

- Goda Emad
- Ahmed Salama
- Ibrahim Elshafey
- Alwafa Ashour
- Elia Fahmy

Supervised by Dr. Ali Khalifa.

## License

MIT, see [LICENSE](LICENSE).
