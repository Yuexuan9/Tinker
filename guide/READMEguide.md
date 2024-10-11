# Tinker: An Open-Source Bipedal Robot

## Recommended Setup and Debugging Steps for Tinker:
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

## Odroid Controller System Configuration

  This guide provides the steps to install the 5.10 RT kernel on the Odroid C4 for real-time communication with the STM32 control board. The steps involve downloading the required image, burning it to an SD card, updating the system, and installing the necessary development tools.

  To set up the system, use the provided instructions to install the RT real-time patch for the 5.10 kernel version. Reference [this forum post](https://forum.odroid.com/viewtopic.php?f=55&t=41129) for more details.
  Since the RT patch is only compatible with the 5.10 kernel version, you will need to download the 1218 version of the image (as the original post linked the 5.11 version, which is not supported). 
  
  Download the image from the following URL:
  [http://ppa.linuxfactory.or.kr/images/raw/arm64/focal/](http://ppa.linuxfactory.or.kr/images/raw/arm64/focal/)
  
  Once downloaded, burn the image to your SD card and insert it into the Odroid system.
  
> Username: `odroid` Password: `odroid`
  
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

It is recommended to update the corresponding 8006 motors to the latest version of the same firmware:


---
