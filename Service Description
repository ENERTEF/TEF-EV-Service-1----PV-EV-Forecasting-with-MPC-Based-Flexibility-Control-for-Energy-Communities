# Energy Community Sharing & EV Charging Flexibility Optimization (ECC)

**Service:** Energy Community Sharing & EV Charging Flexibility Optimization
**TEF:** TEF EV – Leneda (Luxembourg)
**End User:** EMOT EMOTION SRL
**Site:** Copal Supermarket Energy Community
**Version:** 1
**Last Updated:** 07 Dec 2025

---

# Overview

The **Energy Community Sharing & EV Charging Flexibility Optimization Service (ECC)** transforms the **TEF EV Leneda time-series dataset** for the Copal Supermarket energy community into an **operational, settlement-aware orchestration layer**.

The service combines:

* Measured electricity signals (consumption and production)
* **Layer-2 sharing allocation outputs (ACR)**
* Forecasting and optimization methods

It produces:

* Auditable energy ledgers
* PV and EV load forecasts
* Flexibility envelopes
* **Model Predictive Control (MPC)** EV charging recommendations

The service is designed for **continuous operational use** with:

* traceable inputs
* reproducible optimization runs
* auditability for energy settlement and validation

---

# 1. Business Context & Definitions

The ECC service focuses on a **PV + EV charging energy community use case**.

Key characteristics:

* **PV production drives local energy availability**
* **EV charging load is the controllable demand**
* The objective is to **shift EV charging to periods of PV generation**

This enables:

* higher local renewable consumption
* reduced grid export
* reduced peak imports

The service integrates **ACR (Collective Renewable Self-Consumption) allocation outputs**, ensuring all operational outputs remain **consistent with energy settlement mechanisms**.

---

# Site Specifications (ECC)

**PV Plant**

| Parameter          | Value                 |
| ------------------ | --------------------- |
| Installed capacity | 973.81 kWc (~1 MW)    |
| Coordinates        | 6.48714 E, 49.70673 N |

**EV Chargers**

| Charger Type | Quantity | Power  |
| ------------ | -------- | ------ |
| AC chargers  | 8        | 22 kW  |
| DC chargers  | 4        | 300 kW |
| DC chargers  | 4        | 400 kW |

**Battery storage:**
Not installed (battery dispatch is **out of scope**).

---

# Key Terms

| Term                                            | Definition                                                                        |
| ----------------------------------------------- | --------------------------------------------------------------------------------- |
| **Energy Community (ECC)**                      | Sharing group at Copal Supermarket with ACR allocation outputs                    |
| **ACR (Collective Renewable Self-Consumption)** | Allocation framework distributing locally produced electricity among participants |
| **Metering point / POD**                        | Unique identifier of a metered connection                                         |
| **OBIS code**                                   | Standard identifier of measured electricity quantities                            |
| **Timestamp ("Started at")**                    | Start of 15-minute interval including timezone                                    |
| **Resolution / Granularity**                    | 15-minute intervals                                                               |
| **Measured / Estimated / Edited**               | Data quality indicator                                                            |
| **Sharing outputs (Layer-2)**                   | Computed values describing energy allocation in the community                     |
| **Flexibility envelope**                        | Allowed modulation capacity for EV charging                                       |
| **Model Predictive Control (MPC)**              | Rolling optimization solving every 15 minutes                                     |

---

# 1.1 End User Context (EMOT Operator View)

The service supports **EMOT EMOTION SRL** in planning and operating EV-ready energy communities.

For the **Copal Supermarket site**, the objectives are:

* Increase **local PV consumption**
* Reduce **PV export (reverse power flow)**
* Reduce **grid import peaks**
* Provide **transparent and auditable energy ledgers**

Operationally, the service:

* produces **rolling control recommendations every 15 minutes**
* enables **backtesting** to quantify improvements versus uncontrolled EV charging

Each optimization result is fully **traceable to input datasets and versions**.

---

# 2. Problem Statement

The service delivers a **production-grade optimization capability** that:

## 1. Builds a settlement-aware energy ledger

At **15-minute resolution**, integrating:

* measured PV production
* EV charging consumption
* Layer-2 ACR allocation outputs

## 2. Generates forecasts

For:

* EV charging baseline consumption
* PV production
* derived import/export risks

## 3. Runs MPC optimization

The optimization recommends **EV charging load shifting** to:

* reduce PV export to the market
* increase PV self-consumption
* reduce grid import peaks
* ensure smooth and realistic control actions

## 4. Ensures auditability

Outputs maintain full lineage to:

* Metering point
* OBIS code
* Timestamp
* Interval length
* Version
* Data quality flags

---

# 3. Data Description

## 3.1 ECC Input Schema

Each record includes:

| Field                         | Description                 |
| ----------------------------- | --------------------------- |
| Metering point                | Unique POD identifier       |
| OBIS code                     | Signal identifier           |
| Unit                          | kW                          |
| Started at                    | Timestamp of interval start |
| Value                         | Numeric measurement         |
| Interval length               | Expected 15 minutes         |
| Estimated / measured / edited | Data quality indicator      |
| Version                       | Data revision index         |

---

## 3.2 Data Dictionaries

