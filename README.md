# TheEasyYolo

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1brPZDy_yVDo38ixxpI6iSu7V4fj82Ohq?usp=sharing)

This repo contains a simple notebook **TheEasyYolo.ipynb** to train multiple instance of YoloV3 and YoloV4 with their tiny versions. You can train yolo with initilization of  different parameters like number of classes, channels, width and height. 

The directory structure:
    
    ├── TheEasyYolo
    ├────── Instance-1
    ├─────────── data
    ├─────────────── train
    ├─────────────── test
    ├────── Instance-2
    .
    .
    ├────── Instance-N
    ├────── darknet
    ├────── TheEasyYolo.ipynb
    ├────── README.md
    

# Instructions
## Setup on Google Drive
Link notebook with your google drive for saving checkpoints,
 ```
 from google.colab import drive
 drive.mount('/content/drive')
 ```

## Clone this repo
Clone this repository to your gdrive

## Setup the parameters and yolo settings
Setting up the yolo with different instance name as your project required, change the parameters according to custom training, 

```
instance_name = "instance_name"     # Put any name of the Instance 
#set hyperparameters
num_of_classes = 1                  # Total number of classes 
channel = 3                         # Channel used "1 for Grayscale or 3 for RGB"
sub_division = 16            
width = 320                         # Width of input image
height = 256                        # Height of input image
batch = 32                          # batch size
yolo_ver = "YoloV4-tiny"            #The input should be YoloV4, YoloV4-tiny, YoloV3, YoloV3-tiny

```



## Upload the dataset to instance's name folder
After initilization the parameters of yolo, gather the dataset and label them according to yolo's label format, and put the "data" folder in instance's name folder.
The data structure should like this:
  
    ├── data
    ├────── train
    ├──────── --.jpg
    ├──────── --.txt
    ├───────test
    
    


## Generate train.names file and add all class names
```
%cd {instance_name}
with open("train.names", "w") as f:   
    f.write("class_name")
    #f.write("\nother classe")
%cd ..
```

## Convert yolov2 model to tflite 
#### Requirement
    tensorflow  1.15

  1 - use this link to convert from .weights to .pb [Link](https://gist.github.com/pra-dan/70944415aae7e6b3dc41d5ada1feb3e7/raw/8c2d5edf164aaf589ce66700f5aa05fc04509475/Darknet2TF_using_Darkflow.sh)
  
  
  2 -  run this command to convert into tflite 
  ```
  toco --graph_def_file built_graph/yolov2_coin.pb     --output_file yolo-v2-tiny-coco.tflite     --output_format TFLITE     --inference_type FLOAT     --inference_input_type FLOAT     --input_arrays input     --output_arrays output    --allow_custom_ops
  ```

