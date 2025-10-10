---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

## Real Time Analog Meter Reader Using Edge Computing
---

### Introduction

This project mainly focuses on developing a solution to read analog gauge meter readings using **Arduino® Nicla Vision Camera**. We first trained a deep learning model to detect the key components of the analog meter (meter, max, min, centre, and pointer). By calculating the angles between these components, the system can determine the actual reading on the meter. The model is deployed on **Arduino® Nicla Vision**, demonstrating real-time detection and recognition of analog meters.

Analog meters are still widely used by various industries to check measurements such as pressure, temperature, voltage, etc. Reading these meters manually is time-consuming and prone to errors, especially in automated environments. The motivation behind this project is to automate this process using a camera-based system, which can increase efficiency and accuracy in various industrial applications. We aim to offer a solution that can read and interpret analog meter readings accurately.

---

### Methodology

#### Hardware and Software Required
- Arduino® Nicla Vision
- Analog Pressure Gauge
- Python
- **OpenMV IDE 4.4.7** – for deploying and running inference scripts on Nicla Vision  
- **Google Colab** – for experimenting with different models during exploration phase  
- **Edge Impulse Studio** – for model training and optimization  
- **EONTM Compiler** – for deploying the quantized model in a memory-efficient format  

---

#### Data Collection

- Captured **2700 images** from the pressure gauge under different camera and pointer positions.
- First dataset: **2000 images**, with 100 images each for different pointer positions.
- Second dataset: **700 images** captured using a fixed-height stand.
- Used a trained **YOLOv5** model to annotate collected images.
  - Trained using the **“Analog Meter Dataset”** [3].
  - Annotations were manually verified and corrected as needed.

---

#### Model Development and Compression

- Trained a **YOLOv5n** model on a high-quality dataset from Roboflow, with annotations for pointer, center, and value markers.
- Fine-tuned for **50 epochs** on a balanced dataset.
- Used this model to auto-annotate additional collected data.

##### Edge Device Challenges:
- Deployment on **Arduino Nicla Vision** (2MB Flash, 1MB RAM) was challenging.
- YOLOv5, even after quantization, was too large for the device.
- **NanoDet** was tested as a lighter alternative but had:
  - Complex post-processing
  - Manual tensor decoding issues

##### Final Solution: **Edge Impulse’s FOMO**
- **FOMO (Faster Objects, More Objects)** model selected due to:
  - Efficient real-time performance
  - Low memory footprint

##### Final Model Specs:
- **Model**: FOMO (MobileNetV2 0.35)
- **Training Platform**: Edge Impulse  
- **Quantization**: INT8 post-training  
- **Deployment Tool**: EON™ Compiler  
- **Final Model Size**: 56.8 kB  

> Edge Impulse provided seamless integration and accurate performance, making it the final choice.

- Trained for **60 epochs** with learning rate of **0.001** (on CPU)  
- Dataset split: **80% training**, **20% validation**  
- Used data augmentation during training

---

### Model Deployment

- Final **TFLite model** deployed using **OpenMV IDE** scripts
- Runs fully **on-device** using onboard camera
- Detects pointer, max, min, and center positions in real-time

### Custom Angle Detection Logic:
- Calculate angle between center-min and center-max lines → total angle
- For a given pointer position, calculate angle between center-min and center-pointer
- Ratio of pointer angle to total angle gives a percentage
- Multiply this ratio by (max reading - min reading) to get the **actual meter reading**

---

<!-- # Prototype and Demo

- The final prototype consists of:
  - **Nicla Vision** board mounted in front of the analog meter
  - On startup, it:
    - Captures video
    - Runs inference
    - Prints estimated meter reading

### Project Resources
- **Demo Video**: [Click here to view](https://indianinstituteofscience-my.sharepoint.com/:f:/g/personal/santoshgupta_iisc_ac_in/Erx3Bu6fPc1Fq8-3j7Erjw0BJZsOhZnUNRWNVvsgeZoNGA?e=Iy3Va7)

--- -->

### Challenges and Workarounds

- **Model Size**: YOLOv5n was too large, even in quantized form.
- **Conversion Issues**: TFLite version had unsupported ops and memory overflows.
- **Explored NanoDet**:
  - Good speed & size
  - Poor documentation
  - Complex tensor parsing needed
- **Thermal Issues**:
  - Nicla Vision experienced heating during continuous inference

**Final Workaround:**
- Migrated to **FOMO** from Edge Impulse
  - Anchorless object detection
  - Compatible with tinyML hardware
  - Easy deployment with Edge Impulse tools

> Additional exposure to TFLite, ONNX, and optimization for low-power MCUs gained during this process.

---

### References

1. **Object Detection using Nicla Vision**  
   [https://mlsysbook.ai/contents/labs/arduino/nicla_vision/object_detection/object_detection.html](https://mlsysbook.ai/contents/labs/arduino/nicla_vision/object_detection/object_detection.html)

2. **W. -J. Wang and P. D. Rosero-Montalvo**  
   "A Gauge Meter Reader Edge Device Based on Computer Vision and Deep Learning",  
   *IEEE Embedded Systems Letters*, doi: 10.1109/LES.2024.3507646

3. **H. Sayed**  
   "Analog meter Dataset", *Roboflow Universe*, Mar. 2024.  
   [https://universe.roboflow.com/hager-sayed-knqqb/analog-meter-dmoh4](https://universe.roboflow.com/hager-sayed-knqqb/analog-meter-dmoh4)

4. **L. Moreau**  
   "Introducing EON Compiler RAM-optimized", *Edge Impulse Blog*, Mar. 14, 2024.  
   [https://www.edgeimpulse.com/blog/introducing-eon-compile](https://www.edgeimpulse.com/blog/introducing-eon-compile)
