---
layout: post
title:  "How to set ARM-DISARM Switch in Mission Planner and RC Transmitter for Pixhawk"
description:  "Quick tip on setting arm disarm switch on pixhawk and rc for beginners"
date:   2022-04-03
categories: Pixhawk
---

I got into making an autonomous quadcopter for a project with no prior knowledge of what goes into building one. As a beginner myself, I was overwhelmed with the number of parameter settings in Mission Planner.  

The default method to ARM is provided here is recommended for beginners.  

*Caution: Accidentally disarming while in mid-air could crash your copter using this method. Only proceed if you know what you are doing.*  

#### a) Mission Planner
Hope you have done the initial pixhawk setup. Connect to pixhawk via usb or telemetry. 
1. Navigate to CONFIG -> User Params 

2. Select RC6_OPTION dropdown. This means we are going to use Channel 6 for this control.  
*Note: Channel 5 is not available as it is used for Flight Modes by default.*  
![](/assets/posts/{{page.url}}/images/ss1.png)

3. Select ArmDisarm option.
![](/assets/posts/{{page.url}}/images/Screenshot (2).png)

4. Click Modify to save changes.
![](/assets/posts/{{page.url}}/images/ss3.png)

5. Click OK to save setting.
![](/assets/posts/{{page.url}}/images/Screenshot (4).png)

Now we are done setting in Mission Planner, let's set RC transmitter channel 6 to switch if not.

---

#### b) RC Transmitter
I'm using Flysky FS-i6x so settings navigation might vary if you are using other transmitter model.   
![Flysky FS-i6x Transmitter]()
The following guide assumes you already know how to navigate and save settings in the RC transmitter. If not READ THE MANUAL!  
1. Go to Functions setup
![](/assets/posts/{{page.url}}/images/rc1.jpg)

2. Select Aux. channels
![](/assets/posts/{{page.url}}/images/rc2.jpg)

3. Set channel 6 to SwD as we have set channel 6 in Mission Planner. You can set this to any one of 4 switches (SWA, SWB, SWC and SWD).  
*Note: The channel number in Mission Planner and Transmitter has to be same.*
![](/assets/posts/{{page.url}}/images/rc3.jpg)

4. Save changes and it's ready to arm. Now toggle the switch to Arm-Disarm.


#### Final Thought
Arming and Disarming through the switch is convenient but if multiple switches are assigned and If you hit the wrong switch it could crash your quadcopter. So use with caution.