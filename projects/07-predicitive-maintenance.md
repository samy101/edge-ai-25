---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

## Acoustic Based Predictive Maintenance

### Introduction

The main objective of this project is to develop an Edge AI-based anomaly detection and prediction system for a 3D printed air blower. The system is designed to monitor the operating conditions of the device, automatically identifying any anomalies or defects through the analysis of the sound produced during operation.

Predictive maintenance plays a crucial role in minimizing machine downtime and maintenance costs in smart manufacturing setups. Acoustic signals serve as a non-intrusive, low-cost, and efficient way to detect early signs of machine failure. The need for real-time, on-device (edge) fault detection drives the integration of Edge AI with acoustic analysis. Traditional cloud-based solutions often suffer from latency, bandwidth, and privacy concerns—Edge AI can help overcome these.

<p align="center">
  <img src="../assets/img/projects25/07-predictive-maintenance.png" 
       alt="Acoustic Predictive Maintenance" 
       width="500"
       style="border-radius: 10px;">
</p>

### Hardware and Software Requirements

**Hardware**
- Arduino Nano BLE Sense 33
- Themisto 12V 4000 RPM DC Motor – 2 Pieces
- 5 mm DC Jack – 1 male and 2 female
- AC to DC 12V adapter -1 piece
- 3D printer for 3D printed casing
- PLA filament
- Steel Screws, Iron blade

**Software**
- Arduino IDE
- Edge Impulse
- Audacity Application for Windows

### Design of Air-blower
To proceed with the development and demonstration of the project, a small-scale air blower was designed using CAD. The model was 3D printed to realistically simulate operating conditions. To enable its functionality, a DC motor was attached to the blower, providing the necessary rotational motion to generate airflow and the characteristic operating sounds required for anomaly detection analysis.

The Air-blower has three main parts:
- **Main Body:** The outside of the blower has a spiral shape, which is typical for fans. It has holes for easy attachment to the front cover lid.
- **Impeller(Rotor):** The rotor has curved blades arranged in a circle around a central hub. The blades are designed to push air toward the outlet, increasing pressure.
- **Lid:** This part close the main body and includes the air outlet duct. It has a circular opening that directs the air flow created by impeller. The cover also has poles for easy attachment.

### Defects Introduced-

Two types of defects were introduced after the CAD Modelling :
- One is something getting stuck inside the blower
- Other is removing some of the screws from the blower

# Data Preprocessing using Audacity

- Converted audio to **16kHz** from **48kHz** using the **Audacity** application.  
- **Audio duration per segment:** ~4.8 to 5.1 seconds  

**Fig. Data Preprocessing using Audacity**

---

### Methodology

#### Feature Extraction

**MFCC (Mel Frequency Cepstral Coefficients)** is used to represent the spectral content of audio signals. It captures key sound characteristics. In this project, **25 MFCC coefficients** are extracted per audio segment to reduce dimensionality while preserving relevant information.

**MFCC Parameters:**

- **Number of Coefficients:** 25  
- **Frame Length:** 0.02 s  
- **Frame Stride:** 0.02 s  
- **Filter Number:** 50  
- **FFT Length:** 512  
- **Normalization Window Size:** 101  
- **Low Frequency:** 20 Hz  
- **High Frequency:** 8000 Hz  
- **Pre-emphasis Coefficient:** 0.98  

**Windows and Segmentation:**

Audio data is divided into temporal windows for analysis. Each window has:

- **Frame Length:** 0.02 seconds  
- **Frame Stride:** 0.02 seconds  

This approach enables detailed temporal analysis by processing each segment individually.

**Training Set Information:**

- **Total Data:** 2h 38m 11s  
- **Classes:** 4 (Crowd Noise, Defect1, Defect2, Normal Mode)  
- **Training Windows:** 17,027  

---

### Model Development

- Model created in **Edge Impulse** using time-series data.  
- **Window Size:** 1000 ms  
- **Window Stride:** 500 ms  
- Feature Extraction: **MFCC**  
- Classification into four classes: **Crowd Noise, Defect1, Defect2, Normal Mode**

### Neural Network Architecture:

- Input: 1,250 MFCC features  
- Layers:
  - Reshape layer  
  - 2× 2D Convolutional layers (with increasing filter sizes)  
  - Flatten layer  
  - Dense (Fully Connected) layer  
  - Output layer (4-class classification)

This architecture extracts and analyzes audio features for real-time classification of blower operating conditions.

**Training Parameters:**

- **Epochs:** 30  
- **Learning Rate:** 0.0005  
- **Processor Used:** CPU  

> Deployment-ready using **Arduino IDE** and **Edge Impulse Arduino Library**, allowing execution without a terminal — just with a power supply.

---

### Model Compression

- **Quantization:** Float32 → Int8  
- **Purpose:** Reduce model size and boost performance with minimal accuracy loss

**Model Size:**

- **Before (float32):** ~383.3 KB  
- **After (int8):** ~121.1 KB  
- **Compression Ratio:** ~3.16×

**Performance Gains:**

- **Latency:** ↓ 2563 ms → 350 ms (7.3× faster)  
- **RAM Usage:** ↓ by >72%  
- **Flash Usage:** ↓ by ~68%  
- **Accuracy:** ↑ from **99.64%** → **99.71%**

---

### Model Deployment

Model was deployed in two ways:

1. **Direct Flashing** on Arduino Nano BLE Sense 33 using Edge Impulse  
2. **Arduino Library Integration**:  
   - Model runs from power supply (e.g., power bank)  
   - **LED Blinking** used to display predicted class (no terminal needed)

<!-- --- -->

<!-- ## Result

### Result on Training Data:
*To be inserted if available*

### Result on Testing Data:
*To be inserted if available* -->

<!-- --- -->

<!-- ## Prototype and Demo

- **Live Demo:** [Edge Impulse Studio Project](https://studio.edgeimpulse.com/studio/661135)  
- **Code Repository:** [GitHub - Acoustic Based Predictive Maintenance](https://github.com/Hrishi2921/Acoustic_based_Predictive_Maintenance.git)  
- **Demo Video:** [Google Drive Link](https://drive.google.com/file/d/1_4VNXr-3AqF0h8gI1namtyJOWFjnBIu6/view?usp=sharing) -->

---

## Challenges and Workarounds

### Challenge 1: CAD Modeling

- **Issue:** Required extensive calculations and manual design.
- **Solution:** Studied online prebuilt designs to visualize and implement custom models.

### Challenge 2: Low Accuracy with Default Neural Network

- **Issue:** Predefined architecture gave only ~75% accuracy.
- **Tried:** Switched to **MFE**, worked during training but failed during prediction.  
- **Solution:** Designed custom neural network layers after MFCC extraction.
- **Outcome:** Achieved **~99.4% accuracy** after 4 training iterations.

### Challenge 3: LED Control via Arduino IDE

- **Issue:** New to Arduino-based LED indication.
- **Solution:** Learned and used Arduino libraries to define custom functions.  
- **Outcome:** Enabled execution from power bank without terminal, improving portability.

---


