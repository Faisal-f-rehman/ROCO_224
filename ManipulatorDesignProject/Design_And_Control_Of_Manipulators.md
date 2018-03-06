#### |---------These are some useful HTML/Markdown commands that we can use while we are writting this report and delete before submission-----------|
_These commands are only visible in the raw format or in gedit_

This command puts two pictures side by side, change percentage for size but always keep height and width the same:  
<img src="" height="0%" width="0%"/><img src="" height="0%" width="0%"/>

For single image:  
![name](image link)

For video:  
[![](picture link)](video link)

Use this to add blank space if required: (each <br> adds one line of space use as many as like)
<br><br>

#### |--------------------------------------------------------------------------------------------------------------------------------------|




## Design and Control of Manipulators 

Design and control of manipulators (approximately 3000 words)

## *Introduction*

### Description of hardware 

### Description of task

### An overview of your approach to the problem

## *Design Process*

Since the arm has 8 servos, the idea behind the design was to keep it as light as possible. We decided to directly attach each servo on to the previous one without any links between them except for one link that goes after the shoulder joint. After we had a rough idea of our design, the first thing we did was to make sure that the RX-28 servos (especially the servo that will need maximum ammout of torque) will be able to deliver the required torque for the design, for this we derived the moment formulas for our design.


_|------------ Final maths for moments ------------|_

word document for torque equation at 90 degrees. how to calculate work for the servo which will be under the most
stress. The second page account for when not at 90 degrees.

_|----------------------------------------------------|_

### What design iterations have you gone through?

### Who worked on what and when?

### What problems did you encounter, and how did you solve them?

## *Implementation*

### Describe the final implementation of your manipulator

### Include figures with images/drawings etc

### Include your solutions for kinematics, motion planning etc.

### Be brief, include support material in appendices, if need be

					Rough workings for moments:  
<img src="https://github.com/Faisal-f-rehman/ROCO_224/blob/master/ManipulatorDesignProject/maths/moments%20drawing%20at%200%20degrees%20redundant.jpg?raw=true" height="30%" width="30%"/><img src="https://github.com/Faisal-f-rehman/ROCO_224/blob/master/ManipulatorDesignProject/maths/moments%20calc%200%20degrees%20redundant.jpg?raw=true" height="30%" width="30%"/><img src="https://github.com/Faisal-f-rehman/ROCO_224/blob/master/ManipulatorDesignProject/maths/moments%20about%20servo%20B%20at%2090%20degrees%20redundant.jpg?raw=true" height="35%" width="35%"/>

<br><br><br>

**Libre writer file:**
![Jack's Torque file](https://github.com/Faisal-f-rehman/ROCO_224/blob/master/ManipulatorDesignProject/maths/JackGell_torque%20equation_%2090degres.docx)

## *Experiments* 

### What testing have you performed of the robot (or subsystems)

### How well have you been able to perform the goal task?

### Include a Method, Results, and Discussion sub-section for each experiment

## *Conclusion*

### Briefly conclude this part of the coursework
