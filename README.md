# person_car_detection

## (neural networks for object detection): YOLO V4



--------------------------------------------------------------------------

1. Model Name: YOLO V4
   Paper YOLO v4: https://arxiv.org/abs/2004.10934

2. Links to dataset and framework:

  Dataset provided by EagleView
  Frame work : I have used YOLOv4 and so have clone the github repository as below
  !git clone https://github.com/AlexeyAB/darknet.
   
  The model has been trained on google colab(Free GPU) for 4 hours. 

I have used YOLO because it is fast and also images are not very small. So it can be easily trained. 
The model has been trained on 699 datasets( not on full dataset) as trainig time is so huge. 


3. Data Preparation:
Annotate of the images are different compared to YOLO format. YOLO needs class and boundary boxes(center, Height and width) values.
So I have used "annotation_coco_to_yolo_format.ipynb" to bring the anootation format as per YOLO. 

Programing files used in data preparation:
i. annotation_coco_to_yolo_format.ipynb: To convert annotation to YOLO format
ii. process.py: This file generates train.txt and test.txt. Train and test txt files hold the information of location of our images and it cab be used during traing process.

4. Model:
I have used YOLOv4 pretrained model and fine tuned it for our custom dataset. 

In order to set up our Darknet environment we need these dependencies:

OpenCV
Cuda Toolkit
cuDNN
GPU resources
GPU Architecture

Goolge colab supports all the dependencies. 


I have created the following custom variables based on our dataset:

- num_classes
- max_batches 
- iteration steps
- layer filters

I have made following chages to configuration file:
i.Classes: 2
ii.Batch sizes: 64
iii. Image height and width: 416
iv. Number of filters: 21 (for 2 classes)
v: max_batches: 6000
vi  steps= 5400,4800

Model file:  
i. people_car.ipynb : For trainig and prediction
The model file is for taining our custom dataset and prediction.
ii. data.names: This file holds Class names(Person, car)
iii. data.data: This file required for trainging and holding model weights.  

5. Analysis:
chart_yolov4-custom.png files captures the loss during training process. Trainig was planned for 6000 iterations but it was terminated at 2200
iterations(5 hours). Aproximately 16 hours will take to complete 6000 iteration.  

From the chart, it is be observed that the loss is decreasing and definitely it will reach near to global minima for 6000 iteration. 

The following result summurised the model performance: 

class_id = 0, name = Person, ap = 59.11%  (TP = 92, FP = 82) 
class_id = 1, name = Car, ap = 58.12%   	 (TP = 55, FP = 44) 

precision = 0.54, recall = 0.60, F1-score = 0.57 
TP = 147, FP = 126, FN = 97, average IoU = 39.61 %

IoU threshold = 50 %, used Area-Under-Curve for each unique Recall 
mean average precision (mAP@0.50) = 0.586163, or 58.62 % 

6. Result and coionculsion:
On of the predictions.jpg is attched for your reference. The model is doing quite well even though it has trained for less time. From 
the image, it was cleared seen that model can able to localised the person and car with the class probabilty. 

It is concluded that the YOLOv4 can be used for this dataset and provides acurate result. The model can be trained for more time with image size 608X608 as larger
image size will provide more accuracy. However, RCNN model  may be tried to increase mAP and depends upon bussiness objective. 
