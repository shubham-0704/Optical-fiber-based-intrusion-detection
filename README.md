
<p align="center"><img width=11.5% src="images_readme\fiber-optics-icon-27.jpg" ></p>

<h1 align="center" >Optical Fiber based Physical Intrusion Detection System </h1>




## Table of content 
* [Basic Overview](#basic-overview) 
* [Installation requirement & Dependencies](#installation-requirement-and-dependencies-and-libraries)
* [Data preprocesing](#data-preprocesing)
* [Model and it's Architecture]()
* [Prediction and Result's](#prediction-and-results)
* [References](#references)
* [Future works](#future-works)
----
<br><br>




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





## Data Preprocesing



## Model and it's Architecture



## Prediction and Result's



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