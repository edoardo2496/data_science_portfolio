# Industrial Machine Anomaly Detection

An end-to-end **Industrial IoT and Machine Learning project** for monitoring heavy machinery through simulated sensor data and detecting abnormal operating conditions.

The project simulates the telemetry of a construction machine — such as an excavator, wheel loader, or compactor — and builds a pipeline capable of:

* generating realistic machine sensor data;
* simulating normal and abnormal operating conditions;
* processing and validating telemetry;
* extracting relevant features;
* detecting anomalies using statistical and Machine Learning techniques;
* evaluating the quality of the detection;
* visualizing machine health and anomalous events.

The long-term goal is to reproduce, in a simplified environment, the architecture of an **Industrial IoT predictive-maintenance system**.

---

## Project Architecture

```text
┌─────────────────────┐
│  Machine Simulator  │
│       C / C++       │
└──────────┬──────────┘
           │
           │ telemetry
           ▼
┌─────────────────────┐
│   Sensor Data       │
│ Temperature         │
│ Pressure            │
│ Vibration           │
│ RPM                 │
│ Fuel consumption    │
│ Load                │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Data Processing     │
│       Python        │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Feature Engineering │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Anomaly Detection   │
│                     │
│ Statistical models  │
│ Isolation Forest    │
│ Other ML models     │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Monitoring &        │
│ Visualization       │
└─────────────────────┘
```

---

## 1. Machine Simulation

The first component of the project is a machine simulator written in **C/C++**.

Instead of collecting data from a physical machine, the simulator generates synthetic telemetry representing the behavior of a heavy industrial machine.

Possible variables include:

| Sensor                  | Description               |
| ----------------------- | ------------------------- |
| `engine_rpm`            | Engine rotational speed   |
| `engine_temperature`    | Engine temperature        |
| `hydraulic_pressure`    | Hydraulic system pressure |
| `hydraulic_temperature` | Hydraulic oil temperature |
| `vibration`             | Machine vibration level   |
| `fuel_rate`             | Fuel consumption rate     |
| `engine_load`           | Estimated engine load     |
| `operating_hours`       | Machine operating hours   |

The simulator will reproduce both:

### Normal operation

The machine operates within expected physical ranges, with realistic noise and correlations between variables.

### Abnormal operation

Fault conditions will be introduced progressively, for example:

* overheating;
* abnormal vibration;
* hydraulic pressure degradation;
* excessive engine load;
* sensor drift;
* combinations of multiple abnormal signals.

The objective is not simply to generate random outliers, but to create **time-dependent failure patterns** that resemble what could happen in a real machine.

---

## 2. Telemetry Pipeline

The simulated machine produces a continuous stream of telemetry.

A simplified record may look like:

```text
timestamp,
engine_rpm,
engine_temperature,
hydraulic_pressure,
hydraulic_temperature,
vibration,
fuel_rate,
engine_load
```

Example:

```text
2026-10-05 08:32:01,
1850,
87.4,
245.2,
61.8,
0.42,
18.7,
0.71
```

The telemetry can initially be stored in CSV files and later extended to a more realistic streaming architecture.

---

## 3. Feature Engineering

Raw sensor measurements are not always sufficient to detect machine degradation.

The analysis pipeline will therefore derive additional features such as:

* rolling mean;
* rolling standard deviation;
* rate of change;
* moving maximum/minimum;
* temperature gradients;
* vibration statistics;
* load-normalized fuel consumption;
* relationships between hydraulic pressure and engine load;
* time spent outside normal operating ranges.

For example:

```text
temperature_delta_5m
vibration_std_30s
pressure_change_rate
fuel_per_load
rolling_engine_temperature
```

This allows the model to capture not only **what the machine is doing**, but also **how its behavior is changing over time**.

---

## 4. Anomaly Detection

The core objective is to identify machine states that deviate from expected behavior.

The project will progressively compare different approaches.

### Baseline: statistical detection

Simple rules based on:

* physical thresholds;
* z-scores;
* rolling statistics;
* control limits.

This provides an interpretable baseline.

### Machine Learning

The project will then investigate unsupervised anomaly-detection algorithms such as:

