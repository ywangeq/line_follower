# Line follower with feedback control
### Purpose
>The purpose of this lab is to create a behavior that will enable your
robot car to follow a line with different color which you set using single
camera in a PID control loop.

### Lab Objectives
By following the directions in this lab, you are expected to achieve
the following:

 - Implement a feedback controlled servo behavior for line-following
 in a behavior-based control structured program.
 - Experiment with implementing PID control and tune the gains to
achieve the best performance
 - Fine tune the control so that the robot can successfully follow a
line as described in the lab

### Required Equipment
1. Jetson robot platform
2. Ros environment
3. Opencv2.4.13

### Programming
>1.Using blurs, threshold, canny edge detection and hough lines
transform to help vision find the line.
<p>2. Calculates the center of mass. For estimating the deviation of
the robot from the line, we will only consider the x coordinate
of the center of mass. There are two cases that we should consider : when the line is visible and when is is not. The "**m00**" value corresponds to the area of the segmented region. If "**m00**" is greater than 6000, set "**error_msg.data**" to be the x coordinate of the certer of mass minus the image width divided bt 2. When ""**m00**"" is less than 6000, than the line is not signficantlt present in the image; in this situation, set the "**error_msg.data**" to the special value "12345" to signla that the line is not present.
<p>Use 'line_error_pub' to publish the current error_msg.
><p> 3. Implementing PID
 </p> in the "**line_pid.cpp**", there is a function call "**errorCallback**", which set the velocity values to 0 when the special value "12345" is received
<p> when the eoor value is not the special，we need to set the velocity of the robot to ensure that the rebot maintains its course on the line. Let's us keep the robot moving forward by setting the linear velocity to you like.
<p> Then consider the requirements for PID - the current error, integral of error, and derivatie of error. Update the "**integral_error**" value by adding the current error. Now set the angular velocity:
<p> vel_msg.angular.z=-(Kp*cur_error+Kd*derivative_error+Ki*integral_error);

### Steps
>To perform this lab, you will need to get the lab_line_follower template into your catkin workspace "**catkin_ws/src**"
- <p> first you need to open the terminal by ctrl+alt+t.
- <p> to get into the catkin workspace ,run the command:  
   `cd ~/catkin_ws/src `
- <p> `git clone https://github.com/ywangeq/line_follower.git`

>To build the code, use the following command when you are in "**workspace**"

- `cd ~/catkin_ws/`

>and then run the next command line to build the source code

- `catkin_make`

> After the build, you can run the system by executing the following command

- `roslaunch lab7_line_follower lab7.launch`

### ros topic show
> to see the topics which you have published, you can run next command line in the terminal
- `rostopic list`
> you can get the information which is published in by this command
- `rostopic echo /xxx/xxx`
