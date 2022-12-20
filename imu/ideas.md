---
title: IMU ideas
description: 
published: true
date: 2022-12-20T15:16:16.400Z
tags: 
editor: markdown
dateCreated: 2022-12-14T19:48:21.807Z
---

# Ideas & links

This page is a "link dump" with ideas and potential useful information/frameworks/solutions/etc.

## Linear algebra

### Embedded
* [BLASFEO - BLAS For Embedded Optimization](https://github.com/giaf/blasfeo)

### x64
* [libxsmm (Intel)](https://libxsmm.readthedocs.io/en/latest/)

## On rotations

* [Better rotation representations for accurate pose estimation](https://towardsdatascience.com/better-rotation-representations-for-accurate-pose-estimation-e890a7e1317f)
* [3D Rotations: Intuitions And Limitations](https://towardsdatascience.com/3d-rotations-intuitions-and-limitations-f3ae2122fe23)

## Sensor fusion

* [Sensor Fusion](https://sensorfusion.se/) online course material from Linköping University.
* [Sensor Fusion: Part 1](https://telesens.co/2017/04/27/sensor-fusion-part-1/): a brief 4 part series fusing accelerometer and gyroscope data into orientation estimates.
* [sensor fusion library](https://github.com/xioTechnologies/Fusion) in C for fusing accelerometer, gyroscope and magnetometer data.
* [Strapdown inertial navigation](https://rotations.berkeley.edu/strapdown-inertial-navigation/)

* [Optimization-Based Sensor Fusion of GNSS and IMU Using a Moving Horizon Approach](https://cdn.syscop.de/publications/Girrbach2017.pdf)

### IMU error sources

* [An Intuitive Approach to Inertial Sensor Bias Estimation](https://www.hindawi.com/journals/ijno/2013/762758/)


### Complementry filters

* [Reading a IMU Without Kalman: The Complementary Filter](https://pieter-jan.com/node/11)

### Kalman

* [Kalman and Bayesian Filters in Python](https://github.com/rlabbe/Kalman-and-Bayesian-Filters-in-Python): great interactive introduction to Kalman filtering.
* [How a Kalman filter works, in pictures](https://www.bzarg.com/p/how-a-kalman-filter-works-in-pictures/)

## General

* [My IMU estimation experience](https://sites.google.com/site/myimuestimationexperience/home): a starting point, but didn't get very far.
* [On the Orientation Error of IMU: Investigating Static and Dynamic Accuracy Targeting Human Motion](https://www.researchgate.net/publication/307969925_On_the_Orientation_Error_of_IMU_Investigating_Static_and_Dynamic_Accuracy_Targeting_Human_Motion)

## Implementations

* [AHRS: Attitude and Heading Reference Systems](https://ahrs.readthedocs.io/en/latest/)

## Sensors

* [TI Precision Labs - Magnetic sensors](https://training.ti.com/ti-precision-labs-magnetic-sensors)

## Alternatives

* [MPU-9250 with Madgwick](https://github.com/kriswiner/MPU9250)

## Optmization filters

* [Ceres](https://github.com/ceres-solver/ceres-solver)
* [Automatic Differentiation: Forward and Reverse](https://jingnanshi.com/blog/autodiff.html)
* [Interactive Gradient Descent Demo](https://blog.skz.dev/gradient-descent)