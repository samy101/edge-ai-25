---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science
---

## Coding Assignments
--- 

➤ [Assignment 1: Sensor Data Collection with On-Board Feature Extraction](#assignment-1-sensor-data-collection-with-on-board-feature-extraction)

➤ [Assignment 2: End-to-end Development of an Activity Detection app](#assignment-2-end-to-end-development-of-an-activity-detection-app)

---

### Assignment 1: Sensor Data Collection with On-Board Feature Extraction

#### Background:

As you know, the Arduino Nano BLE Sense board includes a built-in `LSM9DS1` IMU module, which features a `3D accelerometer, 3D gyroscope, and 3D magnetometer`. These sensors measure linear acceleration, rotational velocity, and magnetic field to determine the device's orientation. Continuous measurements from these sensors can be used for various applications, including human activity detection, in realtime. However, raw IMU sensor data is often noisy and highly sensitive to small changes. Therefore, it is necessary to extract meaningful features over a moving time window before implementing machine learning models for real-time activity detection. 

![image](https://github.com/user-attachments/assets/57a8207d-21fe-473e-8221-ba64467826de)

Source: [image link](https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.researchgate.net%2Ffigure%2FExample-of-acceleration-data-from-IMU_fig5_350865965&psig=AOvVaw2vZSvhx0Gr_Cf1he2RPirh&ust=1741949316946000&source=images&cd=vfe&opi=89978449&ved=0CBUQjRxqFwoTCMiPj_LxhowDFQAAAAAdAAAAABAg)

#### Assignment Objective:

In this assignment, you will develop an end-to-end sensor data collection application with on-board feature extraction for activity detection, collect samples for various activities, and gain an understanding of the challenges involved in real-world sensor data collection.

#### Assignment Steps:

This assignment involves completing the following three steps: 

**Step 1: Write a MicroPython Script to Collect IMU Sensor Data**
  
Your script should:

  1. Continuously read and store data from all three channels of the accelerometer, gyroscope, and magnetometer into separate variables (e.g., `Ax, Ay, Az` for the accelerometer; `Gx, Gy, Gz` for the gyroscope; and `Mx, My, Mz` for the magnetometer).
  2. Create a buffer (size `N=100`) for each of the nine channels. Each buffer should retain only the most recent readings.
  3. Write MicroPython functions to extract at least 10 different time-series features (e.g., mean, min, max, standard deviation) for each of the nine channels from their respective buffers. Note that MicroPython does not provide the necessary libraries for extracting the features using various mathematical or statistical functions. So, you may need to implement them in pure MicroPython from scratch.
  4. Print the data (sequence number, buffer size, raw IMU data, and extracted features) to the terminal using UART. Use proper formatting and naming conventions.
**For example:**

`Seq:0 N:100 Ax:0.03 Ay:-0.01 Az:0.99 Gx:0.12 Gy:0.73 Gz:-1.77 Mx:-12.74 My:52.00 Mz:1.11 Ax_mean:0.45 Ax_min:0.45 Ax_max:0.45 ... Gx_mean:0.12 Gx_min:0.73 Gx_max:-1.77 ... Mx_mean:-12.74 Mx_min:52.00 Mx_max:1.11`

The sequence number should be unique and increment with each iteration.

**Step 2: Write a Python Script for Data Collection**

Develop a Python script that runs on your computer/laptop to:

  1. Read sensor data from the Nano 33 BLE Sense board via a serial interface (e.g., a COM port on Windows).
  2. Parse the data received from the board and store it in a `.CSV file`.
 
A sample code will be provided, but you need to modify it to suit your data collection needs.

**Optional:** 

Develop a simple real-time sensor data visualization application using [Streamlit](https://streamlit.io/)

**Step 3: Collect IMU Sensor Data for Multiple Activities**

Using the setup above, collect IMU sensor data and features for at least **three different activities** (e.g., `walking, running, etc.`).

  1. Collect a minimum of 5,000 samples for each activity.
  2. Save the data for each activity in separate `.CSV` files.

#### Submission Format:

Your final submission should include:

  1. MicroPython Code: For reading IMU sensor data and performing on-board feature extraction `(4 marks)`.
  2. Python Code: For reading sensor data from the Nano 33 BLE Sense board `(1 mark)`.
  3. Activity Data: Separate `.CSV` files for each activity, containing at least 5,000 samples per activity `(3 marks)`.
  4. Write-Up: A text file with a brief summary of lessons learned, such as `(2 marks)`:

      1. How many samples were you able to collect per second?
      2. What changes would you make to your code to increase the sampling rate?
      3. What challenges did you encounter while collecting real-world data using IMU sensors?
      4. Any other insights or observations?

#### Submission deadline:

This assignment is due on Thursday, February 6, at 11:59 PM. Late submissions will be accepted until Saturday, February 8, at 11:59 PM. Please note that these deadlines are firm, and no extensions will be granted!


#### References:

  1. 9-Axis IMU - [Youtube-link](https://www.youtube.com/watch?v=2AO_Gmh5K3Q) 
  2. Activity Recognition Experiment Using Smartphone Sensors - [website-link](https://www.youtube.com/watch?v=XOEN9W05_4A)
  3. Awesome-IMU-Sensing - [github-link](https://github.com/rh20624/Awesome-IMU-Sensing)
  4. Awesome Human Activity Recognition - [github-link](https://github.com/haoranD/Awesome-Human-Activity-Recognition)
  5. A Survey on Deep Learning for Human Activity Recognition - [website-link](https://dl.acm.org/doi/abs/10.1145/3472290)
  6. tsfresh features - [website-link](https://tsfresh.readthedocs.io/en/latest/text/list_of_features.html)
  7. tsfresh feature calculator code  - [github-link](https://github.com/blue-yonder/tsfresh/blob/main/tsfresh/feature_extraction/feature_calculators.py)
  8. MicroPython math library - [website-link](https://docs.micropython.org/en/latest/library/math.html)
  9. MicroPython statistics library - [github-link](https://github.com/rcolistete/MicroPython_Statistics/blob/master/statistics.py)
  10. pySerial library - [website-link](https://pyserial.readthedocs.io/en/latest/shortintro.html)

### Assignment 2: End-to-end Development of an Activity Detection app

#### Background:  

Smartwatches and fitness trackers have revolutionized the healthcare and fitness industry by enabling real-time monitoring of physical activities such as walking, jogging, and cycling. Have you ever wondered how these devices detect different activities in real time? They use built-in motion sensors, such as accelerometers and gyroscopes, to collect raw movement data, which is then processed by machine learning models running on the device to classify various activities in real time.

![alt text](/assets/img/Assignment_2_image.png "Flowchart of activity detection")

Source: [image link](https://github.com/andresquintanilla/fitbit-activity-recognition/tree/master)

#### Objective: 

In this assignment, you are required to implement an end-to-end activity detection system using the Arduino Nano BLE Sense board, which includes an onboard IMU sensor. You are required to collect sensor data for various common activities, implement an ML workflow for model development, including feature extraction, ML model training, hyperparameter tuning, and cross-validation, and finally deploy the ML model on the Arduino Nano BLE Sense and demonstrate the activity detection application. 

#### Assignment Steps: 

This assignment involves completing the following four steps:   

**Step 1: Data Collection `(2 marks)`**

  1. Collect 5,000 samples of continuous IMU sensor data (accelerometer, gyroscope, magnetometer) for at least five different activities. Activities can include idle, walking, running, jumping, stretching, writing, typing, etc. 

  2. Store the collected data in, appropriately named `.csv` files. e.g. `walking.csv`

  3. You may use the code from previous assignments or lab sessions. 

**Step 2: Activity Detection Model Development `(4 marks)`** 

  1. Create a Colab notebook to implement an ML workflow, including data preprocessing, exploratory analysis, feature engineering, model training, hyperparameter tuning, and cross-validation.
      1. Exploratory Data Analysis (EDA): Visualize and analyze sensor patterns across activities to identify the patterns.
      2. Feature Engineering: Extract at least 10 features, which can be either historical or statistical (using a sliding window approach similar to the first coding assignment)
      3. Model Selection: Train at least three ML models, such as `Decision Tree, Random Forest, or XGBRFClassifie`r that are supported by the `m2cgen` library.
      4. Model Optimization: Apply hyperparameter tuning and cross-validation techniques.
      5. Final Model Selection: Choose the best-performing model based on classification accuracy. The selected model must achieve at least 90% accuracy.

**Step 3: Model Deployment `(2 marks)`** 

  1. Convert the trained model into Python code using the m2cgen tool.
  2. Write a MicroPython script to deploy the selected model on the Arduino Nano BLE Sense board.
  3. Implement real-time inference by integrating feature extraction based on the selected features from model development.
  4. The detected activity should be continuously printed on the terminal. 

**Step 4: Demonstration `(2 marks)`** 

  1. Demonstrate the working of your activity detection application.
  2. Ensure that your application is robust and accurately classifies activities. If required, repeat the above steps.

#### Submission instructions:

You are required to submit the following files:
  1. Sensor Data Files: Separate files for each activity, containing 5,000 samples each. Append your full name as a suffix to the filename (e.g., `walking_anil_kumar.csv`).
  2. A Colab notebook (e.g., `activity_detection.ipynb`) implementing the ML workflow for model development.
  3. A MicroPython file (e.g., `predict.py`) for model deployment and real-time inference. Note that this file should contain the logic for feature extraction.
     
***Note that you are required to demonstrate your application during the next lab session or to the TAs before the final submission of this assignment. Failing to do so will result in zero mark, even if you have completed the other steps.***

#### References:

m2cgen - [github-link](https://github.com/BayesWitnesses/m2cgen)



