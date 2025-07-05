````markdown
# 🅿️ Dynamic Pricing for Urban Parking Lots

**Capstone Project - Summer Analytics 2025**  
Hosted by **Consulting & Analytics Club × Pathway**

---

## 📌 Overview

Urban parking spaces are often inefficiently utilized due to **static pricing**, causing congestion and revenue loss. This project implements a **real-time dynamic pricing system** for 14 urban parking lots using **data-driven ML models** and **real-time streaming pipelines**.

💡 This pricing engine dynamically updates prices based on:

- Real-time occupancy & queue length
- Nearby traffic congestion
- Special events (holidays, city events)
- Incoming vehicle type
- Geographic competition with nearby lots

---

## 🧰 Tech Stack

| Layer            | Technology Used                  |
|------------------|----------------------------------|
| Language         | Python                           |
| Libraries        | Pandas, NumPy, Bokeh             |
| Streaming Engine | [Pathway](https://pathway.com/)  |
| Visualization    | Bokeh (real-time plots)          |
| Deployment       | Google Colab, Jupyter            |

---

## 📊 Architecture Diagram (via Mermaid)

```mermaid
graph LR
    A[Raw CSV Dataset (Simulated Stream)] --> B(Pathway Streaming Engine)
    B --> C[Feature Extraction]
    C --> D1[Model 1: Baseline Linear]
    C --> D2[Model 2: Demand-Based]
    C --> D3[Model 3: Competitive Pricing]
    D1 --> E[Price Updates]
    D2 --> E
    D3 --> E
    E --> F[Visualization: Bokeh]
    E --> G[Suggested Rerouting (Optional)]
````

---

## ⚙️ Project Architecture & Workflow

### 1. 📥 Data Stream Simulation

* The dataset simulates real-time parking lot activity across 73 days.
* Each time step (every 30 minutes from 8:00 AM to 4:30 PM) is streamed using a generator and delay (`simulate_stream.py`).

### 2. 🧠 Model Building (in order of complexity)

#### ✅ **Model 1: Baseline Linear**

* Increases price linearly with occupancy.
* `Price_t+1 = Price_t + α × (Occupancy / Capacity)`

#### ✅ **Model 2: Demand-Based Pricing**

* Uses a weighted demand function:

  ```
  Demand = α × (Occupancy / Capacity) + β × QueueLength
           - γ × Traffic + δ × IsSpecialDay + ε × VehicleWeight
  ```
* Price is adjusted relative to normalized demand.

#### ✅ **Model 3: Competitive Pricing**

* Adds geographic proximity awareness:

  * Uses Haversine formula to compute distances
  * Adjusts price based on competitor prices nearby
  * Implements rerouting or strategic price drops/hikes

### 3. 📈 Visualization

* **Bokeh** plots show real-time pricing for each lot.
* Compares all 3 models across time and location.
* Helpful for justifying pricing logic visually.

### 4. 🚀 Real-Time Stream with Pathway

* Pathway handles:

  * Delayed data ingestion
  * Timestamp preservation
  * Continuous feature processing
  * Realtime prediction emission

---

## 📂 Repository Structure

```
.
├── data/
│  └── dataset.csv
├── bokeh_plots.ipynb
├── requirements.txt
└── README.md
```

---

## ✅ Installation & Running

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Stream & Simulate Data

```python
from streaming.simulate_stream import simulate_streaming
```

### 3. Apply Models

```python
from models.model1_baseline import baseline_linear_pricing
from models.model2_demand import demand_based_pricing
from models.model3_competitive import competitive_pricing
```

### 4. Visualize

```python
from visuals.bokeh_plots import plot_prices
plot_prices(df_with_prices, lot_id=100001)
```

---

## 📅 Assumptions

* Invalid vehicle/traffic types are ignored or mapped to default.
* Rerouting is suggested only when lot is full and competitor is cheaper.
* All prices are smoothed and bounded between \$5 and \$20.

---

## 🌟 Future Enhancements

* Weather-aware pricing using public APIs
* Historical trend-based predictions
* Mobile app UI for end-user parking recommendations
* City-wide dashboard for demand heatmaps

---

## 📚 References

* [Pathway Documentation](https://pathway.com/developers/user-guide/)
* [Mermaid Live Editor](https://mermaid.live/edit)
* [Summer Analytics 2025](https://www.caciitg.com/sa/course25/)

---

## 🧠 Author

**Ayan Ali**  
🚀 Passionate about AI, data-driven systems, and real-time applications  
📧 [ayanali0249@gmail.com](mailto:ayanali0249@gmail.com)  
🌐 [LinkedIn](https://www.linkedin.com/in/ayan-ali0249) &nbsp;|&nbsp; 🌍 India  
💼 Capstone Contributor @ Summer Analytics 2025 – **Consulting & Analytics Club, IIT Guwahati**  

---

> *This project was developed as a capstone for Summer Analytics 2025 and demonstrates dynamic pricing strategies using real-time ML systems and Python data stack.*
