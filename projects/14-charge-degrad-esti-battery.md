---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

## Intelligent State of Charge (SoC) Estimation Using LSTM on Edge Devices

### Introduction

The primary objective of this project is to develop an intelligent system capable of estimating the **State of Charge (SoC)** of Lithium-ion batteries using **machine learning techniques**, specifically **Recurrent Neural Networks (RNN)** and **Long Short-Term Memory (LSTM)** models. The system works with real-time data from two types of batteries:

- **Li-ion NMC**
- **LiFePO₄**

This addresses the shortcomings of traditional SoC estimation methods (e.g., Coulomb counting), which suffer from drift and inaccuracies.

### Data Acquisition Hardware

A custom hardware circuit was built using the **Arduino Nano 33 BLE**, connected to sensors measuring:

- Voltage  
- Current  
- Temperature  
- Capacity  
- WhAccu  
- Previous SoC  
- SoC from Coulomb counting  

Data was collected during controlled charge/discharge cycles and used to train deep learning models.

### Edge Deployment

After training, the best-performing model (LSTM) was:

- **Quantized to float16**
- **Converted to TensorFlow Lite (.tflite)**
- **Compiled to C++ (.cc)** for deployment

The final model was **flashed onto the Arduino Nano 33 BLE**, enabling **real-time SoC predictions** using just voltage, current, and temperature.

This project demonstrates a **low-power, real-time, cloud-free Edge AI application** for battery management systems.

---

### Background and Motivation

Lithium-ion batteries are central to:

- Electric vehicles (EVs)
- Renewable energy storage
- Portable electronics

#### Challenge

A critical parameter in Battery Management Systems (BMS) is the **State of Charge (SoC)**. Traditional SoC estimation methods include:

- **Coulomb Counting**: Prone to cumulative error
- **Open-Circuit Voltage (OCV)**: Inaccurate under load
- **Model-based methods**: Require detailed electrochemical understanding

#### Motivation

With advances in **AI** and **Edge Computing**, more robust solutions are possible. RNNs and LSTMs are ideal for modeling **time-series data** like voltage, current, and temperature.

Our system is:

- Accurate and adaptive
- Based on simple measurements
- Deployed on embedded hardware (Arduino Nano 33 BLE)

It improves safety, reliability, and efficiency of battery-powered edge devices.

---

### Methodology

#### Hardware Used

| Component              | Description                                                  |
|------------------------|--------------------------------------------------------------|
| Arduino Nano 33 BLE    | Microcontroller with BLE and TensorFlow Lite support         |
| Li-ion 18650 Cell      | 3Ah rechargeable lithium-ion battery                         |
| LiFePO₄ Cell           | Rechargeable lithium iron phosphate battery                  |
| 10W Power Resistor     | For controlled battery discharge                             |
| 10kΩ Resistors         | Used in voltage divider for voltage scaling                  |
| DHT11 Sensor           | Measures ambient battery temperature                         |

---

#### Software Used

| Tool                          | Purpose                                                   |
|-------------------------------|-----------------------------------------------------------|
| Google Colab (Python)         | Model training and preprocessing                          |
| TensorFlow & Keras            | Model architecture and training                           |
| TensorFlow Lite Converter     | Conversion to .tflite format                              |
| Post-training Quantization    | Float16 model compression                                 |
| Arduino IDE                   | Code flashing and deployment                              |
| TFLite for Microcontrollers   | Edge inference engine                                     |

---

#### Data Collection Setup

- Voltage divider → Battery voltage
- Shunt resistor → Current (via Ohm's Law)
- DHT11 → Battery surface temperature
- Sampling interval: **100 ms**
- Total samples collected: **159,647**
- Discharge until ~3.2V

#### Recorded Features:

- Voltage  
- Current  
- Temperature  
- Capacity  
- Energy (Wh)  
- Coulomb-counted SoC (ground truth)

#### SoC Calculation Formula:

`SOC(t) = SOC(t-1) - (Current × Δt) / Battery Capacity`

Or simplified as:

`SOC(present) = SOC(previous) + (Current / 10800 × 10)`


---

### Model Development

#### Model Architectures Explored:

- **Recurrent Neural Network (RNN)**
- **Long Short-Term Memory (LSTM)** Best performer

#### LSTM Model Architecture

- **Two LSTM layers** (128 units each)
- **Dropout layers** (0.2) after each LSTM
- **Final Dense Layer**: 1 unit, linear activation

#### Training Configuration

- **Loss Function**: Mean Squared Error (MSE)
- **Optimizer**: Adam
- **Batch Size**: 64
- **Epochs**: 15
- **Early Stopping**: Patience = 5 epochs

### Results

- Training Loss: **2.26e-4**
- Validation Loss: **3.88e-4**
- Final Test Loss: **0.0025**

---

### Model Compression and Deployment

#### Conversion Pipeline:

1. **Keras → TensorFlow Lite (.tflite)**
2. **Quantization to float16**
3. **Converted to .cc (C array) using `xxd`**
4. **Flashed to Arduino Nano 33 BLE**

#### Edge Deployment

- Runs LSTM inference using **voltage, current, and temperature**
- Executes **entirely on-device**
- No need for cloud or external computation
- Output verified over **serial interface**

---

### Real-Time Laptop Telemetry Validation

As an extension, we tested SoC estimation using **laptop battery telemetry** collected via **HWiNFO64** over 2–4 hour sessions.

#### Collected Features (every 100ms):

- CPU / GPU / SSD temperatures
- Battery voltage, remaining capacity
- Power draw, wear level
- Estimated time, charge %

#### Processing & Modeling:

- Derived current & temperature proxy
- Smoothed, resampled, and scaled features
- Trained dense neural network with:
  - Regularization
  - Dropout
  - Batch normalization

#### Evaluation:

- Compared model predictions vs Coulomb Counting
- Metrics:
  - **Mean Absolute Error (MAE)**
  - **Root Mean Square Error (RMSE)**
- Visualizations confirmed that **neural network outperformed** traditional method

---

### Challenges and Workarounds

#### 1. Data Collection

- Issues with resistor overheating and circuit failures
- Required multiple redesigns of:
  - Voltage divider
  - Current sensing section
- Maintained high-resolution sampling over long cycles

#### 2. Model Deployment

- Original model too large for Nano BLE (float32)
- Applied **float16 quantization**
- Compatibility issues with TFLite model
- Required fine-tuning during `.cc` compilation

#### 3. Key Learnings

- **Model size optimization is critical** for Edge AI
- Hands-on experience in hardware-software integration
- Learned quantization trade-offs, memory management
- Valuable insight into deploying **AI on microcontrollers**

---

### Conclusion

This project successfully demonstrates a complete pipeline for **Edge AI-based State of Charge estimation**:

- Trained LSTM model using real battery data
- Achieved high accuracy and generalization
- Compressed and deployed on **Arduino Nano 33 BLE**
- Validated on both physical batteries and laptop telemetry

It serves as a **prototype for smart Battery Management Systems (BMS)** and can be extended to:

- Predict **battery cycle life**
- Monitor **health degradation**
- Improve safety in **IoT and EV applications**

---