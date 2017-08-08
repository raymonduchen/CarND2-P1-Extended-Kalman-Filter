# CarND2-P1 Extended Kalman Filter

## Description

**This my 1st project result of Udacity self-driving car nanodegree (CarND) term 2. It's required to combine two types of sensing data, lidar and radar, to localize object using so-called extended Kalman filter (EKF). A simulator is provided to visualize sensing data and EKF localization result.**

**The following demonstrates EKF localization result and measurement data in action :** 

* Blue circle : radar measurement
* Red circle : laser measurement
* Green circle : computed EKF localization

![alt text][image1]

* Udacity self-driving car nanodegree (CarND) :

  https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd013
  
* Udacity self-driving car nanodegree term 2 simulator :

  https://github.com/udacity/self-driving-car-sim/releases/

The goals / steps of this project are the following:

[//]: # (Image References)
[image1]: ./images/ekf.gif
[image2]: ./images/flowchart.png
[image3]: ./images/EKF.png
[image4]: ./images/radar.png
[image5]: ./images/laser.png
[image6]: ./images/radar_laser.png
[image7]: ./images/pRMSE.png
[image8]: ./images/vRMSE.png

![alt text][image2]

* The measurement data receiving and connection to simulator is in C++ file `./src/main.cpp`.

* The Kalman filter initialization, predict and update is called in C++ file `./src/FusionEKF.cpp`.

* The implementation of Kalman filter is in C++ file `./src/kalman_filter.cpp`.

* Fuction to calculate RMSE and jacobian matrix used for evaluation of localization quality is in C++ file `./src/tools.cpp`.

## Usage
* `mkdir build` 
* `cd build`
* `cmake ..`
* `make`
* `./ExtendedKF`
* Download simulator `term2_sim.app` (if in OSX) and open it. Click `play!` bottom, select Project 1/2: EKF and UKF, and press `Start` bottom to start.

## Extended Kalman Filter (EKF)

Kalman filter is a typical technique used to fuse multiple sensing data and get a more accurate result (state) based on linear assumption and Bayes rule. While laser measurement is linear and applicable for Kalman filter, radar measurement required to be linearized to fit a so-called extended Kalman filter. 

Both Kalman filter and extended Kalman filter generally takes two step : predict and update. 

In predict step, elapsed time `dt` is used to update state transition matrix `F` or `Fj` and process covariance matrix `Q`. Then state vector `x'` and state covariance matrix `P'` are predicted.

In update step, measurement data `z` and previous state `x'` are used to judge the measurement pre-fit residual `y` between predicted state `Hx'` or `h(x')` and measurement data `z`. pre-fit residual covariance `S` and Kalman gain `K` are also calculated. Then updated state `x` and state covariance matrix `P` are computed.

The detailed formula is listed below :

![alt text][image3]


## EKF performance evaluation

By comparing RMSE of EKF result and ground truth, EKF localization performance can be evaluated. position RMSE and velocity RMSE are compared :

![alt text][image7]

![alt text][image8]


## Discussion

By disabling laser or radar update, the EKF localization performance is obviously deviate the ground truth than utilizing both sensor update. The lower RMSE mentioned in previous figure manifests Kalman filter indeed increase the accuracy of localization. 

Here's three types of EKF route comparisons between groud truth and EKF estimation : 

### Only use radar

![alt text][image4]

### Only use laser

![alt text][image5]

### Use both radar and laser

![alt text][image6]



