---
layout: post
title:  "Pixhawk: Getting started with initial setup"
title:  "Quick guide on how to setup pixhawk for beginners"
date:   2022-04-02
categories: Aero Pixhawk
---
![](https://docs.px4.io/master/assets/img/console_debug.a86c2eb3.jpg)

[Pixhawk](https://ardupilot.org/copter/docs/common-pixhawk-overview.html){:target="_blank"} is the most sought out flight controller for numerous applications among hobbyists and professionals. By pairing with a companion computer more advanced tasks can be performed like live object tracking, real time 3D image reconstruction, streaming data to the cloud and much more.  

[Ardupilot](https://ardupilot.org/){:target="_blank"} and [Px4](https://px4.io/){:target="_blank"} are the most popular open source firmwares available for pixhawk. However Ardupilot is more mature than Px4, with more features and community support. Now let's get started with the setup with Ardupilot.

## Prerequisite
- xCopter with Pixhawk as flight controller with GPS.
- [Mission Planner](https://ardupilot.org/planner/docs/mission-planner-installation.html){:target="_blank"} as Ground Control Station. 

## Instructions
---  
Here is the basic connection to be made before proceeding any further.  
Hang on tight, it's is going be a bumpy ride (I'm talking to pixhawk, not you silly)

![](https://ardupilot.org/copter/_images/pixhawk_connect_essential_peripherals.jpg)


#### 1. **Flash firmware to pixhawk**  
![](https://ardupilot.org/planner/_images/Pixhawk_InstallFirmware.jpg)

We will be using ardupilot firmware. This can be flashed through mission planner.  
Here is the [detailed instruction](https://ardupilot.org/planner/docs/common-loading-firmware-onto-pixhawk.html){:target="_blank"} to install firmware to pixhawk.


#### 2. **Calibrate Accelerometer and Compass**  

![](https://ardupilot.org/copter/_images/mp_accelerometer_calibration.png)

- [Detailed Accelerometer calibration steps](https://ardupilot.org/copter/docs/common-accelerometer-calibration.html){:target="_blank"}.
- [Detailed Compass calibration steps](https://ardupilot.org/copter/docs/common-compass-calibration-in-mission-planner.html){:target="_blank"}.

#### 3. **Connect RC, ESC and Motors**  

I'm sure many of you have seen this diagram. Have eveything connected and ready.  
<b>*Note: Don't connect propellers*</b>

![](https://ardupilot.org/copter/_images/Pixhawk-Inforgraphic2.jpg)


#### 4. **Calibrate Radio Control**  
![](https://ardupilot.org/copter/_images/mp_radio_calibration.png)

- [Detailed RC calibration steps](https://ardupilot.org/copter/docs/common-radio-control-calibration.html){:target="_blank"}.

#### 5. **Calibrate ESC**  
<b>*Note: remove propellers if attached*</b>
![](https://ardupilot.org/copter/_images/copter_disconnect_props_banner.png)

- [Detailed ESC calibration steps](https://ardupilot.org/copter/docs/esc-calibration.html){:target="_blank"}.

#### 6. **Setting extra parameter (Optional)**  
By default motors will start spinning when armed even at zero throttle. To   only spin when throttle is given, following setting needs to be changed.  
1. Go to CONFIG -> Advanced Params
![](/assets/posts/{{page.url}}/images/ss1.png)

2. Find -> Type MOT_SPIN_ARM and click OK
![](/assets/posts/{{page.url}}/images/ss2.png)

3. Set Motor Spin armed -> Low
![](/assets/posts/{{page.url}}/images/ss3.png)

#### 7. **Assemble for test flight (Not so fast)**  
Get eveything assembled to frame, attach propellers and tuck in hanging wires.  
- Double check esc, motor and propeller connection configuration.
<b>*Note: Don't arm yet*</b>


#### 8. **Calibrate Level**   
Place the assembled copter on plain flat surface and click on Calibrate Level. This is to set reference point to copter to be stable. 
![](https://ardupilot.org/planner/_images/mp_calibration_successful.png)

#### 9. **Setting another extra parameter (Optional)**  
To make life easy, swtiches comes in handy. To arm and disarm default method is hold throttle stick to down-right for 5 seconds.
To assign this to a switch follow [How to set ARM-DISARM Switch in Mission Planner and RC Transmitter for Pixhawk](/arm-disarm-pixhawk){:target="_blank"}.


#### 10. **Fly my child 🕊️**  
This is a test flight so be cautious of your surrounding and not to fly beyond 2 meters. Keep it low and steady.  
1. Set the flight mode to Auto or Loiter.  
2. Turn on safety switch and arm the motors. 
- If you have not followed step 9, then follow this [arm and disarm](https://ardupilot.org/copter/docs/arming_the_motors.html){:target="_blank"}.  
