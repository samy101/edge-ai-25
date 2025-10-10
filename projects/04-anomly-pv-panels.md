---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

## Anomly Detection in PV Panel

### Objective
The goal of this project is to create an AI-based system that can identify irregularities in photovoltaic panels, which is essential for improving the efficiency of solar power generation, lowering maintenance costs, and guaranteeing long-term performance. In large-scale solar farms, where manual inspection is time-consuming and unfeasible. Hence, automated inspection systems are essential due to the growing worldwide push toward renewable energy sources, notably solar.

### Types of Anomalies considered 
- Clean
- Dust
- Organic Matter (bird droppings, leaves)
- Cracks
- Decolourisation

### Hardware and Software Used
- PV Panels
- Nicla Vision
- OpenMV
- Edge Impulse
- Google Colab

### Data Collected
- **Image Resolution:** 256 x 256 pixels  
- **Manually Collected Dataset:** 2500 images  
- **Open-source Data:** 500 images  
- **Data After Cleaning:** 2000 images  
- **Data After Cleaning & Augmentation:** 3000 images  

> **Note:** Open-source data was used to obtain clean datasets and drone shots of the panels to improve model robustness and generalizability.

### Anomaly Categories (Post Augmentation)
1. **Clean:** 500  
2. **Dust:** 832  
3. **Organic Matter (bird droppings, leaves):** 855  
4. **Crack:** 312  
5. **Decolourised:** 500  

---

## Data Collection Process

- **Tools Used:** OpenMV and Nicla Vision  
- **Image Resolution:** 224 x 224 pixels  
- **Time Frame:** Morning and evening hours were selected to:
  - Prevent glare issues  
  - Capture images under varied lighting and angles

### Data Augmentation & Preprocessing Techniques
1. Resizing to normalize input dimensions for model training  
2. Rotation and tilting to replicate changes in camera angle  
3. Cropping to highlight damaged or important areas  
4. Flipping and brightness variation to address illumination differences  
5. Horizontal and vertical shifting

---

## Annotation Type
- Manual class labeling was performed using **Edge Impulse**, based on the type of anomaly observed in the image.

---

### Challenges

#### During Data Collection
- **Accessibility Issues:** Some PV panels were located on rooftops or restricted-access areas  
- **Limited Time Frame:** Data collection was restricted to early morning and late evening due to heat and glare  
- **Lighting & Perspective:** Capturing consistent lighting and angles was difficult  
- **Multiple Anomalies:** Some samples had more than one anomaly, complicating classification  
- **Crack Detection:** Difficult to find visible cracks; many were too small to detect visually or using Nicla Vision

#### During Data Labelling & Model Training
- Annotating augmented images manually and ensuring consistent labeling was tedious  
- Difficulty in selecting the optimal model for training  
- **Model Quantization:** The biggest challenge was compressing the model to fit within space constraints while maintaining good accuracy

### Results:
**Best model performance:**

- Accuracy: TinyCnn - 93% (on validation set) : MobileNet V2 0.35 - ~85% through Edge Impulse
- Deployment model size: MobileNet V2 0.35 - ~40 KB (via Edge Impulse) : ResNet8 - ~50kB (quantized tflite model)
- Inference time: ~100 ms on Nicla Vision