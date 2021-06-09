# YOLO_like_detector

## Project description
The goal of this project is to perform multi object detection and localization in COCO images using an approach similar to YOLO that will be described below. We will be working with bus, car, and truck as our 3 classes of interest. We only select images that have a maximum 5 instances of these objects and contain at least 2 of these classes or all 3 of them. The selected images are then resized to 128x128, and all the corresposnding annotations are modified accordingly. <br>

## Training
The YOLO detector is a regression-based network, i.e. it does both detection and localization of objects in the image based on some regression-based metrics. The training function in which the network is trained has many differences with the ones for single object purposes. We first descritize the image using a grid of 36 (6x6) cells. Our next goal is to assign an achor box to each of the object instances based on its aspect ratio. To this end, we assume 5 different anchor boxes with aspect ratios of 1/5, 1/3, 1, 3, and 5, and assign the anchor box that has the closest value to the aspect ratio of each object. For each anchor box, we assume a vector with 8 elements (YOLO vector) of all zeros initially. The last 3 elements denote the class of the object the assined anchor box refers to in a one-hot encoding manner. The first element of this vector would be 1 for the assigned anchor box. Consequently, there will be a total of 36x5 of these 8-element vectors. After reshaping row wise, we get a gian vector with 1440 (36x5x8) elements, which we name the flattened YOLO tensor. The center of each object is determined based on which, we determine which cell it belongs to. We then find the difference between the object center and the center of its assinged cell in both x and y directions in terms of the cell dimensions and put them as the second and third elements of the YOLO vector whose first element is 1. Similarly, we replace the fourth and fifth elements of such YOLO vector with the true height and width of the object bounding box in terms of the cell dimensions. <br>

## Reference:
https://engineering.purdue.edu/kak/distDLS/

