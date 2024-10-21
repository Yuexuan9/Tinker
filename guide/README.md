# Tinker
## _Flexible, and Ready to Move: Your Cartoon-Style Bipedal Robot!_
Tinker primarily uses reinforcement learning for control. Below is the complete tutorial for deploying the robot. If the corresponding hardware modules are provided by RoboHome, you can skip the relevant sections.

## Recommended Setup and Debugging Steps
1. **Prepare Materials**: Follow the Tinker BOM checklist.
2. **Configure Odroid Operating System**.
3. **Flash STM32 Firmware**.
4. **Configure STM32 Parameters**.
5. **Download and Configure Odroid Motion Control Program** and set up auto-start.
6. **Motor Configuration**: Modify motor ID and parameters.
7. **Servo Configuration**: Reset servo IDs to 0.
8. **Assemble Tinker V1**: Follow the Tinker V1 assembly guide.
9. **Gait Test - Leg Retraction**.
10. **Run RL Model**: Set up training and deployment environment.
11. **Gait Test - RL Server Mode**.
12. **Configure Jetson Nano Deployment Environment**.
13. **Gait Test - Onboard RL Mode**.
14. **Further Development**: Explore Tinker's extensibility with external sensors and hardware.

---

## Odroid Controller System Configuration

  This guide provides the steps to install the 5.10 RT kernel on the Odroid C4 for real-time communication with the STM32 control board. The steps involve downloading the required image, burning it to an SD card, updating the system, and installing the necessary development tools.
  
  [2_IP303 Instruction](https://docs.google.com/document/d/1vPL9UoZW20sJJxURa68NVbsvmoNdLAVW/edit?usp=drive_link&ouid=104255196359889104654&rtpof=true&sd=true)

  To set up the system, use the provided instructions to install the RT real-time patch for the 5.10 kernel version. Reference [this forum post](https://forum.odroid.com/viewtopic.php?f=55&t=41129) for more details.
  Since the RT patch is only compatible with the 5.10 kernel version, you will need to download the 1218 version of the image (as the original post linked the 5.11 version, which is not supported). 
  
  Download the image from the following URL:
  [http://ppa.linuxfactory.or.kr/images/raw/arm64/focal/](http://ppa.linuxfactory.or.kr/images/raw/arm64/focal/)
  
  Once downloaded, burn the image to your SD card and insert it into the Odroid system.
  
> Username: `odroid` Password: `odroid`

<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug1.PNG" height="300" />
</div>
  
  Since the system is a server version, it cannot connect to the internet and has no text editor installed. Therefore, the first priority is to update the system and install the basic development environment. Since the Odroid C4 does not have Wi-Fi and is directly connected via Ethernet, it lacks the ifconfig tool to check its own IP address, making it impossible to connect to the internet. Thus, I will use a router relay solution here: 

```bash
sudo apt update
sudo apt dist-upgrade
```
  
```bash
sudo apt install linux-image-5.10.0-odroid-rt-arm64
sudo reboot
```

After reboot, check if the RT kernel is running:

```bash
uname -a
```

You should see output similar to: 

```
Linux focal-server 5.10.0-odroid-rt-arm64 #1 SMP PREEMPT_RT Ubuntu 5.10.0-202012062208~focal (2020-12-06) aarch64 aarch64 aarch64 GNU/Linux
```

Install the necessary development tools such as `nano`, `ifconfig`, `cmake`, and others:

```bash
sudo apt-get install g++
sudo apt-get install cmake
sudo apt install net-tools
```

---

## Programming the STM32 Carrier Board

To achieve CAN communication, SPI is used for high-speed communication between Odroid and the STM32 carrier board. After installation, program the STM32 using the SWD interface with ST-LINK Utility:

**V1:** The V1 version currently only provides firmware.

[F407_FC.hex](https://drive.google.com/file/d/1Gf5wbCc6sO4q2qFnuwNtqjt-A1DhvB2R/view?usp=drive_link)

---
## Motor Configuration

The Tinker uses the Dagu motor as its main execution unit, and it requires the accompanying upper computer for configuration. One of the most important settings is to modify the CAN Timeout to 0. The motor sequence for the left and right legs is as follows:

| Motor         | CAN ID | Model |
|---------------|--------|-------|
| Yaw Rotation  | 1      | 6006  |
| Roll Rotation | 2      | 8006  |
| Thigh         | 3      | 8006  |
| Calf          | 4      | 8006  |
| Ankle Joint   | 5      | 6006  |

The internal configuration parameters for the individual motors are shown in the figure below. The corresponding coefficients in the control amplitude need to match the parameters listed below. Additionally, complete the settings for timeout, ID, and current loop parameters:

```bash
case DM_6006://Small flat motor
P_MIN_CAN_MIT[i] =-12.5f;
P_MAX_CAN_MIT[i] = 12.5f;
V_MIN_CAN_MIT[i] =-45.0f;
V_MAX_CAN_MIT[i] = 45.0f;
T_MIN_CAN_MIT[i] =-12.0f;
T_MAX_CAN_MIT[i] = 12.0f;
break;
case DM_8006 ://Gear ratio 6 motor              
P_MIN_CAN_MIT[i] =-12.5f;
P_MAX_CAN_MIT[i] = 12.5f;
V_MIN_CAN_MIT[i] =-45.0f;
V_MAX_CAN_MIT[i] = 45.0f;
T_MIN_CAN_MIT[i] =-20.0f;
T_MAX_CAN_MIT[i] = 20.0f;
motor_chassis[i].motor.anal_type=M_MIT;
break;
```

<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug2.png" height="500" />
</div>

It is recommended to update the corresponding 8006 motors to the latest version of the same firmware.

<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug3.png" height="200" />
</div>

[Damiao.rar](https://drive.google.com/drive/folders/1KnC-RKWRdck51djY4cLO2_fAsvc746Mc?usp=drive_link)

---

## Servo Configuration

If Tinker is equipped with a head, you need to configure the servos on the bus. Use the Feetech bus control module to first reset the zero position of the 3 servos, then configure the bus IDs in sequence:

| Motor           | Servo ID | Model  |
|-----------------|----------|--------|
| 1-Axis Pitch    | 0        | SCS40  |
| 2-Axis Pitch    | 1        | SCS40  |
| Yaw (Heading)   | 2        | SCS125 |

<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug4.png" height="500" />
</div>

[FD19.8.1.rar](https://drive.google.com/file/d/1EDrdxpF2Ymz0OfZ5OsW3DxpGYs4qwE90/view?usp=drive_link)

---

## STM32 Carrier Board Configuration

The STM32 carrier board is accompanied by a custom-developed upper computer. After connecting the USB converter to the corresponding interface on the STM32 carrier board, ensure that the power supply is stable. Then, open the upper computer software and connect to the virtual COM port. If the virtual COM port is not detected, you may need to install the necessary drivers:  
[Virtual COM Port driver V1.5.0.rar](https://drive.google.com/file/d/1uuhiYtNGxeTXtBCTBPr5kz_kKH_pcbce/view?usp=drive_link)
Next, open the actuator interface and configure it as shown below. Select the corresponding motor type and the appropriate direction settings, then save the motor configuration: 

<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug5.png" height="500" />
</div>

Please note that the image folder in the upper computer software must be placed in the root directory of the D drive.  

[upper computer.rar](https://drive.google.com/file/d/1icTSwYw3gnz_ipY1XrbzaZGFPWtGljmV/view?usp=drive_link)

---

## Motion Control Program Download

After completing the Odroid RT system configuration, you need to download the control program to the robot controller:  
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug6.png" height="300" />
</div>
Create the Tinker and the corresponding subdirectories in the root directory of the Odroid system:  
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug7.png" height="200" />
</div>
Next, edit the auto-start script by running:

```bash
sudo nano /etc/rc.local
```

Add the following lines:

```bash
test -f /etc/ssh/ssh_host_dsa_key || dpkg-reconfigure openssh-server
sleep 10
sudo /home/odroid/Tinker/hardware_task_tinker &
sleep 3
sudo /home/odroid/Tinker/control_task_tinker &
sleep 3
sudo /home/odroid/Tinker/navigation_task_tinker &
```

Afterward, restart the controller. Once the system is up, use the `top` command to check if the auto-start process was successful:  
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug8.png" height="200" />
</div>
For configuration software, you can use:  

[putty.exe](https://drive.google.com/file/d/1WcXI9IVzbpopcH0JQHlvaY-ucwCFGIxr/view?usp=drive_link)
[WinSCP.exe](https://drive.google.com/file/d/1DlW7sgCHLVWpbjxLYgEGm6deTLkvyu92/view?usp=drive_link)

**V1:**  

[Tinker.rar](https://drive.google.com/file/d/1KfFQUZ8alXkkvc0c4pAmWQHyw0OcuPXl/view?usp=drive_link)

---

## Running RL Model

After completing the software setup, you need to follow the assembly guide to complete the installation of Tinker V1. Once the motors and controllers are confirmed to be working properly, use the control software to perform robot leg calibration and power-on. After verifying the system's functionality, you can proceed with RL model testing. 

For standard model testing, we recommend using a server to perform inference tests to ensure the real-time solution of the model. Control commands are transmitted to the robot's controller over a UDP network to drive the robot.  

<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/whiteboard_ug2.png" height="150" />
</div>

We recommend the following server configuration for sampling:  

| Component   | Description                |
|-------------|----------------------------|
| Server      | Configuration for sampling  |
| pt Model    | File generated during training, used for inference testing  |
| jit Model   | Optimized model for deployment |
| UDP Network | Used to transmit control commands to the robot |
| IP Address  | Configure the robot controller's IP for UDP communication  |

This table outlines the essential components and configuration required for running and testing the RL model on the Tinker V1 robot.

In the RL project we provide, `train` generates the corresponding `.pt` files in the log, which can be further converted into deployable models like `jit` through `simple_play`. The final inference result is transmitted via UDP using the scripts from `sim2sim_lcm` in the C++ version. The steps for exporting and running a model are as follows:

1. Set the path to the `.pt` model in `Simple_play` and run it:  
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug9.png" height="280" />
</div>
2. The `jit` model generated after training should have its path configured in the `sim2sim` software:  
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug10.png" height="250" />
</div>
At the same time, configure the robot controller's IP address:  
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug11.png" height="300" />
</div>
Inside the `build` folder, run `make` and execute `udp_publish_tinker`. If everything is working correctly, the system will show that the model has been successfully loaded and real-time action results will be printed: 
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug12.jpeg" height="500" />
</div>

---

## JetsonNano Configuration

To achieve fast RL control, we recommend using UDP for deployment testing after training to verify the basic functionality of the model. Once verified, you can proceed with converting and deploying the model at the edge. The commands will be sent directly to the robot via UDP. The system connection is shown below (currently, we are using a 4060 training GPU with a time per iteration of approximately 1.1s under 1024 environments. In the future, we will also release a dedicated RL suite to help configure the hardware, enabling training and deployment right out of the box).

To achieve edge-side deployment, we use JetsonNano instead of a server, running the previously migrated software:

<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/0/whiteboard_ug3.png" height="150" />
</div>

First, you need to complete the JetsonNano environment setup (you can also use our official image directly). This guide references [this post](https://blog.csdn.net/qq_41451125/article/details/116262611).

### Steps:

1. **Install Miniconda**:  
   Select the `Miniconda3 Linux-aarch64 64-bit` version for Linux. Create a virtual environment with Python 3.6. If you encounter a message that Python 3.6 cannot be found, modify the channel as follows:
   ```bash
   conda config --add channels conda-forge
   ```
   After creating the environment, modify the `pip` configuration:
   ```bash
   [global]
   timeout = 6000
   index-url = https://pypi.tuna.tsinghua.edu.cn/simple
   trusted-host = pypi.tuna.tsinghua.edu.cn
   ```

2. **Download the Jetson Nano Torch Version**:  
   Visit [PyTorch for Jetson](https://forums.developer.nvidia.com/t/pytorch-for-jetson/72048) (version 1.10 is recommended). In the newly created environment, install it via `pip`.

3. **Test PyTorch Installation**:  
   Enter Python and import `torch` to check for errors. If you encounter the error "Illegal instruction (core dumped)," add the following to the environment variables in `~/.bashrc`:
   ```bash
   export OPENBLAS_CORETYPE=ARMV8
   ```

4. **Install CMake** in the new environment:
   ```bash
   conda install -c anaconda cmake
   ```

5. **Install the LCM Package** from the `tinymal` source files:  
   Delete the contents of the `build` folder inside the LCM folder, then enter the `build` directory in the terminal and run the following three commands:
   ```bash
   cmake ..
   make
   sudo make install
   ```

6. **Modify the `CMakeLists.txt` File**:  
   Update the paths for CUDA and Torch libraries, and add the `cuBLAS` library path.  
   <div align="center">
    <img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug13.png" height="500" />
   </div>

7. **Compile the Contents** of the `sim2sim_lcm` folder:  
   Before compiling, modify the model path in the file to point to `model_jitt.pt` and run:
   ```bash
   ./udp_publisher
   ```

8. **Set Up SSH and VNC for Remote Connection**:  
   Refer to [this post](https://blog.csdn.net/yangyu0515/article/details/133922022#:~:text=%E7%82%B9%E5%87%BBadd%EF%BC%8C%E5%9C%A8%E6%96%B0,add%E7%A1%AE%E8%AE%A4%E6%B7%BB%E5%8A%A0%E3%80%82) for details.

Once installation is complete, copy the Jetson-specific `sim2sim` software to your local machine and compile it. Afterward, copy the model from the server to Jetson, modify the model path and master controller IP as done on the server, and run the test.

[sim2sim_lcm.rar](https://drive.google.com/file/d/1YC_1fXLcj6rgHkGUtPaOiV9k3QHX9NVM/view?usp=drive_link)

---

## Gait Testing

After completing all functional tests on the robot, you can start testing the gait. First, select an IP name in the image file's TXT document on the upper computer, modify the address to the controller's IP, and choose its name when connecting with the upper computer:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug14.png" height="200" />
</div>
Before opening the upper computer, insert a USB controller, connect to Wi-Fi, and select the corresponding IP:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug15.png" height="200" />
</div>
If the angle display on the upper computer shows `333`, the controller is running:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug16.png" height="500" />
</div>
Reset the STM32 controller board by pressing the reset button, then check that joint angles and posture data on the upper computer are normal:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/Instruction/ug17.png" height="500" />
</div>

### Steps:

1. **Powering On**:  
   Before powering on, make sure the robot’s joint calibration has been completed. Lift the robot with its legs in a vertical position, then press and hold the `X` button. The robot will retract its legs to a squat position. At this point, the robot should be able to stand using position loop control for angles.  
   If an anomaly occurs or the motor rotates incorrectly, press the `↓` button to cut the power.

2. **Starting the RL Program**:  
   Refer to the previous content to start the RL software and confirm the data is refreshing.

3. **Gait Activation**:  
   While in standing mode, press the `X` button again. The robot will use RL data to initiate gait control. The left joystick corresponds to XY speed commands, while the left and right triggers on the back of the controller correspond to heading commands. If the robot operates correctly, you can control its movement.

---
