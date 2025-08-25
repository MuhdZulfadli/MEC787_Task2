# Week 2 Task: ROS2 Topics & Teleoperation with TurtleBot3

## Overview
This task demonstrates ROS2 communication concepts using TurtleBot3. The objectives are:
- Launch a TurtleBot3 simulation in Gazebo.
- Teleoperate the robot.
- Explore key ROS2 topics and messages.
- Visualize data in RViz2.
- Record and replay data using `ros2 bag`.

**Topics explored:**
- `/cmd_vel` → velocity commands
- `/odom` → position & orientation
- `/scan` → LIDAR sensor data
- TF → coordinate frames for visualization

---

## 1. Launch Simulation
```bash
export TURTLEBOT3_MODEL=burger
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
````

## 2. Teleoperate Robot

```bash
ros2 run turtlebot3_teleop teleop_keyboard
```

* Use **W/A/S/D/X** keys to move the robot.
* Ensure the robot moves in Gazebo before recording.

## 3. Record Bag Data

```bash
ros2 bag record /cmd_vel /odom /scan /tf
```

* Move the robot for \~2 minutes while recording.
* Press **Ctrl+C** to stop recording.

## 4. Replay Bag

```bash
ros2 bag play rosbag2_2025_08_25-10_49_01
```

* Open RViz2 to visualize `/odom`, `/scan`, and TF:

```bash
rviz2
```

* Add the following displays: **TF**, **RobotModel**, **Odometry (/odom)**, **LaserScan (/scan)**.
* If the robot looks static, check that `/odom` and TF were recorded properly.

## 5. Explore Topics

```bash
ros2 topic list
ros2 topic info /cmd_vel
ros2 topic echo /odom --once
ros2 topic hz /scan
```

## 6. Inspect Message Structures

```bash
ros2 interface show geometry_msgs/msg/Twist
ros2 interface show sensor_msgs/msg/LaserScan
```

## 7. Screenshots

* [ ] `img/gazebo.png` → Gazebo robot spawn
* [ ] `img/teleop.png` → Teleop terminal
* [ ] `img/topic_list.png` → Topic list
* [ ] `img/odom_echo.png` → /odom messages
* [ ] `img/scan_hz.png` → /scan frequency
* [ ] `img/rviz.png` → RViz2 visualization
* [ ] `img/bag_replay.png` → Bag replay in RViz2

## 8. Bag Info

```bash
ros2 bag info rosbag2_2025_08_25-10_49_01
```

* Save output as `ros2_bag_info.txt`.

## 9. Reflection

* See `reflection.pdf` for a 200-word reflection.
* Key question: *How `/cmd_vel`, `/odom`, `/scan`, and TF work together to enable robot navigation, and what challenges occur if topics are missing?*

## 10. Video Demo

* `video/teleop_demo.mp4` → Show Gazebo, teleoperation, and RViz2 visualization.

## 11. Notes / Tips

* Always record `/odom` and TF if you want the robot motion visible in RViz2.
* Teleop **before recording**, otherwise the robot will stay static.
* Bag replay keyboard shortcuts:

  * **SPACE** → Pause/Resume
  * **→** → Play next message
  * **↑** → Increase rate 10%
  * **↓** → Decrease rate 10%
