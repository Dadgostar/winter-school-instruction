# winter-school-instruction

# Instructions for the user

The purpose of this exercise is to get familiar with the data collection process in a bimanual Franka Research 3 setup using the Gello arms teleoperation devices. In this exercise, you will try two cloth manipulation tasks:

- Fold the cloth.
- Flatten the cloth.

## How to collect an episode?

You can manage the whole process through Franka Data Collection UI. The following are the step-by-step instructions to collect an episode. You need at least 2 people to do this; in this scenario, person A manages the episode start/stop at the workstation, and person B does the teleoperation:

1. (For Person A) Navigate to the Franka Data Collection UI, it is one of the bookmarks on the browser. Check Picture ???.
2. (For Person A) Make sure all boxes in the system status panel are green. (Don't mind the Gripper boxes as they should turn green in the next step.)
3. (For Person A) Check whether all camera streams are working.
4. (For Person A) Click on "Start Teleoperation".
5. (For Person B) should pick up the Gello arms carefully and adopt a posture similar to that of the Franka arms and keep that posture.
6. (For Person A) While person B is holding still, click on "Reset Robot Position" in the UI; this adjusts the robot arms to Gello arm configuration, and the robot is ready to be teleoperated.

**Important Note:** It is important to note that sudden and rapid movements by the teleoperator will cause the robot to enter emergency lock mode. In such a case, activate the emergency brakes, click on "Stop Teleoperation", and inform your operator guide to resume operation.

7. (For Person A) When ready, select your task using "Change Tasks" then press "Start Recording."
8. (For Person B) Perform their desired task using the Gello arms.
9. (For Person A) Upon finishing the task, click "Stop Recording". A menu will appear, allowing you to decide whether to save or discard your data. Note that the system is still in the teleoperation mode.
10. (For Person A) Click on "Stop Teleoperation".
11. (For Person B) Insert back the Gello arms into their calibration rods. Check Picture ??? to see the correct configuration pose.

## How to see your collected data?

The data is recorded with mcap format. The collected episode is accessible via _____.

## Notes

- Don't mind the lag/jitters on data collection camera streams, if you want to see a smoother stream of the wrist or head cameras, you can viewing in "rqt" directly via:
  - Press Ctrl + alt + T to open a new terminal window.
  - Type "terminator -l debugging" to open the debugging workspace.
  - Type `docker compose exec ros-deb-franka bash`.

- If the franka arm is blinking yellow, this is a warning indicating that one or some of the joints are near their limits.

- Aggressive and too dynamic motions may cause the arms to activate their emergency mode and get locked, in such case:
  - Stop teleoperating via the Franka Data Collection UI.
  - If the Franka arms are blinking a red light, that means the emergency locks are activated and you need to inform your helper operator to resume data collection.
