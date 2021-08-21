# ClearQuote_Assignment
This repository contains project by given ClearQuote as internship problem.

### Problem Statement:   
- Given a grocery store shelf image, detect all products present in the shelf image (detection only at product or no-product level)
- The assignment requires you to implement an Object Detector to detect the products present on the shelf.

### Description of Data:   
The dataset contains images of the different brands of products on the shelf. [Here's the dataset link](https://github.com/gulvarol/grocerydataset). Big thanks to [Gulvarol and et.al](https://github.com/gulvarol/grocerydataset/commits?author=gulvarol).  It contains 354 image of total 11 class out of which 0 is named as `other_class`.


Annotated csv contains the bounding box location of each product in the particular image.
```CSV file contains  
<image_name> <x_i> <y_i> <x_j> <y_j> <class of the product>
  where image_name:name of the image
        x_i: x-coordiante of the upper left corner of the boundng box.
        y_i: y-coordiante of the upper left corner of the boundng box.
        x_j: x-coordiante of the lower right corner of the boundng box.
        y_i: y-coordiante of the lower right corner of the boundng box.
        class: product class.
  ```
  
 Since it contains the upper left and lower right corner co-ordinates of the bounding box. But we want hight and width of the bounding box alongwith the x, y co-ordinate of the bounding box. So we can calculate respective co-oridinate difference which would be width and height respectively.  
 Save this refined file as csv to generate tfrecord. 
 
 ### Training:  
 To train the object detection model, used pretrained weigths of the [RetinaNet50](http://download.tensorflow.org/models/object_detection/tf2/20200711/ssd_resnet50_v1_fpn_640x640_coco17_tpu-8.tar.gz).
You can read more about RetinaNet [here.](https://arxiv.org/abs/1708.02002)  
In that particular paper, authors of the paper identifies `class imabalance` as the main obstacle which impedes the single stage detectors from achieving the state of the art accuracy. So, they propose a new loss as `FOCAL LOSS` which is dynamically scaled cross entropy loss.  
RetinaNet able to match speed of the SSD's while supassing the accuracy of all existing two stage detectors. 

At default setting of the hyperparameters it works well with minor chages in the `pipeline.config` file such as batch_size and number of classes `num_class`.
Trained it for 10000 epochs, and get training side loss with leariing rate:  
``` 
'Loss/total_loss': 0.16385211,
'learning_rate': 0.029201299`
 ```
 
 **Training Log on Tensorboard:**
 ![alt text](https://github.com/jajinkya/ClearQuote_Assignment/blob/main/Train_log.PNG)
 
 For test data:   
 
 ![alt text](https://github.com/jajinkya/ClearQuote_Assignment/blob/main/Evaluation.PNG)
 ```
 "map": 0.666, 
 "Precison": .713, 
 "Recall": .649
 
 ```
 **Testing Log:**
 
 ![alt_text](https://github.com/jajinkya/ClearQuote_Assignment/blob/main/evaluation_log.PNG)
 

**Inference on Some Images:**

![alt text](https://github.com/jajinkya/ClearQuote_Assignment/blob/main/img1.PNG)![alt text](https://github.com/jajinkya/ClearQuote_Assignment/blob/main/img2.PNG)


Cite:
```
@article{varol16a,
      TITLE = {{Toward Retail Product Recognition on Grocery Shelves}},
      AUTHOR = {Varol, G{"u}l and Kuzu, Ridvan S.},
      JOURNAL = {ICIVC},
      YEAR = {2014}}
```
