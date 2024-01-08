---
layout: post
title: Parking Detection with TinyML
subtitle: Nathan Litzinger, Saurabh Roychowdhury, and Saumya Bhandarkar 
# cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/license_plate_6.jpg
# share-img: /assets/img/path.jpg
tags: [fall_23]
---
Paying for parking is still a hassle in 2023. Whether in a garage or on the street, there is no single, low-cost, ubiquitous system that can be deployed everywhere. Therefore, we set out to create a low-cost, automated parking detection system grounded in embedded deep learning. We propose a two-part system wherein a microcontroller-based ”meter” uses a deep neural network to detect when a parked car’s license plate is visible, and then sends a picture of the plate to a second, more powerful ”hub” device (on par with a smartphone) that will run a robust deep neural network to extract the license plate number from the captured plate image. This plate number can then be used to lookup a user and automatically charge them for parking.  

Our system runs Edge Impulse’s FOMO object detection model [3] to detect license plates on a Seeed XIAO ESP32S3 Sense microcontroller serving as the meter. The resulting model achieved an F1 score of 68.0%, occupied approximately 240KB of memory, and took only 140ms to run. The hub device runs EasyOCR [4] to extract plate numbers from the plate images sent from the meter. While this model is supposed to be more robust, it performed very poorly on many straightforward plate images.  

Despite performance issues with our chosen Optical Charac- ter Recognition (OCR) model, the overall pipeline successfully demonstrates the viability of the proposed low-cost system as both an improved parking payment system and a more efficient parking enforcement system.  

# Introduction  

Parking infrastructure is remarkably inadequate. Street park- ing, garage/permit-based parking, and parking enforcement infrastructure alike are wildly behind in the technology they utilize and the interface they provide to end-users as a result.  

# The Problem  

In 2023, it is still necessary to tote around a handful of different apps on your smartphone to pay for street parking, depending on where you find yourself. Even when you do have the right app, in many cases, you have to continue to manually ”reload” the meter every so many hours or risk getting a ticket.  
For permitted parking, you still often have to swipe a physical key or card of some sort to admit you access to the garage/lot. In city garages used for events by visitors, similar infrastructure is used, but requires the user to manually pay their ticket at a physical kiosk or with a credit card before departing. This then only adds to the congestion in parking garages when troves of people all try to leave at the same time.  

Additionally, for businesses, universities, and municipalities, parking enforcement is still a manual process. Without modern technology, these entities are left employing someone to man- ually walk around and ticket vehicles that are illegally parked. More recent methods involve driving around a vehicle outfitted with cameras to identify unregistered/illegally parked vehicles according to their vehicle type and plate number. While this is certainly an improvement over traditional ”on-foot” methods, it still requires an employee to spend their time driving all over creation and can not be used to enforce parking laws in real time in every location. While you can scale this solution up, it requires more drivers, more specially equipped vehicles–and therefore a whole lot more money.

# Our Solution
With the rise in popularity of deep learning based computer vision in the last decade, Automatic License Plate Recognition (ALPR) has become more practically feasible than ever before, as demonstrated in papers like [17], [7], and [11]. Also a product of growing research dedicated to ALPR is the increasingly large number of datasets available like [16], [12], and [6] available to train the networks that make up ALPR systems.  

However, advances in deep learning and computer vision alone are not enough to (realistically) solve this problem. In order for a municipality, business, landlord, or university to adopt any technological solution, it must be affordable and scalable–as well as (hopefully) solve more problems than it creates.  

To solve this problem in a scalable and economical way, we propose a system that, for a particular parking lot or street, is composed of a distributed network of camera-equipped microncotrollers called meters and a single, more powerful central device called a hub. Each meter is a solar-charged, battery-powered, low-cost microcontroller capable of detecting when a vehicle has parked in front of it and detecting a license plate in its view of the vehicle. Each meter is connected to the hub via a wireless network protocol like WiFi or LoRa. A meter sends any detected license plate images to the central hub device, where the hub is capable of running a robust and reliable OCR model like [13] to extract the plate number from the image. This plate number can then be used to charge a user identified by their vehicle’s plate number, or to issue a citation for a non-registered plate number, for example. Fig. 1 depicts how the components of the system work together in the street parking payment scenario, as an example.  

This paper focuses on a primitive implementation of the proposed system that we create to demonstrate the viability of such a system. Specifically, we first discuss the motivation behind the system architecture. We then examine the design, training, and deployment of the deep learning model that runs on the microcontroller-based meter devices. Additionally, we briefly examine the construction of hub device’s software prototype, as well as other hardware considerations for the system.

<p align="center"> <img src="/mbed_dl/assets/img/license_plate_1.jpg" width="90%" height="90%"> </p>
<p align="center"> <img src="/mbed_dl/assets/img/license_plate_2.jpg" width="90%" height="90%"> </p>
<p align="center"> <img src="/mbed_dl/assets/img/license_plate_3.jpg" width="90%" height="90%"> </p>
<p align="center"> <img src="/mbed_dl/assets/img/license_plate_4.jpg" width="90%" height="90%"> </p>
<p align="center"> <img src="/mbed_dl/assets/img/license_plate_5.jpg" width="90%" height="90%"> </p>
<p align="center"> <img src="/mbed_dl/assets/img/license_plate_6.jpg" width="90%" height="90%"> </p>  

# For more information, please contact the authors:    
* nlitzing@andrew.cmu.edu  
* sroycho2@andrew.cmu.edu  
* ssbhanda@andrew.cmu.edu  