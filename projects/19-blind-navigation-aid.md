---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

## On-Device Object Recognition and Proximity Feedback for Blind Navigation Aids

### Introduction

This project presents a real-time assistive system for visually impaired users. By integrating lightweight on-device object classification with ultrasonic distance estimation, our prototype delivers context-aware voice alerts to guide users around obstacles. The solution is designed to be low-power, portable, and a proof-of-concept for integration into wearable smart glasses.

Traditional mobility aids like white canes are effective but offer limited spatial context. Emerging edge AI devices provide opportunities to enhance situational awareness. Our motivation was to combine vision-based object classification and real-time distance sensing in a unified prototype that visually impaired users could benefit from, using off-the-shelf, cost-effective hardware.

<p align="center">
  <img src="../assets/img/projects25/19-proximity-blind-nav.png" 
       alt="Blind Navigation Aid" 
       width="500"
       style="border-radius: 10px;">
</p>

### Methodology

**Hardware Used**

- **Arduino Nicla Vision**: Cortex-M7 @ 480 MHz, 2MB flash, 512KB RAM, onboard camera.  
- **Arduino Uno R3**: Microcontroller to read sensor data and forward it over Serial.  
- **HC-SR04 Ultrasonic Sensor**: Measures distance by sending and receiving echo pulses.

**Software Tools**

- **Edge Impulse Studio** – Data Collection, Training, Deployment  
- **Arduino IDE** – Firmware development and flashing  
- **Python** – `pyttsx3` for Text-to-Speech (TTS), `pyserial` for reading distance

### Data Collection

We created a dataset of 300 images divided into 3 classes:

- **Person** (100 images)  
- **Objects** (100 images)  
- **Walls** (100 images)

Images were captured in varying lighting conditions and preprocessed to size 96×96, later resized to 48×48 for deployment. Data augmentation was used during training to improve generalization.

### Model Development and Compression

We used **MobileNetV2** with transfer learning in Edge Impulse. The initial model (96×96, float32) failed due to Nicla’s 256KB RAM constraint. To overcome this:

- Images were resized to 48×48  
- Post-training quantization to **INT8** was applied

### Accuracy after Quantization:

- **Wall**: 100%  
- **Person & Objects**: 70%

After compression, the quantized model was successfully deployed to the Nicla Vision. The device performed real-time classification at **3 FPS**. Output was validated using the serial monitor in Edge Impulse runner.

### Prototype and Demo

#### Figure 1: Ultrasonic Sensor Connection with Arduino Uno R3

#### Distance Measurement

Initial trials with **Nano 33 BLE** failed due to voltage mismatch. We switched to **Arduino Uno R3**, which is compatible with the **5V logic** required by HC-SR04.

**Connections:**

- `Trig` → D2  
- `Echo` → D3  
- `VCC` → 5V  
- `GND` → GND

**Formula:**

Distance (cm) = Duration × 0.0343


#### Voice Feedback

A Python script on a host PC reads distance from Uno over serial and provides voice alerts using `pyttsx3`. Alerts are spoken when a **person or object is detected within configurable proximity thresholds**.

### Final System Architecture

We envisioned serial communication between Nicla and Uno, but this was skipped due to soldering limitations. Instead, the modules function independently:

- **Nicla Vision**: Classifies objects  
- **Uno R3**: Measures proximity and triggers alerts

### Figure 2: Ultrasonic Sensor with Uno R3 (rotated)  
### Figure 3: Nicla Vision Module

### Challenges and Workarounds

#### 1. Memory Limitations on Nicla Vision

The initial model (MobileNetV2 with 96×96 input and float32 weights) failed due to 256KB RAM constraint. We addressed this by:

- Downscaling images to 48×48  
- Applying INT8 quantization  

This enabled efficient on-device inference with minimal performance compromise.

#### 2. Voltage Compatibility with Nano 33 BLE

The **Nano 33 BLE** operates at 3.3V, while **HC-SR04** requires 5V. The Echo pin’s 5V output posed a risk. Although we considered using a voltage divider (1k–2k), soldering was challenging due to the small pads.  
**Workaround**: Switched to **Arduino Uno R3**, which supports 5V logic.

#### 3. Pin Accessibility and Soldering on Nicla Vision

Planned integration between Nicla Vision and Uno R3 for serial communication was dropped due to **castellated edge pins** making soldering unreliable. To avoid hardware damage, both systems were operated **independently**.

#### 4. Latency in Voice Feedback

Early testing showed delays in feedback due to slow serial polling and TTS rendering.  
**Optimizations** included:

- Reducing serial buffer size  
- Using threshold-based alerting  
- Minimizing Python script overhead for near real-time response

### Project Resources

- **GitHub Repository**: [link](https://github.com/Ganesh-g-29/EDGE_AI.git)  
- **Edge Impulse Project**: [link](https://studio.edgeimpulse.com/studio/680351)

### References

1. [link](https://mlsysbook.ai/contents/labs/arduino/nicla_vision/object_detection/object_detection.html)  
2. *Low-cost Obstacle Detector for Visually Impaired Using Ultrasonic Sensor* (2024). MJARET, 3(4). [link](https://doi.org/10.54228/xsa7mm61)  
3. *MCUNet: Tiny Deep Learning on IoT Devices*. [link](https://arxiv.org/abs/2007.10319)  
4. *TensorFlow Lite Micro*. [link](https://arxiv.org/abs/2010.08678)  

