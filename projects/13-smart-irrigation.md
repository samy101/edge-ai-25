---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

## Smart Irrigation System for Precision Agriculture
### Introduction

The **Edge AI Precision Irrigation System** is a fully autonomous, on-device solution for dynamically adjusting water supply to **nursery-stage crops** (e.g., onion seedlings) in response to environmental and crop conditions. It integrates **historical climate data** and **real-time soil moisture sensing** into a **machine learning inference engine** running on a **microcontroller**, which computes the crop’s current water demand and controls pump actuation **without cloud reliance**.

<p align="center">
  <img src="../assets/img/projects25/13-smart-irrigation.png" 
       alt="Smart Irrigation System" 
       width="500"
       style="border-radius: 10px;">
</p>

In our implementation:
- Weather inputs (**Tmax, RH, Irradiation**) via **weather API** feed an **MLP-based model** on a **Raspberry Pi Pico W** to estimate **daily reference evapotranspiration (ET₀)**.
- ET₀ is then used to derive actual crop evapotranspiration (**ET₀ × Kc**).
- The computed water requirement is used by the Pico to set the irrigation volume.
- An **ESP32 node** drives a **water pump** via **MQTT** for the calculated duration.

Conventional irrigation often over-waters or follows rigid schedules, wasting water and harming crops. Onion seedlings are especially vulnerable:
- Early over-watering disrupts **root aeration** and **yield**.
- Uneven watering or **waterlogging** leads to **soil salinity** and **nutrient loss**.

In **water-scarce regions**, these issues are severe.

This system:
- Adjusts irrigation dynamically based on **growth stage**, **weather**, and **soil moisture**.
- Predicts **reference ET₀** and applies the **onion-specific Kc** to deliver precise water per growth stage.
- Runs entirely on the **edge**, ensuring **cloud independence**.

---

### Data Collection

#### Historical Climate Data
- Source: **NASA POWER API**
- Variables: 
  - Min & Max Temperature (`T2M_min`, `T2M_max`)
  - Relative Humidity at 2m (`RH2m`)
  - Wind Speed (`WS2m`)
  - Solar Radiation (`ALLSKY_SFC_SW_DWN`)

#### Label Generation (ET₀)
- Computed using the **FAO-56 Penman–Monteith formula**.
- These **ET₀ values** serve as labels for supervised model training.

#### Real-Time Sensor Data
- Analog **soil moisture sensor** installed per bed or pot.
- Outputs **voltage** proportional to **volumetric water content (VWC)**.
- Converted to **available water depth**.
- Feeds the controller for real-time irrigation decisions.

---

### Preprocessing & Feature Engineering

- **Outlier Removal**: Filtered extreme/erroneous values.
- **Scaling**: Applied **Z-score normalization** using `StandardScaler`.
- **Feature Selection**: Top 3 predictors identified via correlation analysis:
  - `T2M_max` (Max Temp)
  - `RH2m` (Relative Humidity)
  - `ALLSKY_SFC_SW_DWN` (Solar Radiation)

---

### Model Design and Training

#### Model Selection
- Evaluated: Linear Regression, SVR, Random Forest
- Final model: **Feedforward MLP Regressor**
- Accuracy: ~97% variance explained

#### Architecture
- Two hidden layers: 16 and 8 neurons
- Activations: **ReLU**
- Optimizer: **Adam**

#### Training Configuration
- Dataset: ~5,569 samples (80% training / 20% testing)
- **Early Stopping** after 1500 iterations
- **Performance**:
  - **MSE** ≈ 0.03
  - **R²** ≈ 0.971

---

### Methodology

#### ET₀ Prediction
- Pico gathers weather data via API: `Tmax`, `RH`, `Solar Radiation`
- Inputs fed to MLP model on-device
- Outputs **ET₀ (mm/day)**

#### Crop Water Demand (ETc)
- ET₀ × Kc (crop coefficient for growth stage) = **ETc**
- Represents daily crop water requirement

#### Soil Moisture Update
- Sensor feeds real-time **VWC**
- Converted to **Available Water Depth**
- Used to **adjust or skip watering** if soil is already wet

#### Irrigation Volume Calculation
- Rule-based logic or controller computes volume:
  - If soil moisture < target → deliver `(ETc – depletion)`
- Ensures optimal water delivery

