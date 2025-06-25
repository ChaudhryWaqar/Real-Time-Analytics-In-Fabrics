# 🌆 Smart City Real-Time Analytics – Microsoft Fabric (PoC)

> Real-Time Urban Monitoring & KPI Alerting System Using **Azure IoT Hub** + **Microsoft Fabric (Eventstream, Eventhouse, Lakehouse)**

---

## 📌 Project Overview

This project demonstrates how to build a **Smart City Real-Time Analytics Platform** using **Microsoft Fabric** and **Azure IoT Hub**. The architecture ingests sensor data from cities across **Florida, USA** for **traffic, pollution, environmental, and signal monitoring**, enabling instant insight via **1-second dashboards** and **automated alerts**.

---

## 📡 Key Components

| Component                      | Description                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| **Azure IoT Hub**             | Collects 1-second interval data from physical sensors (Vehicle, Speed, AQI). |
| **Fabric Eventstream**        | Streams data into real-time systems (Eventhouse, Lakehouse).                |
| **Eventhouse (Hot Data)**     | Real-time KQL analytics & dashboards (1s refresh).                          |
| **Lakehouse (Cold Data)**     | Historical storage in Delta tables for batch queries.                      |
| **KQL Dashboards**            | Visualize key metrics with line, bar, area charts.                         |
| **Data Activator**            | Triggers real-time alerts (e.g. AQI > 150) via Email/MS Teams.             |

---

## 🧠 Key Metrics (KQL-Based KPIs)

✅ **Traffic Metrics**:  
- Total Vehicle Count  
- Average Speed  
- Queue Length by Intersection  
- Congestion Level %

✅ **Pollution KPIs**:  
- AQI Categorization  
- Pollutant Distribution (PM2.5, CO₂, NOx)

✅ **Environment KPIs**:  
- Avg Temp / Humidity  
- Fog Level Index  
- Rainfall Trend

✅ **Signal KPIs**:  
- % Red Signal Time  
- Adaptive Signal Usage  
- Intersection Load

---

## 🚀 Real-Time Dashboard Preview

🔗 **Live Dashboard (Fabric Real-Time)**  
> [👉 Click to Open Live Dashboard](#)  
> _(replace with your actual dashboard link or Fabric workspace link)_

📊 **Power BI .pbix File**  
> [📥 Download Dashboard.pbix](dashboards/Dashboard.pbix)


