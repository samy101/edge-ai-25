---
layout: post
title: Crosswalk Aid
subtitle: James Li, Pingyuan Liang, and Xuanye Li
# cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/crosswalk_aid_1.jpg
# share-img: /assets/img/path.jpg
tags: [spring_23]
---

The visually impaired encounter a number of difficulties when crossing streets. Without auditory information from parallel traffic, blind pedestrians can easily veer away from crosswalks. Complicated road junctions may also confuse a blind pedestrian’s ability to accurately determine the location of crosswalks. Last but not least, blind pedestrians are also inconvenienced by the fact that they always have to wait for the start of a pedestrian cycle to begin crossing to ensure they have enough time. These problems can be alleviated by dog guides and/or electronic aid, but these solutions are typically very expensive. As a result, we propose an alternative crosswalk aid solution which we will power using a Raspberry Pi and a RPi camera module. The crosswalk aid solution offers the follow functionality:
1. Device provides crosswalk detection and alert if the user has reached and is correctly orientated towards a crossing using a camera module. Crosswalk position is continuously labeled as the user crosses the crosswalk to provide feedback alerting if the user is on course and has not veered away from the crosswalk.  
    * Image classification  
    * Computer vision post-processing  
2. Device will provide pedestrian traffic light detection and alert the user if one is present.
The device will further relay the state of the pedestrian traffic light (go and stop)  
    * Object detection  
    * Computer vision post-processing  

Our proposed solutions excels in many ways outlined by the BLERP model. In terms of bandwidth, no wireless transmission will be used in our design which means that there would be huge power savings since wireless transmission takes up a lot of energy in low power embedded systems. This means a visually impaired person would be able to utilize our device without charging for a prolonged period, which would substantially increase convenience. The on-edge nature of our solution also enables a pedestrian to negate cloud latency. A second difference can mean that a pedestrian might still be on the crosswalk when cars start moving in a green light. The solution could be employed in poorer regions of the world where dog guides and electronic aid are harder to come by. Network failures will also not be a problem using this solution; users need not rely on something like an online map database to navigate city crosswalks. Finally, no data would be transmitted and saved remotely. This eliminates potential privacy concerns associated with the camera because a cloud provider would otherwise be able to track the exact whereabouts of the user.  
<p align="center"> <img src="/embed-dl-s23/assets/img/crosswalk_aid_2.jpg" width="100%" height="100%"> </p>