#### Pump Actuation
- **Pico sends MQTT command** to ESP32
- **ESP32 activates relay/pump** for the required time
- Operates in a **closed loop** every 24 hours or on-demand

---

### Hardware and Software Stack

#### Hardware Components

| Component               | Specification                                           | Role/Use                                           |
|------------------------|---------------------------------------------------------|----------------------------------------------------|
| **Raspberry Pi Pico W**| RP2040 dual-core @ 133MHz, 264 KB RAM, Wi-Fi            | Hosts MLP model, sensor reading, volume calculation|
| **ESP32**              | Dual-core 240MHz MCU with Wi-Fi/Bluetooth               | Receives MQTT, actuates pump                       |
| **Soil Moisture Sensor**| Analog resistive sensor                                 | Measures real-time VWC                             |
| **Relay Module**       | 5V/12V controlled relay board                            | Switches pump power via GPIO                       |
| **Water Pump**         | 12V DC pump (~X L/min flow rate)                        | Delivers water to crop                             |

---

#### Software Stack

| Tool            | Use                                                                 |
|----------------|----------------------------------------------------------------------|
| **Python (PC)**| Model training, preprocessing: `pandas`, `numpy`, `scikit-learn`     |
| **MicroPython**| Edge inference on Pico: matrix ops, manual activations               |
| **ESP32 FW**   | MQTT listener, GPIO toggle for pump relay                            |
| **Support Tools**| Thonny IDE, `umqtt.simple`, Jupyter for model export               |

---

### Results

#### ET₀ Prediction Accuracy
- **R² ≈ 0.97**
- **MSE ≈ 0.10 mm²/day²**

#### Model Efficiency
- Original model: **~18 KB**
- Pruned for deployment: **~12 KB**
- Inference time on Pico: **≤ 50 ms**
- Fits within Pico W's **RAM/flash constraints**

---

### Challenges and Mitigations

#### 1. Integrating Multiple Sensors
- **Challenge**: I/O and bandwidth limitations
- **Mitigation**: Multiple ESP32s; Wi-Fi aggregation

#### 2. Sensor Accuracy Drift
- **Challenge**: Drift due to temperature or low-cost hardware
- **Mitigation**:
  - Use temperature-compensated sensors
  - Periodic recalibration
  - Firmware-level smoothing (moving average)

#### 3. Resource Constraints (Pico W)
- **Challenge**: Limited flash/RAM
- **Mitigation**:
  - Prune and quantize model
  - Manual implementation of inference logic

---

### Conclusion

This project presents a complete **Edge AI-based irrigation system** for nursery crops:

- Leverages long-term **climate data** and on-device **MLP** for accurate **ET₀ prediction**
- Integrates **soil feedback** for optimal irrigation
- Achieves **~97% accuracy** against FAO-56 benchmarks
- Fully **cloud-independent** and runs on **low-cost hardware**
- Successfully combines hardware and AI into a working prototype

### Future Directions:
- Add user interface (LCD/app)
- Extend to more crop types via ensemble models
- Integrate additional environmental sensors
- Modular, open-source design supports replication and customization

---

### References

- **Allen, R. G., et al. (1998)**: *FAO-56 Penman–Monteith Method*  
  _Crop evapotranspiration: FAO Irrigation and Drainage Paper 56_

- **NASA POWER API**: [NASA POWER Documentation](https://power.larc.nasa.gov/docs/)

- **Pedregosa, F., et al. (2011)**: *Scikit-learn: Machine Learning in Python*  
  _JMLR 12, 2825–2830_

- **Onion Crop Coefficients (Kc)**: Allen et al., 1989  
  _Agronomy Journal, 81(4), 650–662_

- **MicroPython on Raspberry Pi Pico**: Monk, S. (2019), *The MagPi Magazine*

- **ESP32 Datasheet**: Espressif Systems (2021)

- **Irrigation Scheduling**: Jones, H. G. (2004)  
  _Journal of Experimental Botany, 55(407), 2427–2436_

- **Wireless Sensor Networks**: Akyildiz, I. F., et al. (2002)  
  _Computer Networks, 38(4), 393–422_

- **Project Repository**:  
  [AYRUS06 / Edge AI Based Precision Irrigation (GitHub)](https://github.com/AYRUS06/Edge_AI_based_precision_irrigatio)

