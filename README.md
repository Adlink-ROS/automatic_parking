# Thie package is under construction!

---

# automatic_parking
This automatic_parking package can be divied into two parts, pattern recognition and moving to goal. In pattern recogintion, this package depends on laser_line extraction package to turn laser point clouds into line segments. Then, this package will go through these line segments to find the designed pattern and broadcast a frame, dock frame. After the frame being populated, the robot will move to the dock and the strategy is shown as the gif below. The ROS version is Foxy.
<img src="https://github.com/CuteJui/automatic_parking/blob/master/readme_resource/docking_demo.gif"/>


## Dependency
- [`Laser Line Extraction`](https://github.com/H-HChen/laser_line_extraction)

## Usage
Creat a new work space
```
mkdir -p docking_ws/src
cd docking_ws/src
```
Clone the Laser Line Extraction package.
```
git clone https://github.com/H-HChen/automatic_parking.git
```
Clone the Laser Line Extraction package.
```
git clone https://github.com/H-HChen/laser_line_extraction.git
cd ..
```
Clone the Laser Line msgs package.
```
git clone https://github.com/H-HChen/laser_line_msgs.git
cd ..
```
Build the package.
```
colcon build --symlink-install 
```
Launch the package.
```
ros2 launch auto_dock auto_foxy.launch.py 
```

## Topics
### Subscribed Topics
- `/line_segments` (laser\_line\_extraction/LineSegmentList)

### Published Topics
- `/cmd_vel` (geometry_msgs/Twist)

## Parameters
### Pattern Angle Definition
<img src="https://github.com/CuteJui/automatic_parking/blob/master/readme_resource/pattern_angle.png" width="467" height="290"/>

### Pattern Parameters Definition
<img src="https://github.com/CuteJui/automatic_parking/blob/master/readme_resource/pattern_parameters.png" width="435" height="270"/>

- `pattern_angle1` (default: 3.84)
	- Theta 1 as shown in pattern angle definition. Note that the unit is radian.
- `pattern_angle2` (default: 1.57)
	- Theta 2 as shown in pattern angle definition. Note that the unit is radian.
- `pattern_angle3` (default: 3.84)
	- Theta 3 as shown in pattern angle definition. Note that the unit is radian.
- `detect_angle_tolerance` (default: 0.2)
	- The maximum difference between detected angle and pattern angle(pattern\_angle1, pattern\_angle2, pattern\_angle3)
- `group_dist_tolerance` (default: 0.15)
	- The maximum distance between two line to be recognize as a part of pattern. Such as the distance between the end point of detected vector b and the start point of detected vector a should smaller than group\_dist\_tolerance to be consider as a part of pattern.
- `laser_frame_id` (default: "laser_frame")
	- The laser frame of the robot.
- `base_frame_id` (default: "base_link")
	- The base frame of the robot.
- `min_v` (default: 0.1)
	- Minimum linear velocity of the robot.
- `min_w` (default: 0.1)
	- Minimum angular velocity of the robot.
- `max_v` (default: 0.3)
	- Maximum linear velocity of the robot.
- `max_w` (default: 0.3)
 	- Maximum angular velocity of the robot.
- `threshold_v` (default: 0.3)
	- The threshold of changing between minimum and maximum linear velocity.
- `threshold_w` (default: 0.4)
	- The threshold of changing between minimum and maximum angular velocity.
- `dist_to_dock` (default: 0.25)
	- Distance to the dock frame.
- `dist_to_center` (default: 0.03)
	- Distance to the center.

## Model
There are models of dock for Gazebo simulation in "Model" file.
### Dock 1
The size of dock 1 is shown as the picture below.                                                                       
<img src="https://github.com/CuteJui/automatic_parking/blob/master/readme_resource/dock_1.png" width="418" height="219"/>

### Dock 2
The size of dock 2 is shown as the picture below.                                                                      
<img src="https://github.com/CuteJui/automatic_parking/blob/master/readme_resource/dock_2.png" width="460" height="238"/>
