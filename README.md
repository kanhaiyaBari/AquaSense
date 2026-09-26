# TechCore 💧
### Smart Water Purification and Quality Monitoring System for Rural and Mining-Affected Areas

**Smart India Hackathon 2026 | Problem Statement ID: 26040**
**Theme:** Clean & Green Technology | **Category:** Hardware
**Team:** TechCore (Team ID: 53)

---

## Problem Statement

Rural and mining-affected regions in Jharkhand lack access to safe drinking water. Groundwater is commonly contaminated by:
- Suspended particles (turbidity) from mining runoff
- Excessive dissolved minerals (TDS)
- Acidic water caused by Acid Mine Drainage (mining-related pH imbalance)
- Heavy metals (arsenic, lead, mercury, uranium) leaching from mining activity
- Microbial/pathogen contamination with no real-time detection

There is currently no affordable system that both purifies contaminated water **and** provides real-time water quality information to communities and authorities.

## Our Solution

TechCore is a smart, IoT-enabled community water purification and monitoring system — think of it as a "Water-ATM" for rural and mining-affected villages. It:

- Purifies raw water through a 4-stage process: **Sediment Filter → Activated Carbon → RO/UF Membrane → UV Sterilization**
- Monitors water quality in real time using sensors at **both input and output** (pH, Turbidity, TDS, Temperature, Chlorine Residual, Bio-fluorescence)
- Uses a trained **Machine Learning model** to classify water as **Safe / Unsafe** automatically
- Blocks release of unsafe water and triggers a **3-tier alert system**: on-site display, SMS to local caretaker/ASHA worker, and a dashboard for government health authorities
- Includes a specialized **Heavy Metal & Mining-Contamination Check** model, since general water potability data doesn't cover mining-specific pollutants (arsenic, lead, mercury, uranium, etc.)

## Live Prototype

🔗 **Try it here:** [https://aquasense-upvcx5ztux5rb9dtmlmole.streamlit.app/](https://aquasense-upvcx5ztux5rb9dtmlmole.streamlit.app/)

No login required — the app is open for demo purposes.

## Features

| Feature | Description |
|---|---|
| Live Simulation | Input water quality parameters manually and get instant Safe/Unsafe prediction |
| Model Insights | View accuracy, precision, recall, confusion matrix, and feature importance |
| Alert System | Simulated real-time alerts (on-site display, SMS, dashboard) for unsafe readings |
| Heavy Metal / Mining Check | Specialized model trained on 20+ contamination parameters (arsenic, lead, mercury, uranium, cadmium, etc.) |
| Live Safety Score Feed | Rolling chart of safety scores across successive readings |

## Tech Stack

**Hardware (Full System Design):**
ESP32 Microcontroller, pH Sensor, Turbidity Sensor, TDS Sensor, Temperature Sensor (DS18B20), Chlorine Residual Sensor, Bio-fluorescence Sensor, GSM Module (SIM800L), Solar Panel + Battery, RO/UF Membrane, UV Sterilizer

**Software / AI (This Prototype):**
- Python
- Pandas, NumPy
- Scikit-learn, XGBoost (Machine Learning classifiers — Random Forest, Gradient Boosting)
- Plotly (visualizations)
- Streamlit (web app / dashboard)

## Machine Learning Models

**1. Water Potability Model**
Trained on the [Kaggle Water Potability Dataset](https://www.kaggle.com/datasets/adityakadiwal/water-potability) — pH, Hardness, Solids, Chloramines, Sulfate, Conductivity, Organic Carbon, Trihalomethanes, Turbidity.
- Accuracy: ~68.75% (Gradient Boosting)
- Recall on unsafe water: 94% (optimized to minimize false negatives — missing contamination is more dangerous than a false alarm)

**2. Heavy Metal & Mining-Contamination Model**
Trained on the [Kaggle Water Quality (Heavy Metals) Dataset](https://www.kaggle.com/datasets/mssmartypants/water-quality) — aluminium, ammonia, arsenic, barium, cadmium, chromium, lead, mercury, uranium, and more.
- Accuracy: 96.9% | Precision: 88.0% | Recall: 84.6% | F1 Score: 86.3% | ROC-AUC: 98.6%

## Why No Dedicated Heavy Metal Sensors?

Direct heavy-metal detection requires Ion-Selective Electrode (ISE) sensors, which cost several thousand rupees per parameter and need frequent calibration — not viable for a low-cost, field-deployable rural unit.

Instead, we use the chemistry of mining contamination as a proxy: mining exposes sulfide minerals to air and water, producing sulfuric acid (**Acid Mine Drainage**). This process both lowers pH **and** dissolves heavy metals into the water. So an abnormally low pH combined with elevated TDS is a scientifically grounded early-warning signature for possible heavy metal contamination — flagged by our system for lab-based confirmation, using sensors already in our design. Dedicated heavy-metal sensors remain a planned next-phase hardware upgrade.

## System Architecture

```
Raw Water Input
      ↓
Input Sensors (pH, Turbidity, TDS, Temperature)
      ↓
Sediment Filter → Activated Carbon → RO/UF Membrane → UV Sterilization
      ↓
Output Sensors (pH, Turbidity, TDS, Temperature, Chlorine Residual, Bio-fluorescence)
      ↓
ESP32 Controller + ML Model → Safe / Unsafe Classification
      ↓
   SAFE → Valve Opens → Water Released
   UNSAFE → Valve Blocked → Alerts Triggered
      ↓
On-site Display | SMS to Caretaker | Government Dashboard
```

Built on the standard **Five-Layer IoT Architecture**: Perception → Transport → Processing → Application → Business.

## Running Locally

```bash
# Clone the repository
git clone https://github.com/kanhaiyaBari/AquaSense.git
cd AquaSense

# Install dependencies
pip install -r requirements.txt

# Run the app
streamlit run app.py
```

## Project Structure

```
TechCore/
├── app.py                # Main Streamlit application
├── requirements.txt       # Python dependencies
└── artifacts/             # Trained model files and supporting assets
```

## Research References

- Singh et al. (2018) — Groundwater Heavy Metals, East Singhbhum, Jharkhand
- Giri et al. (2023) — Metal Contamination, Iron Mining Area, Jharkhand
- Groundwater Suitability, Charhi & Kuju Coal Mining Areas, Jharkhand
- Jal Jeevan Mission — Water Quality Monitoring Framework
- WHO — Guidelines for Drinking-water Quality, 2026
- Essamlali et al. (2024) — ML & IoT for Water Quality Monitoring (Heliyon)

## Team

Built by **Team TechCore** for Smart India Hackathon 2026 — Problem Statement 26040.

---

*This is a hackathon prototype. Hardware components described above represent the full proposed system design; the current deployed application simulates the AI/ML decision-making layer using real trained models on real datasets.*
