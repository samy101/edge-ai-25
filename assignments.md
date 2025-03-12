---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science
---

### Coding Assignments
--- 

- [Assignment #1: Sensor Data Collection with On-Board Feature Extraction](Assignment-1-Sensor-Data-Collection-with-On-Board-Feature-Extraction)


#### Assignment 1: Sensor Data Collection with On-Board Feature Extraction

![image](https://github.com/user-attachments/assets/823ffc1a-8175-460f-ac46-d7ca99bab464)



![imag](/assets/img/images1.jpg)

##### Background:

As you know, the Arduino Nano BLE Sense board includes a built-in LSM9DS1 IMU module, which features a 3D accelerometer, 3D gyroscope, and 3D magnetometer. These sensors measure linear acceleration, rotational velocity, and magnetic field to determine the device's orientation. Continuous measurements from these sensors can be used for various applications, including human activity detection, in realtime. However, raw IMU sensor data is often noisy and highly sensitive to small changes. Therefore, it is necessary to extract meaningful features over a moving time window before implementing machine learning models for real-time activity detection. 

- **Step 1: Write a MicroPython Script to Collect IMU Sensor Data**
  
Your script should:

  1. Continuously read and store data from all three channels of the accelerometer, gyroscope, and magnetometer into separate variables (e.g., `Ax, Ay, Az` for the accelerometer; Gx, Gy, Gz for the gyroscope; and Mx, My, Mz for the magnetometer).
Create a buffer (of size N=100) for each of the nine channels. Each buffer should retain only the most recent readings.

  2. Write MicroPython functions to extract at least 10 different time-series features (e.g., mean, min, max, standard deviation) for each of the nine channels from their respective buffers. Note that MicroPython does not provide the necessarily librararies for extracting the features using various mathematical or statistical functions. So, you may need to implement them in pure MicroPython from scratch.

  3.  Print the data (sequence number, buffer size, raw IMU data, and extracted features) to the terminal using UART. Use proper formatting and naming conventions. For example:


