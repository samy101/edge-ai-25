---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

## Feature Estimation and Object Identification

### Introduction

This report presents a project that explores a novel approach to feature estimation and object identification using **ultrasound and camera sensors on edge devices**. Leveraging the relationship between object shape and distance as a function of the scanning angle of the ultrasound sensor, the system identifies unique features of objects effectively, even in **dark or nighttime conditions** [1]. 

When integrated with a camera, the system achieves enhanced performance, even in **low-light environments** [2]. By employing **sensor fusion**, the system combines ultrasound and vision-based sensing to enable accurate object classification while optimizing computational and power efficiency. 

<p align="center">
  <img src="../assets/img/projects25/20-object-identification.png" 
       alt="Object Identification System" 
       width="500"
       style="border-radius: 10px;">
</p>

The hardware setup includes edge devices such as the **Arduino Nano BLE Sense** and **Nicla Vision**, complemented by **machine learning-based techniques**. This hybrid approach is specifically designed for edge devices, addressing the significant **resource constraints** inherent to such platforms.


**Radar/Sonar-Based Feature Extraction**

- Objects exhibit distinct return profiles based on their **shape, orientation, and location** relative to the sonar or radar system.
- By capturing these return profiles under varying conditions, a **machine learning (ML)** model can be trained to classify object types — for instance, different aircraft models.
- The novel approach leverages **variations in sonar signatures** to enable reliable object recognition.

> **Fig. 1:** Return Signal profile for objects of different shape

Unlike optical systems, **radar-based classification** operates effectively under all weather conditions and during both day and night.

---

### Methodology

#### Ultrasound Sensor for Distance Measurement

The **HC-SR04 Ultrasound Sensor** is utilized for measuring the distance of objects. Ultrasound waves are emitted, and the time taken for their return is used to calculate distance.

**Key Advantages**
- **Ambient Light Independence:** Functions effectively in both bright and dark environments.
- **Environmental Tolerance:** Resilient to dust and fog.
- **Cost Efficiency:** A low-cost alternative to other distance-measuring technologies.

#### Servo Motor for Angular Scanning

The ultrasound sensor is mounted on a **servo motor**, enabling angular scanning across a predefined range.

- **Angular Range:** Scans across multiple angles to generate a 2D object signature.
- **Distance-Angle Relationship:** Captures a **unique profile** for objects based on shape.

#### Vision Sensor for Enhanced Classification

To overcome the **limitations of ultrasound** (e.g., inability to distinguish same-shaped objects of different colors or textures), a **Nicla Vision** sensor is integrated.

- **Lightweight ML Model:** Runs on-device for efficient object classification.
- **Optimized Parameters:** Minimizes parameters for efficient edge deployment.

---

### Data Collection

#### **Ultrasound:**

- Captured unique distance-angle signatures for various objects (e.g., battery, talc container, can).
- Scanned objects at **multiple distances, angles, and orientations**.

> **Fig. 2:** Ultrasound Sensor and its working principle (top left), Integrated hardware system (bottom left), Distance profile vs. scanning angle (right)

#### **Camera:**

- The same objects were captured using the **Nicla Vision** under varying lighting conditions.
- Data used to train an ML model to ensure **robust performance** in diverse scenarios.

---

### Model Development and Compression

- **Signature Analysis:** ML models analyze distance vs. angle relationships.
- **Shape-Based Classification:** Initial classification relies on object **geometry**.

> **Fig. 3:** Training results for ML model over collected dataset

- Leveraged **Edge Impulse** to train and optimize the model.
- Deployed model as **8-bit quantized** version on Arduino-compatible hardware.

> **Fig. 4:** Accuracy and loss metrics from Edge Impulse training

Despite high accuracy for geometrically distinct objects, the system struggles to differentiate **objects with similar shapes** (e.g., cans of different brands).

To address this:

- Integrated **camera-based classification**.
- Employed **lightweight ML model** to detect color or texture.

> **Fig. 5:** Edge Impulse used to develop and quantize camera data model using **FOMO**.

**Sensor Fusion**

- Combines ultrasound and camera data for **enhanced classification**.
- Maintains **minimal computational overhead**.

---

### Model Deployment and Demo

Sensor fusion of **ultrasound** and **vision** data leads to:

- **Improved Accuracy:** Combines shape + texture features.
- **Efficient Resource Use:** Reduces overall model size and complexity.
- **Environmental Robustness:** Works well in **low-light** and **dusty** environments.

> **Fig. 6:** Ultrasound detects a "can" but **cannot distinguish** between Coke and Sprite.

**Vision Sensor-Based Model**

- **Lightweight & Edge-Optimized**
- Differentiates **similar-shaped but visually distinct** objects.
- **Complementary Role** to the ultrasound model.

> **Fig. 7:** Camera sensor output for same-shaped objects (Sprite vs Coca-Cola)

---

**Scalability with Advanced Sensors**

Though this system uses an ultrasound sensor, it is designed to support **higher-resolution sensors** in the future:

- **Enhanced Resolution:** Radar/LiDAR provide finer details.
- **Future-Proof Architecture:** Can integrate LiDAR or advanced radar in real-world applications.

---

### Challenges and Workarounds

- **Integration Challenge:** Difficulty in syncing data between ultrasound and Nicla Vision.
  - **Solution:** Used a **separate serial port** for reliable data exchange.

---

### Conclusion

This project demonstrates a successful **hybrid edge AI system** combining **ultrasound** and **vision sensors** for real-time object classification and distance estimation.

- The fusion approach addresses limitations of individual sensors.
- Designed specifically for **edge applications** with limited resources.
- Lays the foundation for **scalable and efficient sensor fusion solutions**.

---

### References

1. HC-SR04 Datasheet or technical paper discussing the sensor's features.  
2. Nicla Vision documentation or technical paper on its imaging capabilities.  
3. Edge Impulse documentation or relevant literature discussing edge-based ML deployment.  
4. *Edge Intelligence: Architectures, Challenges, and Applications*  
   - Dianlei Xu, Tong Li, Yong Li, Xiang Su, Sasu Tarkoma, Tao Jiang, Jon Crowcroft, Pan Hui

