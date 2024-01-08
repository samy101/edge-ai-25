---
layout: post
title: Speech Light Control System
subtitle: Aishwarya Joshi, Iris Dong, and  Sreekesh Devanathan
# cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/light_control_1.jpg
# share-img: /assets/img/path.jpg
tags: [fall_23]
---
For more information, please contact the authors:  
(aishwarj@andrew.cmu.edu)  
(ipdong@andrew.cmu.edu)  
(sdevanat@andrew.cmu.edu)  

Our main goal is to create a system which allows users to control light color and/or brightness through the use of speech commands. The commands would be preceded by a wake word, “nano”, to indicate that a command has been spoken. As for controlling the lights from the arduino, we initially plan to have an LED strip that will be able to light up in different colors and will wire directly to the Arduino board. We were able to achieve an overall training accuracy of 93.2% and testing accuracy of 89.6%, as well as an on-device inference time of 6ms with 3.8KB peak RAM usage.   

The core of the voice-controlled lighting system is the Arduino Nano 33 BLE Sense, which serves as the brain of the setup. It is responsible for processing spoken instructions and translating them into control signals for the lighting system. Connected seamlessly to the Arduino Nano 33 BLE Sense is an Arduino NeoPixel LED strip, adding a vibrant and dynamic visual component to the system. The LED strip has individually addressable WS2812 or SK6812 RGB LEDs, which allows users to control not only the brightness but also the color of the emitted light. This integration provides a customizable and aesthetically pleasing lighting experience, enhancing the user's ability to create different ambient settings.
The hardware setup includes a solderless power supply that ensures continuous operation and flexibility in placement. This power supply connects to a reliable 9V battery, offering portability and eliminating the need for a constant power source. The use of a battery not only enhances mobility but also ensures a consistent power supply in scenarios where conventional power outlets are unavailable. The comprehensive hardware configuration results in a compact, portable, and user-friendly voice-controlled lighting system. The synergy between the Arduino Nano 33 BLE Sense, MEMS microphone, NeoPixel LED strip, and battery power supply creates a seamless integration of hardware components, providing users with an immersive and convenient lighting control experience in various settings.  

In conclusion, the extended hardware setup of the voice-controlled lighting system is a well-designed and efficient configuration. The system's hardware components work cohesively to offer users a customizable and aesthetically pleasing lighting experience. The inclusion of a solderless power supply and battery power source enhances the system's portability and ensures continuous operation in various settings.  
<p align="center"> <img src="/mbed_dl/assets/img/light_control_1.jpg" width="100%" height="100%"> </p>
<p align="center"> <img src="/mbed_dl/assets/img/light_control_2.jpg" width="100%" height="100%"> </p>
<p align="center"> <img src="/mbed_dl/assets/img/light_control_3.jpg" width="100%" height="100%"> </p>
<p align="center"> <img src="/mbed_dl/assets/img/light_control_4.jpg" width="100%" height="100%"> </p>
<p align="center"> <img src="/mbed_dl/assets/img/light_control_5.jpg" width="100%" height="100%"> </p>
