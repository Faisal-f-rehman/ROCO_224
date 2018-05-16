# IMPLEMENTATION WITH MATLAB AND ROS

For demonstration purposes, as our inverse kinematics could not be resolved we decided to use motion planning with forward kinematics instead.

<br><br>

## ROS SETUP

Before we could jump into matlab and create all the algorithms we had to create ROS package and nodes. This included the following files:

				controller_manager.launch
This is a launch file that can be run by the roslaunch command in the terminal. This file handles all the serial communications between nodes:  

```XML
<!-- -*- mode: XML -*- -->

<launch>
    <node name="dynamixel_manager" pkg="dynamixel_controllers" type="controller_manager.py" required="true" output="screen">
        <rosparam>
            namespace: dxl_manager
            serial_ports:
                pan_tilt_port:
                    port_name: "/dev/ttyUSB0"
                    baud_rate: 57600
                    min_motor_id: 1
                    max_motor_id: 25
                    update_rate: 20
        </rosparam>
    </node>
</launch>
```

<br><br>

				start_meta_controller.launch
This again is a launch file that runs the tilt.yaml file which contians all the joint/servo states. I decided to meta controller for single and coupled double joints:  

```XML
<!-- -*- mode: XML -*- -->

<launch>
<!-- Start tilt joint controller -->
    <rosparam file="$(find my_dynamixel_tutorial)/tilt.yaml" command="load"/>
    <node name="controller_spawner" pkg="dynamixel_controllers" type="controller_spawner.py"
          args="--manager=dxl_manager
                --port pan_tilt_port
                joint1_controller                       
                joint4_controller                       
                joint5_controller
                joint6_controller
		joint7_controller
                joint8_controller
                "
          output="screen"/>
          
  <!-- Start joints trajectory controller controller -->
    <rosparam file="$(find my_dynamixel_tutorial)/joints_trajectory_controller.yaml" command="load"/>
    <node name="controller_spawner_meta" pkg="dynamixel_controllers" type="controller_spawner.py"
          args="--manager=dxl_manager
                --type=meta
                f_arm_controller
                                                
                "
                
                          output="screen"/>

  <!-- Start dual_motor joint controller -->
    <rosparam file="$(find my_dynamixel_tutorial)/dual_motor.yaml" command="load"/>
    <node name="dual_motor_controller_spawner" pkg="dynamixel_controllers" type="controller_spawner.py"
          args="--manager=dxl_manager
                --port pan_tilt_port
                dual_motor_controller"
          output="screen"/>
</launch>

```
<br><br>
 
				tilt.yaml

This is a ROS node of type std_msg and size float 64 bits, that can be published to, to send joint angles and subscribed to, for reading the state of the servos
 
```yaml
joint1_controller:
    controller:
        package: dynamixel_controllers
        module: joint_position_controller
        type: JointPositionController
    joint_name: shoulderA
    joint_speed: 0.5
    motor:
        id: 1
        init: 0
        min: 0
        max: 4095
        
joint4_controller:
    controller:
        package: dynamixel_controllers
        module: joint_position_controller
        type: JointPositionController
    joint_name: shoulder_B
    joint_speed: 0.5
    motor:
        id: 5
        init: 0
        min: 0
        max: 4095
        
joint5_controller:
    controller:
        package: dynamixel_controllers
        module: joint_position_controller
        type: JointPositionController
    joint_name: elbow
    joint_speed: 0.5
    motor:
        id: 6
        init: 0
        min: 0
        max: 4095
        
joint6_controller:
    controller:
        package: dynamixel_controllers
        module: joint_position_controller
        type: JointPositionController
    joint_name: wristA
    joint_speed: 0.5
    motor:
        id: 9
        init: 0
        min: 0
        max: 4095

joint7_controller:
    controller:
        package: dynamixel_controllers
        module: joint_position_controller
        type: JointPositionController
    joint_name: wristB
    joint_speed: 0.5
    motor:
        id: 10
        init: 0
        min: 0
        max: 4095

joint8_controller:
    controller:
        package: dynamixel_controllers
        module: joint_position_controller
        type: JointPositionController
    joint_name: wristC
    joint_speed: 0.5
    motor:
        id: 12
        init: 0
        min: 0
        max: 4095

dual_motor_controller:
    controller:
        package: dynamixel_controllers
        module: joint_position_controller_dual_motor
        type: JointPositionControllerDual
    joint_name: dual_motor
    joint_speed: 0.5
    motor_master:
        id: 3
        init: 0
        min: 0
        max: 4095
    motor_slave:
        id: 4

``` 

<br><br>


## MATLAB

First step in Matlab was to setup ROS by creating publishers and subscribers to allow us to communicate with the servos:  

				ROS initiation function
![ROS INIT MATLAB](https://raw.githubusercontent.com/Faisal-f-rehman/ROCO_224/master/ManipulatorDesignProject/maths/matlab%20screenshots/ros_init.png)
		
<br><br>

Second step was to create a function for publishing joint angles that would be easier to call recursively:  

				Joint Angle Publisher Function
![Joint angle pub](https://raw.githubusercontent.com/Faisal-f-rehman/ROCO_224/master/ManipulatorDesignProject/maths/matlab%20screenshots/ros_joint_angles.png)

<br><br>

Finally main.m file to recursively call the joint angle function with different joint positions for each trajectory:

				main.m
![main.m trajectory](https://raw.githubusercontent.com/Faisal-f-rehman/ROCO_224/master/ManipulatorDesignProject/maths/matlab%20screenshots/Motion%20Planning%20Main.png)

<br><br>

			
				Demonstrational video

[![](https://raw.githubusercontent.com/Faisal-f-rehman/ROCO_224/master/ManipulatorDesignProject/media_man/youtube%20pic.PNG)](https://www.youtube.com/watch?v=rU_hAAqRPvU)

