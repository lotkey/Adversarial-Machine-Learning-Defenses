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
   - Attacks an image to fool the [clarifai celebrity identifier](https://www.clarifai.com/models/celebrity-face-recognition)

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

The dataset used is the [Labeled Faces in the Wild (LFW)](http://vis-www.cs.umass.edu/lfw/) dataset.  

### Clarifai

The [clarifai celebrity identifier](https://www.clarifai.com/models/celebrity-face-recognition) is used in AdversarialTrainingDefense.ipynb.  

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

## data_loader.ipynb

This notebook loads the LFW dataset, normalizes it, and saves separate files for training, testing, and validation data.  
