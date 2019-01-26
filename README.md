# Driving Style Representation in Convolutional Recurrent Neural Network Models of Driver Identification

In this repository we provide all the implementations for our models and baselines, along with several sample files to reproduce our results.

## Feature Engineering 
* Statistical Feature Matrix: to generate feature matrix as input for deep models, use ```Create_FeatureMatrix.py```. 
* Feature Vector V1: to generate the original feature vector for a trajectory to be used by GBDT model, use ```Create_FeatureVector_V1.py```. 
* Feature Vector V2: to generate the modified feature vector for a trajectory to be used by GBDT model, use ```Create_FeatureVector_V2.py```. 

## Models
* __D-CRNN__: this is our proposed model to perform driver prediction based on driving style information. This model combines several important compoenents of deep-neural-network architectures including recurrent, convolutional, and fully connected components. An implementation of this model in Tensorflow can be find [here](#). Following diagram also describes the design of this model: <center><img src="/files/D-CRNN_2.png" width="1100"></center>

* __VRAE__: this is the Variational Recurrent Auto-encoder model, proposed by [Fabius and Amersfoort (2015)](https://arxiv.org/abs/1412.6581). Here we extend the [original implementation](https://github.com/y0ast/Variational-Recurrent-Autoencoder) to use it for driver prediction task by a modified loss function. The implementation of this model in Theano can be find [here](#). 

* __GBDT__: this is a Gradient Boosting Decision Tree model which we use it for driver prediction task. A Python imeplementatin of this method based on scikit-learn library is available [here](#). 

* __CNN-model__: this is a Convolutional Neural Network model to perform driver prediction task, and is proposed by [Dong et al. (2016)](https://arxiv.org/abs/1607.03611). Imeplementation of this method in Tensorflow can be find [here](#). 

* __RNN-model__: this is a Recurrent Neural Network model to perform driver prediction task, and is proposed by [Dong et al. (2016)](https://arxiv.org/abs/1607.03611). Imeplementation of this method in Tensorflow can be find [here](#). 

## Requirements
* __Python__: You may use either Python 2.7 or 3. 
* __Tensorflow__: For all deep models except VRAE, you need Tensorflow (```version >= 1.12.0``` is recommended). 
* __Theano__: To run VRAE model, you need theano version > ??. 
* __Cuda Library__: You need to have Cuda Library for tensorflow-based codes, and ```version > 9.0.176``` is recommended. 
* __Scikit-learn__: For GBDT models, you need to install scikit-learn library. 

Note that our models can be run on both CPU and GPU machines. 

## How to Run
__Creating Feature Vector/Matrix__
* Generate Feature Matrix: Use ```python Create_FeatureMatrix.py``` to create feature matrix. This will result in creating two files in __data__ directory, one _npy_ and one _pkl_ file. 
* Generate Feature Vector: This is to generate input for non-deep models, such as GBDT. For the original version of features as described [here](), use ```Create_FeatureVector_V1.py```, and for the modified version as described in [our paper](), use ```Create_FeatureVector_V2.py```. For each data file, we create one _npy_ and one _pkl_ file, using either of scripts. 

__Modeling and Prediction__
* Run Deep Models: You just need to use ```python [MODEL_NAME].py```. Make sure you have all the requirements satisfied. 
* Run GBDT Models: Set the desired input data file in script and use ```python GBDT.py``` to run the script. 

## Sample Data
You may find a raw sample file in [data](https://github.com/sobhan-moosavi/DCRNN/tree/master/data) directory. In this file we have 5 drivers, and 10 random trajectories for each driver. The format of this file is described as follows: 

| Attribute | Description |
|:---------:|-------------|
|Driver| Indicates driver id, which is a string. |
|ID| Indicates trajectory id, which is a string. |
|Time| An integer which indicates the timestep for a datapoint of a trajectory. |
|Lat| Shows the latitude value of GPS coordinate. |
|Lon| Shows the longitude value of GPS coordinate. |
|Speed| Shows the ground velocity of the vehicle as reported by OBD-II port. |
|Acceleration| Shows the rate of change of ground velocity or speed. |
|RPM| Shows the round per minute, as reported by OBD-II port. |
|Heading| Shows the bearing of the vehicle, which is a value between 0 and 359. |
|AccelX| Shows the acceleration sensor reading along with X-axis. |
|AccelY| Shows the acceleration sensor reading along with Y-axis. |
|AccelZ| Shows the acceleration sensor reading along with Z-axis. |


## Sample Results
Following is the result of different models on a random sample set of 50 drivers, with 50 trajectories per driver. For deep models, we report accuracy on both segment as well as trajectory, see the [paper](#) for details. 

| Model | Accuracy--Segment | Accuracy--Trajectory |
|:-----:|:-----------------:|:--------------------:|
| GBDT-V1| -- | 25.13% |
| GBDT-V2| -- | 49.24% |
| CNN-model | 42.83% | 59.90% |
| RNN-model | 55.45% | 70.73% |
| VRAE | 51.28% | 63.67% |
| D-CRNN | __62.94%__ | __78.00%__ |


## Acknowledgments 
Please cite the following paper when use this code: TBD
