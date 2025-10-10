---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

## Smart Waste Segregation using Arduino BLE and Edge AI

### Introduction

Waste segregation plays a crucial role in improving recycling efficiency and reducing environmental impact. Traditional methods of waste sorting are labor-intensive, slow, and inefficient. With the global increase in waste generation, the need for automated, efficient waste segregation has become critical. 

This project aims to address the problem of manual waste sorting by developing an **Edge AI system** that automatically classifies and segregates waste materials. Using an **Arduino Nano 33 BLE Sense Lite** device and the **OV7675 camera**, the system aims to improve recycling rates, reduce landfill waste, and promote sustainability.

The world’s waste problem is escalating, with over **2 billion tons** of solid waste generated annually. Most of this waste ends up in mixed bins, making recycling and waste management a challenge. 

The lack of an efficient system to automatically segregate waste has led to the reliance on manual sorting, which is:

- Costly
- Slow
- Often inaccurate

This inefficiency results in recyclable materials being discarded, contributing further to environmental degradation.

### Project Motivation

The motivation for this project is to **leverage Edge AI and machine learning** to develop an automatic waste segregation system that can classify and separate waste types such as:

- Cardboard
- Plastic
- Wet waste

This helps enhance recycling processes, reduce waste sent to landfills, and support a **circular economy**.

---

### Challenges with BLE and OV7675 Camera

Using the Arduino Nano 33 BLE Sense Lite and the OV7675 camera presented several technical limitations that impacted the system's performance and deployment feasibility.

#### A. Low Camera Resolution

The **OV7675 camera** has a resolution of **640x480 pixels**, which is relatively low. This affects:

- Fine-grained image classification
- Object detail visibility

**Solution:**
- Used image preprocessing
- Downsampled images to **64x64 pixels**

#### B. Limited RAM and ROM

The **Arduino Nano 33 BLE Sense** has:

- **1 MB flash memory**
- **256 kB RAM**

These constraints made it difficult to deploy a large image classification model.

**Solution:**
- Reduced the number of classes from six to **three**: cardboard, plastic, wet waste
- This allowed the model to fit into the limited memory with minimal accuracy loss

#### C. BLE’s Limited Processing Power

Although the BLE device uses a **32-bit ARM Cortex-M4** processor, it is not optimized for computationally intensive tasks like real-time image classification.

**Solution:**
- Used the **EON compiler** to optimize the model
- Chose **quantized (int8)** version of the model
- Resulted in:
  - **18% reduction** in RAM usage
  - **15% reduction** in ROM usage

<!-- > _Fig. 1. EON compiler configuration for model quantization (int8)_

--- -->

### Methodology 

#### A. Hardware Required

| Component                 | Specifications                                                                 |
|---------------------------|---------------------------------------------------------------------------------|
| Arduino Nano 33 BLE Sense | 32-bit ARM Cortex-M4, 1MB Flash, 256KB RAM, low-power microcontroller          |
| OV7675 Camera Module      | 640x480 resolution, low-cost, suitable for basic image capture                 |

#### B. Software Used

- **Edge Impulse Studio**: Model training and deployment
- **Arduino IDE**: Programming and flashing the board
- **Python**: Image preprocessing

#### C. Data Collection

- Captured **691 images** using a mobile phone over an A4 sheet
- Images manually labeled into 6 categories
- Performed **80-20 train-test split**
- Uploaded dataset using **Edge Impulse's image data uploader**

#### D. Model Development and Compression

- Enabled **data augmentation**
- Achieved:
  - **100% training and validation accuracy**
  - **92% test accuracy**
- Used **EON compiler** with **int8 quantization**
- Deployed model as **Arduino library**
- Ran live inference using: `edge-impulse-run-impulse`


<!-- > _Fig. 2. Confusion Matrix shows perfect validation accuracy for all three classes_

> _Fig. 3. Edge Impulse Studio's transfer learning output features for waste classification_ -->

---

### PROTOTYPE AND DEMO

A prototype of the smart waste segregation system was developed by integrating:

- Arduino Nano BLE Sense
- Edge AI image classification model

#### Features:
- Autonomous waste classification
- Real-time inference
- Accurate identification of:
- Cardboard
- Plastic
- Wet waste

---

# Project Resources

- **GitHub Repository**: [SmartWasteSegregator](https://github.com/thanishnasir/SmartWasteSeginator)

<!-- > _Fig. 4. Feature output showing clear class clusters (cardboard, plastic, wet waste)_ -->

---

### Challenges and workarounds

| Challenge              | Description                                                                 | Solution                                                                                  |
|------------------------|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| **Data Variability**   | Lighting/background changes affected performance                           | Applied **data augmentation** to improve robustness                                       |
| **Memory Constraints** | BLE device memory limited large model deployment                           | Used **quantization (int8)** and **EON compiler**                                         |
| **Low Camera Quality** | OV7675’s resolution limited classification accuracy                         | Applied **image resizing** and **preprocessing** techniques                               |

#### Insights:

- Embedded ML development requires **optimization trade-offs**
- BLE-based inference is **possible but constrained**
- Importance of **tooling** like Edge Impulse and **model compression**
- Edge AI can make a **real-world impact** in sustainable technology

---

### References

1. Nasir, T., Sindhura, S., & Sathvik, M. (2025). *Smart Waste Segregation using Arduino BLE and Edge AI*. [Available Online](https://github.com/thanishnasir/SmartWasteSegregator/tree/main)

2. Edge Impulse, Inc. (2025). *Edge AI for Embedded Systems*. [Available Online](https://www.edgeimpulse.com/docs/)

3. Arduino. (2025). *Arduino Nano 33 BLE Sense*. [Available Online](https://www.arduino.cc/en/Guide/Nano33BLESense)

4. Fang, B., Yu, J., Chen, Z., et al. (2023). *Artificial intelligence for waste management in smart cities: a review*. _Environmental Chemistry Letters, 21_, 1959–1989. [DOI Link](https://doi.org/10.1007/s10311-023-01604-3)

5. Gayathri, B., et al. (2023). *Edge Computation Assisted Garbage Monitoring and Alerting System for a Smart City*. In _ICCCI 2023, Coimbatore, India_, pp. 1-4. [DOI: 10.1109/ICCCI56745.2023.10128268](https://doi.org/10.1109/ICCCI56745.2023.10128268)

