---
layout: post
title: Inventory Management on Edge (Empty Shelf Percentage Estimator)
subtitle: Netra Trivedi, Rishi Pachipulusu, and Cathy Tungyun
# cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/inventory_management_1.jpg
# share-img: /assets/img/path.jpg
tags: [spring_23]
---

In a warehouse or a retail setup: Given a frame of reference, our model indicates the percentage of empty spaces with reference to a shelf full of boxes (either rectangular or square) for new inventory. 

Our dataset consists of 221 images that we have collected with each image having the label of its % empty space used for regression. Using the labeling program that we have made, it simplifies the process of labeling through the following features:
1. Keeps the box width constant
2. Allows us to draw multiple rectangles on the image
3. Returns the % area of empty spaces by dividing the total area of rectangles by the area of the shelf.
4. Renames the file to its labels for ease of import. (Also ensures that different images with the same label are not overwritten.)
<p align="center"> <img src="/embed-dl-s23/assets/img/inventory_management_2.jpg" width="100%" height="100%"> </p>