| Signal                            | OBIS code   | CSV file                            | Unit | Time range              | Notes                 |
| --------------------------------- | ----------- | ----------------------------------- | ---- | ----------------------- | --------------------- |
| Measured active consumption       | 1-1:1.29.0  | ECC_ACR_8_consumers_PV_Active_C.csv | kW   | 2023-10-11 → 2025-11-13 | Community consumption |
| Measured active production        | 1-1:2.29.0  | ECC_PV_Active_P.csv                 | kW   | 2023-10-11 → 2025-11-13 | PV production         |
| Consumption covered by production | 1-65:1.29.3 | ECC_PV_Consumption.csv              | kW   | 2024-07-15 → 2025-11-12 |                       |
| Remaining consumption invoiced    | 1-65:1.29.9 | ECC_PV_C_Remained.csv               | kW   | 2025-02-23 → 2025-11-12 |                       |
| Production shared within group    | 1-65:2.29.3 | ECC_PV_P_Shared.csv                 | kW   | 2024-07-15 → 2025-11-12 | ACR sharing           |
| Remaining production sold         | 1-65:2.29.9 | ECC_PV_P_Remained.csv               | kW   | 2024-07-15 → 2025-11-12 | PV export             |

---

## 3.3 Site Metering Points

### PV Meter

| Parameter   | Value                             |
| ----------- | --------------------------------- |
| POD         | LU0000010669300000000000770597826 |
| Capacity    | 973.81 kWc                        |
| Coordinates | 6.48714 E, 49.70673 N             |

---

### EV Charging Meters

| Charger group | Configuration                | POD                               |
| ------------- | ---------------------------- | --------------------------------- |
| CBB EMOB 1    | 4 × DC 300 kW                | LU0000010669300000000000070591610 |
| CBB EMOB 2    | 4 × DC 400 kW + 8 × AC 22 kW | LU0000010669300000000000070620104 |

---

### Community Consumption (ACR)

Community contains **8 PODs**, including the EV chargers.

Aggregated consumption identifier:

```
LU0000010669300000000000070597826
```

---

### ACR Sharing Signals

| Signal                             | OBIS        |
| ---------------------------------- | ----------- |
| Consumption covered by production  | 1-65:1.29.3 |
| Remaining consumption invoiced     | 1-65:1.29.9 |
| Production shared within group     | 1-65:2.29.3 |
| Remaining production sold/exported | 1-65:2.29.9 |

---

## 3.4 Reconciliation Identities (QA)

The following consistency checks are used.

### Production split (validated)

```
Measured Production
= Shared Production
+ Remaining Production Sold
```

```
1-1:2.29.0
=
1-65:2.29.3
+
1-65:2.29.9
```

### Consumption split (ECC caveat)

Target check:

```
Measured Consumption
≈ Covered Consumption
+ Invoiced Consumption
```

```
1-1:1.29.0
≈
1-65:1.29.3
+
1-65:1.29.9
```

---

# 4. Analytics Scope & Update Frequency

| Parameter        | Value                           |
| ---------------- | ------------------------------- |
| Forecast horizon | 24–48 hours                     |
| Time resolution  | 15 minutes                      |
| Update frequency | Every 15 minutes                |
| Execution mode   | Rolling operation + backtesting |

---

## Output Package Per Run

Each run produces:

* **Issue time (UTC)**
* Forecasts for:

  * EV charging load
  * PV production
* **MPC optimization results**

  * EV charging modulation trajectory
* Derived KPIs

  * import/export metrics
  * peak demand metrics
* Traceability metadata

  * input data versions
  * model version
  * run ID

---

# 5. Evaluation Protocols & Metrics

The evaluation ensures the service provides **stable and operational optimization results**.

---

## 5.1 Backtesting Protocol

Evaluation uses a **rolling historical simulation**.

Procedure:

1. Select a historical period.
2. At each decision timestamp:

   * use only data available at that time
3. Generate forecasts.
4. Run MPC optimization.
5. Apply only the **first control action**.
6. Compare results with a **baseline (uncontrolled charging)**.

---

## 5.2 Data Gaps & Exceptions

Handling rules:

* Missing or invalid intervals are **excluded from scoring**
* If insufficient data exists:

  * the service returns a structured error
  * or falls back to safe behavior:

```
u = 0
```

(no EV charging control applied)

---

## 5.3 KPIs

### Export Reduction

Reduction in exported PV energy.

Proxy signals:

* `1-65:2.29.9`
* or derived grid export intervals

---

### Import Energy & Peak Reduction

Measured via:

* total grid import reduction
* peak demand reduction

---

### PV-to-EV Alignment

Increase in intervals where:

```
EV charging ≈ PV production
```

---

### Control Smoothness

Measured via:

* ramp usage
* boundedness of charging adjustments

---

### Forecast Accuracy (optional)

Metrics:

* MAE
* RMSE

For:

* PV production forecast
* EV load baseline forecast

---

# 6. Deliverables & Submissions

The service lifecycle produces **three reports**.

---

## 6.1 Deliverable Reports

### 1️⃣ Pre-Service Deliverable

**Service Design & Setup Report**

Includes:

* analytical approach
* forecasting methodology
* baseline definition
* MPC formulation
* backtesting plan

---

### 2️⃣ Intermediate Deliverable

**Interim Performance & Operations Report**

Includes:

* data coverage
* preliminary KPI results
* limitations
* calibration updates

---

### 3️⃣ Final Deliverable

**Final Evaluation & Recommendations Report**

Includes:

* final performance results
* KPI improvements
* operational recommendations
* future roadmap

Example improvements:

* EV session-aware control
* enhanced telemetry integration

---

## 6.2 Technical Submissions

Required artifacts:

* **Service interface documentation**

  * input/output formats
  * run configuration
  * audit metadata

* **Deployment artifacts**

  * reproducible environment
  * containerization if required

* **Configuration documentation**

  * model versions
  * dataset versions
  * calibration parameters

* **Security & data protection notes**

  * handling of site identifiers
  * GDPR-aligned logging practices
