# Tinker
# *Flexible, and Ready to Move: Your Cartoon-Style Bipedal Robot!*


## 📢 **UPDATE V1.1**
> Please visit [README_V1.1.md](https://github.com/Yuexuan9/Tinker/blob/main/assemble/README_V1.1.md) for the latest version of documentation.

<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/2025040901.PNG" width="300" />
</div>

---

## Hardware Assembly
Tinker V1 version simulates the primary structure of Disney's biped robot, featuring 5 degrees of freedom (DoF) per leg and powered by a 24V battery. The total weight is approximately 10 kg. It uses CAN servo communication to achieve high real-time 1KHz low-level communication and can deploy reinforcement learning algorithms for driving. The head uses a 3-DoF servo to adjust pitch and yaw angles, supporting SDK for secondary development:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm1.PNG" width="300" />
</div>

[Robot Reference Model](https://drive.google.com/file/d/1_RZISD0UwsXpW5vh1HhzGIpm2f5NXvxn/view?usp=share_link)

The assembly process can be referred to in the file: [TinkerV1_assemblyproduce.pdf](https://github.com/Yuexuan9/Tinker/blob/main/assemble/TinkerV1_assemblyprocedure.pdf)

- ### Assembling the Middle Frame
First, complete the assembly of the middle frame structure. Before installation, ensure all motors are calibrated and parameters configured. During assembly, connect the CAN and power lines of each motor to facilitate welding after assembly:

| Motor   | CAN ID | Model |
|---------|--------|-------|
| Yaw     | 1      | 6006  |
| Roll    | 2      | 8006  |
| Thigh   | 3      | 8006  |
| Shin    | 4      | 8006  |
| Ankle   | 5      | 6006  |

The motor ID sequence for both legs is consistent, as shown below:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm2.PNG" width="300" />
</div>

First, install the power board and base plate, and complete the installation of the support base. Note that the notch at the back of the base plate is where the battery is located, and the PCB 24V DC terminal is located here:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm3.PNG" height="300" />
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm4.PNG" height="300" />
</div>

Then use M4 screws to install the bottom support:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm5.PNG" width="300" />
</div>

Install the top plate and two 6006 motors. Align the debugging port with the notch:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm6.png" width="300" />
</div>

Mount the aluminum structure on the 6006 motors:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm7.png" width="300" />
</div>

Install two 8008 motors and aluminum supports to assemble with the above 6006 motors:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm8.png" width="300" />
</div>

Complete the installation of the thigh motors and aluminum structures. The roll structure should bend downwards. Note that when installing the thigh motors, there is a separate carbon fiber support:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm9.png" height="300" />
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm10.png" height="300" />
</div>

Assemble the thigh structure with the roll structure, ensuring the orientation of the head and aluminum structure:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm11.png" height="300" />
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm12.png" height="300" />
</div>

After completing the assembly of the 6 motors, use carbon fiber beams to assemble the upper and lower plates, finishing the middle frame assembly:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm13.png" height="300" />
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm14.jpeg" height="300" />
</div>

- ### Assembling the Thighs
After completing the middle frame assembly, proceed with the thigh assembly. Ensure all motor wires are connected properly, and check the orientation of the head and thigh arm cutouts:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm15.png" width="300" />
</div>

Once the thigh carbon plates are installed, install the left and right cable protection structures. Pay attention to the notch position and ensure the motor wires are routed correctly:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm16.png" width="300" />
</div>

- ### Assembling the Shin
Assembling the shin is relatively simple. Secure the motor and route the cables as shown in the diagram:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm17.png" width="300" />
</div>

Route the foot-end cables through the shin's carbon plate groove, bundling them with the shin motor cables:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm18.png" width="300" />
</div>

Finally, install the foot end with a separate carbon fiber support:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm19.png" width="300" />
</div>

- ### Installing the Battery
Install the battery and the chest's printed structure:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm20.png" width="300" />
</div>

Route the battery power cables upwards, and connect the power wiring and air switch input/output connections. Install the air switch and its mounting structure:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm21.png" width="300" />
</div>

- ### Installing the Main Control Board
Before installing the main control system, ensure all control units are configured. Install the Odroid controller, router, and servo driver board according to the diagram:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm22.png" width="300" />
</div>
Mount the Jetson Nano on the back using the printed support structure:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm23.png" width="300" />
</div>

After completing the main control system's hardware installation, secure it to the body using the support structure:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm24.png" height="300" />
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/bm24.jpeg" height="300" />
</div>
With the above steps, the Tinker assembly is complete. Before installing the head, perform electrical welding and gait testing. Only install the head once no errors are detected to avoid damage from falls.

## Electrical Wiring Diagram
After completing the mechanical structure assembly, begin electrical wiring. The following diagram shows the power supply for the entire Tinker. The CAN and power wires of a single leg can be merged into one path inside the body and plugged into the main controller and distribution board:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/whiteboard_ag1.png" width="500" />
</div>

For communication cables, the left and right legs' CAN lines are combined into one. On the STM32 carrier board, the left leg connects to CAN1, and the right leg connects to CAN3. The servo board is connected via UART2, with the IO definitions shown on the silkscreen. Ensure TX on the servo board is connected to TX on the carrier board, and RX to RX.
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/whiteboard_ag2.png" height="300" />
</div>

## Prototype Testing
1. After completing hardware assembly and servo system installation, verify polarity before powering up. Connect to the router, check the IP of the main controller, and start the three control programs either manually or automatically.
2. Open the upper computer to confirm that data feedback is normal, with joint angles consistent with the coordinate system definitions. You can use Rviz to check URDF for the correct motor directions:
You can download the file from [this Google Drive link](https://drive.google.com/file/d/1ZrNIlMniP54uTsEq2xIo4VjpPapP6Isk/view?usp=drive_link).

```bash
roslaunch urdf_tutorial display.launch model:=/home/pi/Downloads/LocomotionWithNP3O-master/resources//tinker/urdf/tinker_urdf.urdf
```
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/ag1.png" height="300" />
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/ag2.png" height="300" />
</div>

3. Insert the game controller, open the upper computer, and place the robot on a flat surface to calibrate the joints. Ensure symmetry between the legs and follow the steps for joint alignment. Avoid wearing sleeves during calibration to prevent errors.
Place the robot base tightly against the ground, with the left and right legs symmetrical, and fasten the foot end to the thigh motor.
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/ag3.jpeg" height="300" />
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/ag4.jpeg" height="300" />
</div>
Press your toes tightly with your hands, keep your thigh motor close to the table, and align your left and right legs.
The left and right thigh arms are pressed backward towards the body structure to achieve a state of outward expansion and inward contraction. Note that the thigh arms must be pushed against the crossbeam structure connected to the upper and lower boards.
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/ag5.jpeg" width="500" />
</div>
Make sure the robot is connected, press the key to reset the main control, wait for the posture to stabilize, and calibrate the acceleration and gyroscope of the motor with the upper computer sensor.
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/ag6.png" width="500" />
</div>
Long press the remote control ` Y ` button, confirm whether the angle is reset after hearing the buzzer sound. It is recommended to repeat the first calibration 2-3 times to ensure that all joint calibration is completed.

4. Re-power the robot (important: some motors need re-powering after calibration). Lift the robot, hold down the ` X ` button, and check if the legs retract to the crouched position. The robot should stand when placed on the ground.

## Installing the Head
Once electrical testing and gait tests are complete, proceed with head installation. Before installing the neck, reset all servos to 0 positions using the upper control software. Then, install the servos in the following angles and positions, ensuring the correct servo IDs and models:
| Motor      | Servo ID | Model  |
|------------|----------|--------|
| Pitch 1    | 0        | SCS40  |
| Pitch 2    | 1        | SCS40  |
| Yaw        | 2        | SCS125 |

<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/ag7.png" height="300" />
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/ag8.png" height="300" />
</div>

After soldering the servo power wires and combining them into one path, connect them to the servo driver board.

## Full System Test
Once the head and the robot are fully assembled, perform a complete system test:

1. **Power On**: 
   Ensure that joint calibration is complete before powering up. Lift the robot with its legs vertical and hold down the ` X ` button. The robot should retract its legs into a crouched position. If everything is functioning correctly, the robot should stand stably on the ground using position control loops.
   
   > If there are issues with the motor rotation, press the `↓` button to cut off power.

2. **Start RL Program**: 
   Refer to previous instructions to start the RL software, and verify that data is refreshing correctly.

3. **Gait Control**: 
   In standing mode, press the X button again to activate RL-based gait control. The left joystick controls XY velocity, and the rear triggers control the yaw direction. If the robot operates normally, you can control its movement.

4. **Head Control**: 
   The right joystick can be used to control the head angle remotely. In disabled mode, pressing the A button enters recording mode, allowing you to move the head manually. Pressing the B button stops recording, and pressing Start will automatically play back the motion (this feature is still being updated). The recorded file is saved in the `Motion` folder as a `.txt` file.
