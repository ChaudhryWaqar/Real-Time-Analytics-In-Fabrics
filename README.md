# Smart City Real-Time Analytics – Microsoft Fabric (PoC)

**End-to-End Real-Time Data Engineering and Analytics Solution using Azure IoT Hub and Microsoft Fabric (Eventstream, Eventhouse, Lakehouse)**

---

## Project Overview

This project is a **Proof of Concept (PoC)** demonstrating how **Microsoft Fabric’s Real-Time Intelligence architecture** can be used to monitor and analyze **Smart City operations** — such as **traffic**, **pollution**, **environmental conditions**, and **signal performance** — across multiple cities in real time.

As a **Fabric Data Engineer**, the goal is to design a scalable pipeline that supports both **streaming (hot path)** and **batch (cold path)** analytics, ensuring data is actionable the moment it arrives and also available for historical trend analysis.

This solution integrates **IoT sensor data from Azure IoT Hub**, processes it through **Fabric Eventstream**, stores it in **Eventhouse** for live KQL analytics, and archives it in **Lakehouse** for deeper batch analysis.

---

## Data Flow Architecture

The following describes the end-to-end workflow within Microsoft Fabric:

1. **Data Generation Layer (IoT Sensors)**

   * Real-world or simulated sensors (traffic counters, pollution monitors, signal timers) send JSON-formatted data every second.
   * Each record includes attributes like `VehicleCount`, `AverageSpeed`, `PollutionLevel`, `FogLevel`, and `SignalStatus`.

2. **Ingestion Layer (Azure IoT Hub → Fabric Eventstream)**

   * Azure IoT Hub collects streaming telemetry from multiple sensor devices.
   * Microsoft Fabric **Eventstream** connects directly to IoT Hub using the built-in connector.
   * Eventstream performs basic transformations such as filtering, mapping fields, and routing data to multiple destinations.

3. **Processing & Analytics Layer**

   * The Eventstream routes data simultaneously to:

     * **Eventhouse (Hot Path)** – optimized for **real-time queries** using KQL.
     * **Lakehouse (Cold Path)** – optimized for **batch processing and historical analysis**.
   * As soon as events land in Eventhouse, analysts can query them using **Kusto Query Language (KQL)** for near-instant insights.

4. **Storage & Modeling Layer**

   * Eventhouse stores the live operational dataset (current window of events).
   * Lakehouse stores raw and curated datasets in **Delta format**.
   * The Lakehouse tables can be accessed in **SQL Analytics Endpoint** or via **Notebooks (Spark, Python, or SQL)** for data modeling and enrichment.

5. **Visualization & Reporting Layer (Fabric Real-Time Dashboard)**

   * KQL queries are pinned to **Fabric Real-Time Dashboards**, refreshing every second.
   * The dashboards provide metrics such as live traffic density, average speeds, and pollution trends across cities.
   * The same Lakehouse data can be connected to **Power BI Desktop** for deeper visuals and historical comparison.

6. **Automation & Alerting Layer (Data Activator)**

   * Fabric’s **Data Activator** monitors KPIs in real time and automatically triggers notifications when conditions are met.
   * Example rules:

     * Air Quality Index (AQI) > 150 → Send alert to Environment Department.
     * Vehicle Count > 120 → Notify Traffic Control Center.
     * FogLevel > 0.6 → Issue visibility warning.

---

## Key Fabric Components and Their Roles

| Component                 | Role in Architecture                                                                                  |
| ------------------------- | ----------------------------------------------------------------------------------------------------- |
| **Azure IoT Hub**         | Collects sensor data from multiple IoT devices every second.                                          |
| **Fabric Eventstream**    | Acts as a real-time data router, ingesting and distributing data streams to Eventhouse and Lakehouse. |
| **Eventhouse (Hot Path)** | Real-time analytical store used for low-latency queries and dashboards via KQL.                       |
| **Lakehouse (Cold Path)** | Long-term storage and historical dataset for advanced analytics and ML.                               |
| **KQL Dashboards**        | Real-time monitoring dashboards built on top of Eventhouse datasets.                                  |
| **Data Activator**        | Monitors KPIs and automates alerts when thresholds are crossed.                                       |

---

## Real-Time KPI Computations (KQL Examples)

### Traffic KPIs

```kql
UnifiedSensorData
| summarize TotalVehicleCount = sum(VehicleCount), AvgSpeed = avg(AverageSpeed)
  by bin(Timestamp, 1m), City
```

### Pollution KPIs

```kql
UnifiedSensorData
| summarize AvgPollution = avg(PollutionLevel), MaxAQI = max(PollutionLevel)
  by bin(Timestamp, 5m), City
```

### Environmental KPIs

```kql
UnifiedSensorData
| summarize FogEvents = countif(FogLevel > 0.6), AvgTemp = avg(Temperature)
  by City
```

### Signal Efficiency

```kql
UnifiedSensorData
| summarize Total = count(), RedSignalTime = countif(SignalStatus == "Red")
  by IntersectionId
| extend RedTimePct = todouble(RedSignalTime) / Total * 100
```

---

## Visualization & Dashboards

* **Fabric Real-Time Dashboard**
  Displays streaming KPIs like:

  * Vehicle Count per City (Bar Chart)
  * Speed Trends (Line Chart)
  * Pollution Index by City (Area Chart)
  * Signal Red-Time Ratio (Pie Chart)

* **Power BI Integration**

  * Historical insights through Power BI Desktop using Lakehouse datasets.
  * Combined **real-time (Eventhouse)** and **batch (Lakehouse)** reports for complete situational awareness.

---

## Business Impact

This Smart City Fabric solution empowers municipalities with:

* Real-time visibility across all urban zones.
* Automated decision-making via alert triggers.
* Actionable insights for congestion, pollution, and environmental safety.
* Scalable architecture ready for expansion to multiple cities or sensor types.

---

## Recommended Next Steps

1. Implement **data quality rules** in Eventstream for cleansing.
2. Add **ML-based predictions** (e.g., AQI forecasting) in Lakehouse notebooks.
3. Enable **Power BI Direct Lake mode** for instant dashboard refresh.
4. Deploy solution as a **Fabric Data Product** for cross-departmental access.

---

## Repository Structure

```
SmartCity-Fabric-RealTime-Analytics/
│
├── data/
│   ├── sample_sensor_data.json
│   └── lakehouse_delta_tables/
│
├── kql/
│   ├── traffic_metrics.kql
│   ├── pollution_metrics.kql
│   ├── environment_metrics.kql
│   └── signal_metrics.kql
│
├── dashboards/
│   └── fabric_realtime_dashboard_config.json
│
├── notebooks/
│   └── historical_analysis.ipynb
│
├── architecture/
│   └── smartcity_fabric_architecture.png
│
└── README.md
```

---

### Summary

This project showcases how a **Microsoft Fabric Data Engineer** can build a complete **Real-Time Analytics Solution** integrating **IoT data ingestion**, **event processing**, **streaming analytics**, **data storage**, and **visualization** — all inside a unified Fabric environment.

It highlights Fabric’s power to handle both **real-time** and **historical** analytics in a single platform, enabling cities to make **data-driven decisions instantly**.