* Isolation Forest;
* Local Outlier Factor;
* One-Class SVM;
* clustering-based approaches.

The important assumption is that **failure data are scarce**, which is common in industrial environments.

Therefore, the initial problem will be treated primarily as an **unsupervised / semi-supervised anomaly detection problem**.

---

## 5. From Anomaly Detection to Predictive Maintenance

Detecting an abnormal sensor reading is only the first step.

The project will eventually distinguish between:

```text
Normal operation
       │
       ▼
Early degradation
       │
       ▼
Anomalous behavior
       │
       ▼
Potential fault
       │
       ▼
Maintenance required
```

This opens the possibility of extending the project toward:

* failure prediction;
* Remaining Useful Life (RUL) estimation;
* fault classification;
* maintenance scheduling;
* machine health scoring.

---

## 6. Technology Stack

### Simulation

* C++
* CMake

### Data Engineering & Analysis

* Python
* NumPy
* Pandas
* SciPy

### Machine Learning

* scikit-learn
* potentially PyTorch for future experiments

### Visualization

* Matplotlib
* Plotly

### Development

* Git
* GitHub
* VS Code

The project is intentionally split between **C/C++ and Python**.

C/C++ is used to reproduce the type of low-level machine/edge-side environment that could generate telemetry, while Python is used for data analysis and Machine Learning.

---

## 7. Repository Structure

The repository will progressively evolve toward the following structure:

```text
industrial-machine-anomaly-detection/
│
├── simulator/
│   ├── src/
│   ├── include/
│   ├── tests/
│   └── CMakeLists.txt
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│   ├── 01_exploration.ipynb
│   ├── 02_feature_engineering.ipynb
│   └── 03_anomaly_detection.ipynb
│
├── src/
│   ├── data/
│   ├── features/
│   ├── models/
│   └── evaluation/
│
├── tests/
│
├── configs/
│
├── reports/
│   └── figures/
│
├── requirements.txt
├── README.md
└── LICENSE
```

---

## 8. Development Roadmap

### Phase 1 — Machine simulator

* [ ] Define machine operating states
* [ ] Implement sensor models
* [ ] Add realistic noise
* [ ] Implement machine workload
* [ ] Generate telemetry
* [ ] Implement abnormal operating conditions

### Phase 2 — Data pipeline

* [ ] Store telemetry
* [ ] Data validation
* [ ] Missing-value handling
* [ ] Outlier analysis
* [ ] Feature engineering

### Phase 3 — Anomaly detection

* [ ] Statistical baseline
* [ ] Isolation Forest
* [ ] One-Class SVM
* [ ] Compare detection performance
* [ ] Tune detection thresholds

### Phase 4 — Industrial monitoring

* [ ] Machine health score
* [ ] Event detection
* [ ] Visualization dashboard
* [ ] Historical machine analysis

### Phase 5 — Predictive maintenance

* [ ] Simulate progressive degradation
* [ ] Define failure events
* [ ] Investigate early-warning detection
* [ ] Estimate time-to-failure
* [ ] Explore RUL models

### Phase 6 — Edge/IoT architecture

* [ ] Streaming telemetry
* [ ] MQTT communication
* [ ] Edge-side preprocessing
* [ ] Model inference at the edge
* [ ] Centralized monitoring

---

## 9. Project Objective

This project is intended as a practical exploration of the intersection between:

**Industrial Engineering + Software Engineering + IoT + Data Science + Machine Learning.**

The final system should resemble a simplified industrial architecture:

```text
PHYSICAL MACHINE
       │
       ▼
    SENSORS
       │
       ▼
 EDGE / EMBEDDED SYSTEM
       │
       ▼
 TELEMETRY PIPELINE
       │
       ▼
 DATA PROCESSING
       │
       ▼
 MACHINE LEARNING
       │
       ▼
 MACHINE HEALTH
       │
       ▼
 MAINTENANCE DECISION
```

The emphasis is therefore not only on achieving a good Machine Learning score, but on understanding the complete engineering pipeline from **machine → data → model → decision**.

---

## Status

🚧 **Work in progress**

The project is currently in the design and simulation phase.

