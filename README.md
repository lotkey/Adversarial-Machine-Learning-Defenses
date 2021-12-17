# Adversarial Machine Learning Defenses
Defenses against white-box evasion attacks

## Overview

The code in this repository is based on an assignment for [CS 404/504](https://www.webpages.uidaho.edu/vakanski/CS_504.html).  
The code does the following:  
 - data_loader.ipynb...
   - Preprocesses the LFW dataset
 - BinaryInputDetectionDefense.ipynb...
   - Trains a classifier on the data
   - Generates white-box attacks against the classifier
   - Implements a binary input detection defense against the attacks
 - AdversarialTrainingDefense.ipynb...
   - Implements an adversarial training defense against the attacks
   - Attacks an image to fool the [Clarifai celebrity identifier](https://www.clarifai.com/models/celebrity-face-recognition)

## Prerequisites
 
### Libraries 

The scripts are in the Jupyter notebook format. The advised way to run the scripts is with [Google Colab](https://colab.research.google.com/). Google Colab is an environment for running Jupyter notebooks on Google hardware. Free GPUs are available, and it is highly recommended you use one. It will save you days of time. Google Colab also has all sorts of libraries for machine learning (and other fields) pre-installed. The ones used in these notebooks are:  
 - tensorflow.keras (different than keras)
 - numpy
 - pandas
 - PIL (Pillow)
 - pickle
 - tabulate
 - matplotlib
 
The library used for the adversarial attacks and training is the [Adversarial Robustness Toolbox (ART)](https://adversarial-robustness-toolbox.readthedocs.io/en/latest/). It is not included in Google Colab, so the scripts automatically install it.  
*THERE IS A SLIGHT ISSUE* with ART at the moment. The Deepfool attack does not currently work. It seems as though the Deepfool attack takes too many steps, applying too much noise and using too much time. The output for the Deepfool attacks will be very inconsistent. Everything else in ART used in these notebooks works just fine.  

### Dataset

The dataset used is the [Labeled Faces in the Wild (LFW)](http://vis-www.cs.umass.edu/lfw/) dataset. The images are 100x100. There are:  
- 3043 training images
- 1049 testing images
- 1021 validation images  

### Clarifai

The [Clarifai celebrity identifier](https://www.clarifai.com/models/celebrity-face-recognition) is used in AdversarialTrainingDefense.ipynb.  

## How to use the repository

Follow the instrunctions for the notebooks in this order:
 - data_loader.ipynb
 - BinaryInputDetectionDefense.ipynb
 - AdversarialTrainingDefense.ipynb
 
Instructions are found below. The files are found in this repository at:
 - [data_loader.ipynb](./data_loader.ipynb)
 - [BinaryInputDetectionDefense.ipynb](./BinaryInputDetectionDefense.ipynb)
 - [AdversarialTrainingDefense.ipynb](./AdversarialTrainingDefense.ipynb)
 
GitHub often has issues with Jupyter notebooks. If this is the case, you can view the notebooks here as well:
 - [data_loader.ipynb](https://nbviewer.org/github/lotkey/Adversarial-Machine-Learning-Defenses/blob/main/AdversarialTrainingDefense.ipynb)
 - [BinaryInputDetectionDefense](https://nbviewer.org/github/lotkey/Adversarial-Machine-Learning-Defenses/blob/main/BinaryInputDetectionDefense.ipynb)
 - [AdversarialTrainingDefense.ipynb](https://nbviewer.org/github/lotkey/Adversarial-Machine-Learning-Defenses/blob/main/AdversarialTrainingDefense.ipynb)

If you are using Google Colab you will not need to download any libraries, the notebooks will take care of that for you. If you are not using Google Colab, you will need to download all of the libraries mentioned above.  

There is a cell for mounting your Google Drive. This only works on Google Colab. If you are not using Google Colab, do not run the cell. It is the first cell in each notebook.  

All the folders in the paths specified by you must already exist. The notebooks do not create folders that do not exist.  

## data_loader.ipynb

This notebook loads the LFW dataset, normalizes it, and saves separate files for training, testing, and validation data. To normalize the data, this notebook loads the images as integer arrays and scales them into float arrays with values in the range [0.0-1.0].   

Download the [LFW](http://vis-www.cs.umass.edu/lfw/) dataset to some path **PATH**. Set the variables:
- **DATA_DIR** to **PATH**
- **PICKLED_DATA_PATH** to the path where you would like to save the pickled (via the pickle library) data

Make sure **PATH** contains the folders **Test**, **Train**, and **Validation**. Next, run the notebook. It will preprocess the data and export it to the path you supplied.  

## BinaryInputDetectionDefense.ipynb

This notebook:
- loads the processed LFW dataset
- trains a VGG16 classifier on it
- attacks the classifier using Fast Gradient Sign Method, Projected Gradient Descent, Deepfool, and Pixel (bonus!) attacks from ART and compare their effectiveness
- implements a binary classification defense against each separate attack and compares their performance against other attacks to show their transferability
- print out reports along the way

You need to set the following variables:
- **DATA_PATH** to the same path as **PICKLED_DATA_PATH** in data_loader.ipynb
- **NAME_LIST_PATH** to the path of name_list.csv in the LFW dataset

You need to set the rest of the paths in the **Setting paths/directories/variables** cell to your preference.

Run the notebook and look at the reports.

## AdversarialTrainingDefense.ipynb

This notebook:
- loads the pretrained VGG16 classifier and attacks from BinaryInputDetectionDefense.ipynb
- adversarially trains the model using ART on the PGD attack 
- compares the performance of the undefended and defended model on various other attacks to view transferability
- uses a binary search to find the best attack with the least amount of perturbation to fool the Clarifai model
- print out reports along the way

You need to set the following variables:
- **DATA_PATH** to the same path as **PICKLED_DATA_PATH** in data_loader.ipynb
- **NAME_LIST_PATH** to the path of name_list.csv in the LFW dataset
- **VGGNET_PATH** to the same path as it is in BinaryInputDetectionDefense.ipynb
- **ADV_ATTACK_INDICES_PATH** to same path as it is in BinaryInputDetectionDefense.ipynb
- **FGSM_ATTACK_PATH** to the same path as it is in BinaryInputDetectionDefense.ipynb
- **PGD_ATTACK_PATH** to the same path as it is in BinaryInputDetectionDefense.ipynb
- **DEEPFOOL_ATTACK_PATH** to the same path as it is in BinaryInputDetectionDefense.ipynb

You need to set the rest of the paths in the **Setting paths/directories/variables** cell to your preference.

Run the notebook and look at the reports. The last part, the binary search, is interactive. The notebook will generate an attack to the path the user specified. The user must then download the image, upload it to [Clarifai model](https://www.clarifai.com/models/celebrity-face-recognition) and report back to the notebook several times. Then the notebook will save the best attack and print a report.  
