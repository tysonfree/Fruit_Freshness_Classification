# How to Create a Fruit Freshness Classification Model

This demo was created on Windows 10 and outlines how to create a model classifies the freshness of fruits such as apples, bananas, and oranges using Tensorflow.

### Prerequisites

During the time of writing this tutorial the following were used:

pip 19.1.1

Python 3.7.3

Tensorflow 1.14.0

curl 7.65.1


### Overarching Tutorial Used to Create This Tutorial

https://www.tensorflow.org/hub/tutorials/image_retraining

### Steps Outline
1.	Gather a Dataset
2.	Retrain a Model on Your Dataset Using Tensorflow
3.	Test and Improve Your Model
4.	Optimize Your Model Using OpenVINO

### 1. Gather a Dataset

*Option 1:* Search for already existing datasets
For this tutorial I used the Fruits Fresh and Rotten for Classification from Kaggle since this dataset already existed and had what I needed to classify different fruits.

*Option 2:* Create your own dataset
Google Chrome has an extension called [Fatkun Batch Download Image](https://chrome.google.com/webstore/detail/fatkun-batch-download-ima/nnjjahlikiabnchcpehcpkdeckfgnohf?hl=en) that you can use to gather a dataset using a simple google search. It allows you edit your dataset from the search as well (in case you get some unwanted images).
Once you gather your dataset, separate them into folders and name each folder what you want to name it for each class. Then, put these folders into the desired directory that you want. 

# 
*Here’s what I did:*

![file structure][image 1]
 
*If you have more fruits in your dataset, you can use more folders of course*
# 


### 2. Retrain a Model on Your Dataset Using Tensorflow

In the command line use curl to get the retrain.py file from tensorflow and put it in the desired directory.

```
cd <Path_To_Desired_Directory>
curl -LO https://github.com/tensorflow/hub/raw/master/examples/image_retraining/retrain.py
```

# 
Here’s where I put it:
 
![file structure][image 2]
# 

Next, run the following command to start the retraining process.
```
python retrain.py --image_dir <Path_To_Images>
```

By default an Inception V3 model trained on ImageNet will be retrained. You can change the amount of training steps, learning rate and other parameters, by passing flags. See more on this [here](https://www.tensorflow.org/hub/tutorials/image_retraining).

# 
*Here’s the command I used:*
```
python retrain.py --image_dir images
```

The files will be store in the ```C:\tmp``` directory. I moved them to a folder called training:

![file structure][image 3]
# 
 
### 3. Test and Improve Your Model

In the command line use curl to get the label_image.py file from tensorflow and put it in the desired directory.
```
cd <Path_To_Desired_Directory>
curl -LO https://github.com/tensorflow/tensorflow/raw/master/tensorflow/examples/label_image/label_image.py
```

# 
*I created an input folder for storing test images to classify:*

![file structure][image 4]
# 
 
In the command line run the following command in order to label an image that you want:

```
python label_image.py --graph C:/<Path_To_Directory>/output_graph.pb --labels C:/<Path_To_Directory>/output_labels.txt --input_layer=Placeholder --output_layer final_result --input_height 299 --input_width 299 --image C:/<Path_To_Directory>/<image_filename>
```

# 
*Here’s the command I used:*
```
python label_image.py --graph C:/Projects/Fruit_Classification_TF/Fruit_Classification/training/output_graph.pb --labels C:/Projects/Fruit_Classification_TF/Fruit_Classification/training/output_labels.txt --input_layer=Placeholder --output_layer final_result --input_height 299 --input_width 299 --image C:/Projects/Fruit_Classification_TF/Fruit_Classification/input/apple.jpg
```
# 

### 4. Optimize Your Model Using OpenVINO
Use this as a guide to use the Model Optimizer:
https://docs.openvinotoolkit.org/latest/_docs_MO_DG_prepare_model_convert_model_Convert_Model_From_TensorFlow.html#Convert_From_TF


### You know should have a model that classifies the freshness of apples, bananas, oranges, or any other fruits that you want!

![Project Gif][image 5]

![Output][image 6]

[image 1]: https://github.com/tysonfree/Fruit_Freshness_Classification/blob/master/README_Pictures/1.PNG
[image 2]: https://github.com/tysonfree/Fruit_Freshness_Classification/blob/master/README_Pictures/2.PNG
[image 3]: https://github.com/tysonfree/Fruit_Freshness_Classification/blob/master/README_Pictures/3.PNG
[image 4]: https://github.com/tysonfree/Fruit_Freshness_Classification/blob/master/README_Pictures/4.PNG
[image 5]: https://github.com/tysonfree/Fruit_Freshness_Classification/blob/master/README_Pictures/project_finished.gif
[image 6]: https://github.com/tysonfree/Fruit_Freshness_Classification/blob/master/README_Pictures/5.PNG


