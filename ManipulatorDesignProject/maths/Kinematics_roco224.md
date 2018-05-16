# Kinematics ROCO224

<br><br>

Kinematics for our arm took many turns:

<br>

First problem we encountered was singularity due to the nature of the design. We did not take into account that every other servo was aligned at the same rotation axis. This meant that the determinant of our Jacobian matrix equaled to zero. We also observed that the closer we got to singularity, ie the closer determinant of the jacobian matrix got to zero the faster rotational velocity became.  

<br>

Secondly the initial position of the arm, in this configuration cannot be set at zero or pi radian. This is becasue sin(0) and sin(pi) = 0, which throws the Jacobian matrix to zero again.

<br>

To avoid singularity due to aligned rotational axis and initial conditions we introduced constraints on the joint angles (theta) in matlab and as recommended to us, in the design review, we introduced offsets for three joints with the aligned rotational axis, in the direction of the parameter "d" of the DH convention, ie in the Z-axis of i-n frame. This worked very well since matlab stopped complaining about singularities in the system.  

<br>

Unfortunately the inverse kinematics still did not produce expected or reasonable results, even though we tried to resolve this until the very last day. 

			Denavit–Hartenberg Table and Homogeneous Transformations 


![FK](https://raw.githubusercontent.com/Faisal-f-rehman/ROCO_224/master/ManipulatorDesignProject/maths/matlab%20screenshots/FKin.PNG)

## Matlab 
**Please zoom in to read**
<br>
			Forward Kinematics and Jacobian Matrix

![Forward Kinematics and Jacobian Matrix](https://github.com/Faisal-f-rehman/ROCO_224/blob/master/ManipulatorDesignProject/maths/matlab%20screenshots/fk1.png)

<br><br>

			Inverse Kinematics by Psuedo Inverse

![IK](https://raw.githubusercontent.com/Faisal-f-rehman/ROCO_224/master/ManipulatorDesignProject/maths/matlab%20screenshots/ik_iterations.png)

<br><br>

				Matlab main.m

![kinematic main.m](https://raw.githubusercontent.com/Faisal-f-rehman/ROCO_224/master/ManipulatorDesignProject/maths/matlab%20screenshots/main.m.png)

<br><br>

				Results

[![](https://raw.githubusercontent.com/Faisal-f-rehman/ROCO_224/master/ManipulatorDesignProject/maths/IK_youtube_pic.png)](https://www.youtube.com/watch?v=hpOUysoVidw)

