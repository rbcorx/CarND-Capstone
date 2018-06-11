# udacity-carnd-capstone
Capstone project of the Udacity Self-Driving Car Nanodegree: Programming a Real Self-Driving Car. 

# System Architecture
The following is a system architecture diagram showing the ROS nodes and topics used in the project.
![architecture](https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59b6d115_final-project-ros-graph-v2/final-project-ros-graph-v2.png)

## Traffic Light Detection
Since we know the locations of the traffic lights and the vechile, we can reduce the classification problem to transformation and detection problem. As color is easier to detect in HSV space and in this use case, red light is important, having two different ranges in the HSV space. As we want to be sensitive to red light, I include both ranges in the the mask. Further improvements can be made when dealing with unknown locations and complex data by applying Deep NN solutions.

## Waypoint Updater
Waypoint updater updates target velocity property of each waypoint based on traffic light and obstacle detection data. The target veloicty at normal situdation is given from `waypoint_loader` node. If the red light is detected, we generate stop trajectory considering vehicle's deacceleration limits. 

## Waypoint Follower
The longitudinal target velocity was set in `waypoint_updater` node. This node determines the target yaw_rate to keep the lane by using pure-pursuit algorithm.

## DBW(Drive-By-Wire) Node
This node calculates throttle, brake and steering angle to follow longitudinal and lateral trajectory simultaneously. This is achieved using a PID controller to calculate throttle and brake based on the differences between the current velocity and the target velocity. The PID controller is based on cross-track error (cte) to calculate appropriate steering command.

# Contributor

| Name | E-mail | 
| ------ | ------ | 
| Raunak Bhandari | ronniebhase@gmail.com |
