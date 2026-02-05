# Instructions for the user

The purpose of this exercise is to get familiar with the data collection process in a bimanual Franka Research 3 setup using the Gello arms teleoperation devices. In this exercise, you will try two cloth manipulation tasks:

- Fold the cloth: the cloth is positioned flat/crumpled on the table, and the goal is to fold it twice along the center line.
- Flatten the cloth: the cloth is positioned crumpled on the table, and the goal is to flatten it as much as possible. You can try 3 techniques to flatten the cloth:
    1. Flattening by stretching the cloth from its edges.
    2. Grab the cloth, swing it and place it back on the table in a flattened manner.
    3. Use the edge of the table to help flatten the cloth.

## How to collect an episode?

You can manage the whole process through Franka Data Collection UI. The following are the step-by-step instructions to collect an episode. You need at least 2 people to do this; in this scenario, person A manages the episode start/stop at the workstation, and person B does the teleoperation:

1. (For Person A) Navigate to the [Franka Data Collection UI](localhost:4000), it is one of the bookmarks on the browser. Check Picture ???
2. (For Person A) Make sure all boxes in the system status panel are green. (Don’t mind the Gripper boxes as they should turn green when starting teleoperation.)
3. (For Person A) Check whether all camera streams are working. Don't mind the lag/jitters on data collection camera  streams. If you want to see a smoother stream of the wrist or head cameras, you can view it directly in the ROS rqt viewer. Check the [Notes](#notes) section below for instructions. 
4. (For Person A) Click on `Start Teleoperation`.
5. (For Person B) Should pick up the Gello arms carefully and adopt a posture similar to that of the Franka arms and hold that posture.
6. (For Person A) While person B is holding still, click on `Reset Robot Position` in the UI; this adjusts the robot arms to Gello arm configuration, and the robot is ready to be teleoperated.
It is important to note that sudden and rapid movements by the teleoperator will cause the robot to enter emergency lock mode. In such a case, activate the emergency brakes, click on `Stop Teleoperation`, and inform your operator guide to resume operation. 

7. (For Person A) When ready, select your task using `Change Tasks` then press `Start Recording`, 
8. (For Person B) Perform their desired task using the Gello arms.
9. (For Person A) Upon finishing the task, click `Stop Recording`. A menu will appear, allowing you to decide whether to save or discard your data. Note that the system is still in the teleoperation mode.
10. (For Person A) Click on `Stop Teleoperation`
11. (For Person B) Insert back the Gello arms into their calibration rods. Check Picture ??? to see the correct configuration pose.

## How to see your collected data?

The data is recorded with MCAP format - a file format for multimodal log data. The format supports viewing and playing the data using the `rosbag` ROS package. 

### Locate the collected data

#### Step 1: Find your episode in the UI
1. In the Franka Data Collection UI, navigate to the `EPISODES` tab
2. Using the date and time information, locate your data in the collected data list
3. Copy the data name hash (e.g., `Episode ...`)

#### Step 2: Access the data files

The collected data is saved in `/data_farm` on the workbench.

```bash
cd /data_farm
```

## Notes

- Don’t mind the lag/jitters on data collection camera  streams, if you want to see a smoother stream of the wrist or head cameras, you can viewing in ROS rqt directly via:
  1. Press `Ctrl + alt + T` to open a new terminal window.
  2. Type `terminator -l debugging` to open the debugging workspace.
  3. Type `docker compose exec ros-debug-franka bash -lc 'source /opt/ros/jazzy/setup.bash && rqt'` to open the ROS rqt viewer application
  4. In rqt viewer select `Plugins` -> `Visualization` -> `Image view`. A grey image should appear.
In the dropdown menu of the rqt viewer select the ROS topic of the camera you wish to view:
Left wrist camera: `/wrist_camera_left/D405/color/image_rect_raw`
Right wrist camera: `/wrist_camera_right/D405/color/image_rect_raw`
Head camera: `/zed/zed_node/rgb/image_rect_color`


- If the franka arm is blinking yellow, this is a warning indicating that one or some of the joints are near their limits.

- Aggressive and too dynamic motions may cause the arms to activate their emergency mode and get locked, in such case:
  - Stop teleoperating via the Franka Data Collection UI.
  - If the Franka arms are blinking a red light, that means the emergency locks are activated and you need to inform your helper operator to resume data collection.
