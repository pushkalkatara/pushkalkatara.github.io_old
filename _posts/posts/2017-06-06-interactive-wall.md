---
layout: post
category: post
tags: Microsoft-Kinect Raspberry-Pi Arduino Servo ProcessingIDE
date: 2017-06-06 13:06
thumbnail: https://cdn.archpaper.com/wp-content/uploads/2014/03/Thibaut-550x366.jpg
title: Interactive Wall using Kinect and Servos
published: true
---

An Interactive wall is constructed of 40 servo motors embedded in the wall connected to a microcontroller and an RGB Camera with a depth sensor,
whole setup connected to a microprocessor. Object or human, if detected in the threshold using the RGB camera, servo in front of the object, gets initialized.
The servo updates with the change in the captured image creating a beautiful pattern. This was my first internship project at Proxbotics Creation Technologies.

<!--more-->
<br />
#### Microsoft Kinect Sensor
Kinect sensor features an RGB camera, a depth sensor consisting of an infrared laser projector and an infrared CMOS sensor, and a multi-array microphone.
It also contains a LED light, a three-axis accelerometer, and a small servo controlling the tilt of the device.
Kinect’s IR projector sends out a pattern of infrared light beams, which bounces on the objects and is captured by the standard CMOS image sensor.
This captured image is passed on to the onboard PrimeSense PS1080 chip to be translated into the VGA sized depth image.
<p align="center">   
<img src="/assets/images/interactivewall/kinect.png" width="400" height="200" align="center"/>
</p>
<br />
#### Servo Motors
Servos are DC motors that include a feedback mechanism that allows you to keep track of the position of the motor at every moment.
The way you control a servo is by sending it pulses with a specific duration. Generally, the range of a servo goes from 1 millisecond
for 0 degrees to 2 milliseconds for 180 degrees. You need to refresh your control signals every 20ms because the servo expects to get an
update every 20ms, or 50 times per second.
<p align="center">
<img src="/assets/images/interactivewall/pwm.jpg" width="600" height="300" align="center"/>
</p>   

<br />
#### 16 Channel PWM/Servo Controller
An i2c-controlled PWM driver with a built-in clock used to control 16 free-running PWM outputs! You can even chain up 62 breakouts to
control up to 992 PWM outputs.   
<br />
#### Hardware Interfacing

- Setting Up Raspberry Pi 3 for Kinect Support:     
Install Raspbian Jessie and boot-up Raspberry-Pi and follow the following steps to setup libfreenect open-source driver for Kinect interfacing –

- Installing Dependencies:
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install cmake libudev0 libudev-dev freeglut3 freeglut3-dev libxmu6 libxmu-dev libxi6 libxi-dev
```
- Setting Up libfreenect Driver
```bash
git clone git://github.com/OpenKinect/libfreenect.git
cd libfreenect
mkdir build
cd build
cmake -L ..
make
sudo make install
sudo ldconfig /usr/local/lib64/
```

- To use Kinect as a non-root user
```bash
sudo adduser $USER video
sudo adduser $USER plugdev
sudo nano /etc/udev/rules.d/51-kinect.rules
```

- Paste the following lines in the newly created file
```bash
# ATTR{product}=="Xbox NUI Motor"
SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02b0", MODE="0666"
# ATTR{product}=="Xbox NUI Audio"
SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02ad", MODE="0666"
# ATTR{product}=="Xbox NUI Camera"
SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02ae", MODE="0666"
# ATTR{product}=="Xbox NUI Motor"
SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02c2", MODE="0666"
# ATTR{product}=="Xbox NUI Motor"
SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02be", MODE="0666"
# ATTR{product}=="Xbox NUI Motor"
SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02bf", MODE="0666"
```

- LogOut and Log back in, open terminal and test with:
```bash
freenect-glview
```
<p align="center"> Image View <br />
<img src="/assets/images/interactivewall/kinect2.jpeg" width="500" height="250" align="center"/>
</p>  

<p align="center"> Connections:  <br />
<img src="/assets/images/interactivewall/kinect.jpeg" width="500" height="200" />
</p>
<br />
#### Control Code
- Approach 1 – Python + Raspberry Pi 3B + 16 Channel PWM Servo Driver

- Approach 2 – Processing IDE + Raspberry Pi 3B + 16 Channel PWM Servo Driver

- Approach 3 – Processing IDE + Raspberry Pi 3B + Arduino(Serial Comm.) + 16 Channel PWM Servo Driver

- Approach 4 – Processing IDE + Raspberry Pi 3b + Arduino Firmata + 16 Channel PWM Servo Driver
