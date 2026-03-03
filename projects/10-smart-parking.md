---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

## IntelliPark: Smart Parking Detection System using Nicla Vision

### Introduction

This project presents an edge-AI-based car detection system leveraging the Arduino Nicla Vision board and Edge Impulse Studio. The primary goal is real-time car detection using onboard image inference powered by TinyML models. The system is trained on a custom dataset with two classes: **car** and **unknown**. The models are optimized and deployed on the Nicla Vision board using OpenMV to enable live visual feedback.

As a secondary objective, the project also explores the **FOMO (Faster Objects, More Objects)** model for multi-object detection to detect car parking occupancy as a potential smart city application.


Urban congestion and inefficient parking management are persistent issues in many cities. Traditional parking systems, such as those based on CCTV and infrared sensors, are often expensive, power-hungry, and challenging to scale. A low-cost, energy-efficient, and scalable solution is required to overcome these limitations.

This project leverages **Edge AI** and **TinyML** to perform real-time, on-device car detection, with a focus on deploying models on the **Arduino Nicla Vision** board. By processing visual data locally, we reduce the need for cloud computing, thereby enhancing system responsiveness, data privacy, and energy efficiency.

- **Primary Objective:** Detect the presence of cars in a given frame using a lightweight image classification model.
- **Secondary Objective:** Explore car parking occupancy detection using the FOMO object detection model.

This secondary functionality demonstrates the potential of such systems in **smart city applications**, particularly for dynamic parking management.

<p align="center">
  <img src="../assets/img/projects25/10-smart-parking.png" 
       alt="Smart Parking Detection" 
       width="500"
       style="border-radius: 10px;">
</p>

### Methodology

#### Hardware Components

| Component       | Specification / Details |
|-----------------|--------------------------|
| Nicla Vision    | Arm Cortex-M7 @ 480MHz, 2MP OV7675 camera, onboard Wi-Fi and BLE, 16MB flash, 1.5MB RAM |
| USB Cable       | Used to power the Nicla Vision board and enable serial/data communication with PC |
| Laptop / PC     | Used for data collection, model training on Edge Impulse, and deploying firmware/scripts |

#### Software Tools

| Software            | Purpose |
|---------------------|---------|
| Edge Impulse Studio | Data collection, model training, and deployment of ML models for edge devices |
| Arduino IDE         | Flashing firmware and running basic scripts on the Nicla Vision board |
| Edge Impulse CLI    | Command-line interface for managing projects, uploading data, and downloading trained models |
| Python              | Serial communication and post-deployment data visualization or logging |
| OpenMV IDE          | Real-time visual debugging and deployment of TensorFlow Lite models on the Nicla Vision board |

---

### Data Collection

The dataset for car parking occupancy detection was built using the car detection model:

- **Custom Dataset:** Real-world images were captured using a mobile phone, representing two categories — `car` and `unknown`.
- **Synthetic and Online Data:** Supplemented with synthetic and public images from internet sources.

Images were uploaded to **Edge Impulse**, labeled, augmented, and split into training and test sets.

---

### Model Development and Compression

Two models were trained in **Edge Impulse**:

- **Binary Classifier:** Based on **MobileNetV2**, classifies `car` or `unknown`.
- **FOMO Model:** Localizes car positions within an image.

**Optimizations** included:

- **Quantization-Aware Training (QAT)**
- **EON Compiler**

---

### Model Deployment

The trained models were converted to **TensorFlow Lite** and deployed on the **Nicla Vision** board. MicroPython scripts enabled:

- Frame capture from the onboard camera.
- Inference using the TFLite model.
- Real-time display of detection results.

---

### Prototype and Demo

#### Setup

- **Mounting:** Board fixed on tripod/custom frame.
- **Power:** Supplied via USB.
- **Connection:** Serial communication through OpenMV IDE.

#### Real-Time Detection

The board:

- Captured grayscale images.
- Resized to 96x96.
- Performed inference.
- Overlaid label results on live feed.

- **FOMO** enabled multi-object detection.
- **Binary Classifier** indicated slot status.

---

### Results

- Achieved approximately **2 FPS** using the trained `.tflite` model on OpenMV hardware with a **240x240** image window.
- Image classification and FOMO provided bounding box visualizations.
- OpenMV IDE helped visualize annotated results in real-time.

---

### Challenges and Workarounds

#### Challenges

- **Limited Resources:** Required lightweight models.
- **Data Diversity:** Diverse data collection was time-consuming.
- **Camera Limitations:** Low image quality in varying lighting.
- **Deployment:** Flashing and debugging had a steep learning curve.

#### Workarounds

- Used **MobileNetV2** and **FOMO** with **QAT**.
- Applied augmentation to simulate diverse environments.
- Tuned exposure and gain settings manually.
- Relied on **OpenMV IDE** for deployment debugging.

---

### Project Resources

- **Hardware:** Arduino Nicla Vision, USB cable, tripod.
- **Software:** Edge Impulse Studio, OpenMV IDE, Arduino IDE.
- **Links:** Project dashboard, scripts, and videos (to be added).

---

### References

- [Edge Impulse](https://edgeimpulse.com/)
- [OpenMV IDE](https://openmv.io/)
- [Arduino Nicla Vision Docs](https://docs.arduino.cc/hardware/nicla-vision)
- [PKLot Dataset](https://web.inf.ufpr.br/vri/databases/parking-lot-database/)
- [Hackster Tutorial](https://www.hackster.io/mjrobot/tinyml-made-easy-object-detection-with-nicla-vision-407ddd)

