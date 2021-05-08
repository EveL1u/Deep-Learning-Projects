# Face Mask Detection
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/dkalantari/MMAI894MaskDetection/blob/main/Notebooks/894_Bremner_Mask_Detection_ScaledYOLOv4_Vfinal.ipynb)  


##### Face Mask Detection algorithm built in PyTorch using Transfer Learning from SOTA Scaled YOLOv4 model and Computer Vision concepts to detect mask or non-mask wearing in static images as well as in videos.
#
#
[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)    [![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)


## Introduction

The COVID-19 pandemic has had a drastic impact on our personal, professional, and social lives for more than one year in duration thus far. The global economy has gone through cycles of workplace shutdowns and has relied heavily on digital infrastructure to continue operating. Many day-to-day services such as shopping malls, hair salons, restaurants and retail stores are closed while leaving only essential services open. Despite substantial research to understand the virus and ways to battle it, the three main methods for the general public to slow the spread of the virus remain: wear face masks, wash hands often, and ultimately get vaccinated  (How to Protect Yourself & Others, 2021). While vaccination is the ultimate way to end this pandemic and return to normalcy, for now all top health organizations have requested the public to wear masks before and after being vaccinated to prevent putting others in danger.

Bremner Inc. was approached by several large private and public organizations such as shopping malls, airports and shared office space, to  develop a means for monitoring mask wearing compliance.  

## Business Solution 
Our team have come up with a solution that would provide the clients with a tool to monitor whether the employees and visitors on their premises are obliging with the COVID-19 protocols. Our solution involves training an object detection model on an image dataset consisting of individual faces which are annotated with labels “mask” and “no-mask” using bounding-boxes. Once the model is trained with the dataset to detect the individual faces in frames and classifying them as mask-wearing versus non-mask-wearing, it can be deployed either directly to hosted API or edge devices for real-life use. 

## Installation of Code

To run our code it is best to use the Google Colab resources as the training will require high GPU processing. Simply, clone this repo and upload to a Colab instance:

```sh
git clone https://github.com/dkalantari/MMAI894MaskDetection.git
```
Or for quick implementation, simply hit the 'Open in Colab' at the top of this page or link below, and once opened Colab make sure to Save a Copy in Drive:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/dkalantari/MMAI894MaskDetection/blob/main/Notebooks/894_Bremner_Mask_Detection_ScaledYOLOv4_Vfinal.ipynb)  
```sh
File ->  'Save a Copy in Drive'
Runtime -> 'Run All'
```




## Data Collection and Preprocessing
With the goal of mask detection in video frames, we knew our data should be made of two types of images: people who wear masks and people who did not wear masks. For our model to generalize to the appropriate backgrounds and demographics in real-life application, we decided to perform a strategic data collection containing a diverse set of people and locations. During a two weeks long collective efforts by everyone in the team, we finalized our dataset with 1,815 images made up of 3,751  “mask” labels and 6,148 “no-mask” labels. We then pre-processed the collected images including image augmentation to train the model. We repeated the process until a good performance is achieved.


## Modelling
Since we are only interested in the task of object-detection and not semantic segmentation or dense pose, we narrowed down the selection to a handful of object-detection families and focused on the group of single-shot detectors. In the report will provide a recap of our model design process that led to our decision of selecting Scaled-YOLOv4-CSP as our main model.


### Classification model: Choice of architecture

Transfer learning was employed to train the model weights of the Scaled-YOLOv4 model.
Learning hyperparameters such as learning rate and momentum were chosen in an iterative manner, and experimented with other model parameters available in the architecture.


![Object Detection](https://i.ibb.co/0tHfFgg/object-dection1.png)

## Criterion for evaluation: Precision & mAP

The Average Precision (AP) or Mean Average Precision (mAP) is averaged across all 10 IoU thresholds an over the 2 categories. This was considered the single most important metric when considering performance with respect to the measuring against the SOTA using the COCO dataset with has over 330,000 val2017 format images.

## Results of Model

Figure below shows after several iterations our model’s average precision score with a recall more than 80% allowing it to capture most ground truth object while not being too imprecise in classifying them.

![Object Detection](https://i.ibb.co/TLTTDFs/fig22-good-on-groundtruth.jpg)

Our experimentation with increasing the number of epochs pushed the model to perform considerably better than only 25 epochs as it allowed the model to have greater number of passes through the dataset and therefore learn the weights more effectively by performing more feature-extractions from each training batch.  We have also experimented with other model parameters and hyperparameters to finalize on the best model.
![Tensorbaord_results](https://i.ibb.co/JpvygmN/tensorboard-result1.png)

### Inference Performance on Test Data (mAP@.5 85.1%, Recall 88.6%, Precision 57.3%):

![Inference_results](https://i.ibb.co/xDMdD22/test-inferencing-score.png)




## Inference on Unseen Videos:

Video Inferencing results from final model using our Best Weights and achieved validation set mAP >75%:


[![Team Inference](https://github.com/dkalantari/MMAI894MaskDetection/blob/main/Assets/team_bef_aft2_small.gif?raw=true)](https://github.com/dkalantari/MMAI894MaskDetection/blob/main/Assets/team_bef_aft2.gif?raw=true)
[![Crowd Inference](https://github.com/dkalantari/MMAI894MaskDetection/blob/main/Assets/crowd_bef_aft_small.gif?raw=true)](https://github.com/dkalantari/MMAI894MaskDetection/blob/main/Assets/crowd_bef_aft.gif?raw=true)
[![Group Inference](https://github.com/dkalantari/MMAI894MaskDetection/blob/main/Assets/group_bef_aft_small.gif?raw=true)]((https://github.com/dkalantari/MMAI894MaskDetection/blob/main/Assets/group_bef_aft_small.gif?raw=true))



## Team Contributors

Bremner Inc. is a multinational professional consulting firm specialized in the field of computer vision. We provide end-to-end computer vision solutions which are tailored to solve complex business problems and help our clients achieve their goals through the use of AI. Below are the team members that helped implement this project:

| Name | Role |
| ------ | ------ |
| Dara Kalantari  | Project Manager |
| Moiz Zafar | Business Consultant |
| Devin Datt | Machine Learning Engineer |
| Yi Liu    | Machine Learning Engineer |
| Milind | Data Scientist |
| Paul Longo | Data Scientist |
| Tianchen (Ray) Guo  | Data Scientist |


