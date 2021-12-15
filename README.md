# Adversarial Machine Learning Defenses
Defenses against white-box evasion attacks

The code in this repository is based on an assignment for [CS 404/504](https://www.webpages.uidaho.edu/vakanski/CS_504.html).  
The code preprocesses:  
 - Preprocesses the LFW dataset
 - Trains a classifier on it
 - Generates white-box attacks against the classifier
 - Implements two different defenses against the attacks
   - Binary input detection
   - Adversarial training
 
The scripts are in the Jupyter notebook format. The advised way to run the scripts is with [Google Colab](https://colab.research.google.com/). Google Colab is an environment for running Jupyter notebooks on Google hardware. Free GPUs are available, and it is highly recommended you use one. It will save you days of time. Google Colab also has all sorts of libraries for machine learning (and other fields) pre-installed. The ones used in these notebooks are:  
 - tensorflow.keras (different than keras)
 - numpy
 - pandas
 - PIL (Pillow)
 - matplotlib
 
The library used for the adversarial attacks and training is the [Adversarial Robustness Toolbox (ART)](https://adversarial-robustness-toolbox.readthedocs.io/en/latest/). It is not included in Google Colab, so the scripts automatically install it.  
*THERE IS A SLIGHT ISSUE* with ART at the moment. The Deepfool attack does not currently work. It seems as though the Deepfool attack takes too many steps, applying too much noise and using too much time. The output for the Deepfool attacks will be very inconsistent. Everything else in ART used in these notebooks works just fine.  

The dataset used is the [Labeled Faces in the Wild (LFW)](http://vis-www.cs.umass.edu/lfw/) dataset.  