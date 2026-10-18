# Airport Operations Coordination Engine
## Module: Flight Operations & Flight Status
### "AI Flight Risk & Impact Cockpit"

> **Real-time flight monitoring, delay risk analysis and operational impact assessment.**

---

### 1. Overview
The **Flight Operations & Flight Status** module is an enterprise-grade aerospace decision-support cockpit engineered for airport coordinators and collaborative decision-making (A-CDM) teams. Rather than presenting a static flight table, this module provides an **AI Flight Risk & Impact Cockpit** designed to answer key operational questions in real time:
1. Which flights are at risk?
2. What is their real-time operational status?
3. What are the explainable root causes of risk?
4. What is the expected delay and delay probability?
5. How will gates, crew rosters, downstream flights, and connecting passengers be impacted?
6. What will happen if a delay increases by +15, +30, or +60 minutes (What-If Simulation)?
7. What proactive advisory action should the airport take?

---

### 2. Architecture & File Structure

```
airport-flight-ops-cockpit/
├── index.html                     # HTML5 shell with dark aerospace styling & JetBrains Mono fonts
├── vite.config.js                 # Vite bundling configuration
├── package.json                   # Project manifest (React, Vite, Lucide-React)
├── src/
│   ├── main.jsx                   # React root entry point
│   ├── App.jsx                    # Root app wrapper rendering FlightOperations page
│   ├── index.css                  # Aviation dark command cockpit design system
│   │
│   ├── data/
│   │   └── demoFlights.js         # Realistic 12-flight dataset with telemetry & risk metadata
│   │
│   ├── services/
│   │   └── flightApi.js           # API-ready service (Promise-based abstraction for backend connection)
│   │
│   ├── pages/
│   │   └── FlightOperations.jsx   # Master cockpit layout combining feed & analysis panel
│   │
│   └── components/
│       ├── SummaryCards.jsx       # Dynamic fleet metrics (Total, On Time, Delayed, High Risk, Critical)
│       ├── SearchFilters.jsx      # Multi-field search, status/risk filter tabs, sorting & view switcher
│       ├── FlightCard.jsx         # Priority flight card with gauge, route strip, & disruption factors
│       ├── FlightTable.jsx        # High-density operational table view
│       ├── RiskScore.jsx          # Reusable SVG radial risk gauge (0-30 Low, 31-60 Med, 61-80 High, 81-100 Crit)
│       ├── RiskFactors.jsx        # Explainable AI root-cause diagnostics (Weather, Gate, Crew, etc.)
│       ├── ImpactSimulator.jsx    # KEY FEATURE: What-if delay simulator (+15m, +30m, +60m)
│       ├── FlightDependency.jsx   # 5-Node visual cascading resource dependency chain
│       ├── AIRecommendation.jsx   # Advisory recommendation with Human-in-the-Loop approval
│       └── AgentStatus.jsx        # Multi-Agent pipeline synchronization states
```

---

### 3. Key Features

#### 1. Dynamic Flight Operations Cockpit
- Real-time dynamic KPI cards calculating **Total Flights**, **On Time**, **Delayed**, **High Risk**, and **Critical**.
- Click-to-filter capability on summary cards for rapid operational filtering.

#### 2. Advanced Search, Filter & Dual View
- Search across flight number (`AI-452`), origin (`DEL`), destination (`HYD`), or airline (`Air India`).
- Filter by operational status (**On Time**, **Delayed**, **Cancelled**) and risk tier (**High Risk**, **Critical**).
- Sort by **Highest Risk**, **Highest Delay**, **Earliest Departure**, or **Flight Number**.
- Dual view toggle: **Cockpit Cards View** and **Operations Table View**.

#### 3. Priority Flights Section
- Prioritizes flights with the highest operational risk score.
- Displays flight trajectory, status badges, delay minutes, delay probability, and primary disruption factors.

#### 4. Explainable Risk Score & Diagnostics
- **Aviation Radial Gauge**: Visualizes composite risk score (0–100) with color-coded safety brackets.
- **Explainable Factors**: Transparent breakdown of root causes (Weather radar cells, departure queues, gate occupancy buffer, inbound delay, ramp staffing).

#### 5. Unique Key Feature: Delay Impact Simulator
- Allows airport controllers to simulate hypothetical delays (**+15 min**, **+30 min**, **+60 min**).
- Recalculates projected departure time and forecasts operational consequences across:
  - **Gate Impact**: Tarmac holds, apron congestion, and stand turnover bottlenecks.
  - **Downstream Aircraft Rotation**: Turnaround compression on subsequent flights.
  - **Flight Crew Duty Limits**: Crew rest depletion and Flight Duty Period (FDP) timeouts.
  - **Passenger Transfers**: Missed connecting flight projections and bag transfers.
  - **Overall Impact**: Multi-resource weighted operational severity with mitigation guidance.

#### 6. Visual Flight Dependency Chain
- Visualizes the 5-node operational chain:
  `Current Aircraft → Assigned Gate → Assigned Crew → Next Flight Rotation → Connecting Passengers`
- Highlights critical international transfers (e.g., ORD, FRA, JFK).

#### 7. AI Recommendation & Human-in-the-Loop Governance
- Displays actionable advisory proposals with confidence metrics.
- Enforces human operator authorization before tactical dispatch, recording an audit log reference.

#### 8. Multi-Agent Pipeline Visualization
- Illustrates data flow across autonomous cognitive agents:
  `Research Agent → Analysis Agent → Resource Agent → Planning Agent → Decision Agent`

---

### 4. Running the Project Locally

```bash
# 1. Navigate to the project directory:
cd "C:\Users\sindh\.gemini\antigravity\scratch\airport-flight-ops-cockpit"

# 2. Run the Vite development server:
npm run dev

# 3. Open your browser:
# Navigate to http://localhost:5173
```

---

### 5. Backend Team Integration Guide
To integrate this module with backend services:
1. Open `src/services/flightApi.js`.
2. Define `VITE_AIRPORT_API_URL` in an `.env` file (e.g., `VITE_AIRPORT_API_URL=http://localhost:8000`).
3. Uncomment the provided `fetch()` calls in:
   - `getFlights()` → `GET /api/v1/flights`
   - `getFlightById(id)` → `GET /api/v1/flights/:id`
   - `getFlightRisk(id)` → `GET /api/v1/ml/risk-analysis/:id`
   - `getFlightImpact(id, minutes)` → `POST /api/v1/simulator/delay-impact`
   - `approveRecommendation(id, action)` → `POST /api/v1/decision-agent/approve`

---

### 6. Safety & Non-Authoritative Advisory Disclaimer
This application is designed strictly as a **decision-support and demonstration interface**. It does not exert autonomous control over aircraft, runway operations, or air traffic control. Operational recommendations require human coordinator authorization.
