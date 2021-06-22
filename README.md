
<p align="center"><img width=11.5% src="images_readme\fiber-optics-icon-27.jpg" ></p>

<h1 align="center" >Optical Fiber based Physical Intrusion Detection System </h1>




## Table of content 
* [Basic Overview](#basic-overview) 
* [Installation requirement & Dependencies](#installation-requirement-and-dependencies-and-libraries)
* [Data preprocesing](#data-preprocessing)
* [Model and it's Architecture](#model-and-its-architecture)
* [Prediction and Result's](#prediction-and-results)
* [References](#references)
* [Future works](#future-works)
----
<br>


## Basic Overview
Using Optical fiber data received from **OTDR** machine then using that data in  **Machine learning model** to detect intrusion and its location so basically, optical fiber is laid on the ground around 5 cm deep or on wall or fence when someone tries to enter then due to movement of intruder vibration is created which disturb the optical fiber signal and get reflected on **OTDR** data. From analyzing the data, model find intrusion location and gives alert of intrusion.

<p align="center">
<img width =35% src="images_readme\fib.jpg" >
<img width =35% src="images_readme\fib2.jpg" >
</p>
<br>

* **Workflow Diagram** :
    - Data is collected from OTDR
    - Data preprocessed and fed to model
    - Making Model and training and Prediction
    - Result of model
<p align="center">
<img width=75% src="images_readme\model_pro.png" >
</p>
<br>






## Installation requirement and Dependencies and libraries
<br>
<p align="left">
<img alt="Python" src="https://img.shields.io/badge/Python-v3.7+-blue?style=?style=flat&logo=python&logoColor=white"/>
    &nbsp;
<img alt="Keras" src="https://img.shields.io/badge/Keras-v2.4.3+-red?style=?style=flat&logo=keras&logoColor=white"/>
    &nbsp;
<img alt="scipy" src="https://img.shields.io/badge/Scipy-v1.4.1+-ff69b4?style=?style=flat&logo=scipy&logoColor=white"/>
    &nbsp;
<img alt="pandas" src="https://img.shields.io/badge/Pandas-v1.0.1+-9cf?style=?style=flat&logo=pandas&logoColor=white"/>
    &nbsp;
<img alt="numpy" src="https://img.shields.io/badge/Numpy-v1.18.1+-important?style=?style=flat&logo=numpy&logoColor=white"/>
    &nbsp;

<img alt="matplotlib" src="https://img.shields.io/badge/Matplotlib-v3.1.3+-green?style=?style=flat&logo=plotly&logoColor=white"/>
    &nbsp;

</p>
<br>





## Data Preprocessing
* Data is generated with a mathematical model of **OTDR** and Intrusion is introduced at the random location using sinusoidal noise.<br>
* For test 4000 meter cable length is taken which divide into 97 zones each of 41 meters approx. for better data extraction and detection.
* Difference of Amplitude is used as the main parameter for feeding in model and detection.

<p align="left">
<img width=45% src="images_readme\dif_amp.png" >
</p>
<br>

* All data are generated in Matlab then it is converted to CSV for working in python.
```python
## Code for converting .mat to csv
data = scipy.io.loadmat('D:\design lab\case1_10.mat')

## data is dictionary with keys : __header__ , __version__, __globals__, array

Amp_data=data["array"][0][0]["Amp"][0].reshape(-1)
DifferenceAmp_data=data["array"][0][0]["DifferenceAmp"][0]
Phase_data=data["array"][0][0]["Phase"][0]
DiffPhase_data=data["array"][0][0]["DiffPhase"][0]
```

* Data Visualization of single trace .
<p align="left">
<img width=65% src="images_readme\vis.png" >
</p>
<br>


## Model and its Architecture
* Data traces are then passed through a **Deep Learning Model**  which is an **Autoencoder** and the model is trained.
* After training the Model, the constructional loss is studied and used as a parameter.
* then from trained autoencoder model we generate mean signal bypassing traces after that the means signal is used as dynamic average and using constructional loss standard deviation to create  an envelope around average signal which shows the normal range in which a data should lies if its crosses then there is some intrusion 
* Autoencoder remove anomaly present in the signal while encoding and after decoding the traces,the output trace acts as the mean signal
<p align="center">
<img width=80% src="images_readme\model.jpg" >
</p>
<br>

```python

## Auto encoder model using CNN
model = Sequential()
model.add(Conv1D(90, kernel_size=1,input_shape=(1,97)))
model.add(LeakyReLU())
model.add(MaxPooling1D(pool_size=1))
model.add(Conv1D(45, kernel_size=1))
model.add(LeakyReLU())
model.add(MaxPooling1D(pool_size=1))
model.add(Conv1D(25, kernel_size=1))
model.add(LeakyReLU())
model.add(MaxPooling1D(pool_size=1))
model.add(Conv1D(45, kernel_size=1))
model.add(LeakyReLU())
model.add(MaxPooling1D(pool_size=1))

model.add(Conv1D(90, kernel_size=1))
model.add(LeakyReLU())
model.add(Flatten())
model.add(Dense(97,activation="sigmoid"))

model.summary()

## Model summary

Model: "sequential"
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
conv1d (Conv1D)              (None, 1, 90)             8820      
_________________________________________________________________
leaky_re_lu (LeakyReLU)      (None, 1, 90)             0         
_________________________________________________________________
max_pooling1d (MaxPooling1D) (None, 1, 90)             0         
_________________________________________________________________
conv1d_1 (Conv1D)            (None, 1, 45)             4095      
_________________________________________________________________
leaky_re_lu_1 (LeakyReLU)    (None, 1, 45)             0         
_________________________________________________________________
max_pooling1d_1 (MaxPooling1 (None, 1, 45)             0         
_________________________________________________________________
conv1d_2 (Conv1D)            (None, 1, 25)             1150      
_________________________________________________________________
leaky_re_lu_2 (LeakyReLU)    (None, 1, 25)             0         
_________________________________________________________________
max_pooling1d_2 (MaxPooling1 (None, 1, 25)             0         
_________________________________________________________________
conv1d_3 (Conv1D)            (None, 1, 45)             1170      
_________________________________________________________________
leaky_re_lu_3 (LeakyReLU)    (None, 1, 45)             0         
_________________________________________________________________
max_pooling1d_3 (MaxPooling1 (None, 1, 45)             0         
_________________________________________________________________
conv1d_4 (Conv1D)            (None, 1, 90)             4140      
_________________________________________________________________
leaky_re_lu_4 (LeakyReLU)    (None, 1, 90)             0         
_________________________________________________________________
flatten (Flatten)            (None, 90)                0         
_________________________________________________________________
dense (Dense)                (None, 97)                8827      
=================================================================
Total params: 28,202
Trainable params: 28,202
Non-trainable params: 0
```

## Prediction and Result's
* From the  data an enevelop is created around dynamic mean signal and from that we detected at which point there is intrusion.
```python
#  creating threshold envelop around the Mean signal/output signal
# standard deviation of conructional loss   
upper_thresh=pred_mean_signal+2.3*standard_deviation

lower_thresh=pred_mean_signal-2.3*standard_deviation
```
* Below is the grpahical demostarion of detection proces by model
<p align="left">
<img width=80% src="images_readme\final.gif" >
</p>
<br>


**Model Accuracy :**  **96.35%**

**Model Resolution :**  **41 meters**

> Resolution means the minimum length in which intrusion can be detected


<br>

## References
* [About auto-encoder and architecture ](https://www.compthree.com/blog/autoencoder/)
* [Deep Learning Algorithms for Signal Recognition in Long Perimeter Monitoring Distributed Fiber Optic Sensors](https://arxiv.org/pdf/1610.00279.pdf)
* [SNR Enhancement in Phase-Sensitive OTDR with Adaptive 2-D Bilateral Filtering Algorithm](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=7919173)




## Future Works 
* Improving the Resolution of system and model
* Filtering out the different type of Intrusion in class as follow :
    * Threatening Intrusion
    * Non-threatening Intrusion
---
<br>

![Contributions welcome](https://img.shields.io/static/v1?label=Contribution&message=welcome&color=orange?style=for-the-badge&logo=appveyor ) 