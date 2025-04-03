# Tinker
## _Flexible, and Ready to Move: Your Cartoon-Style Bipedal Robot!_ 

Tinker is driven by reinforcement learning, where neural networks execute gaits, achieving stable walking and standing. During testing, software is required to train the neural network. 

## Acknowledgements
This project is based on the original code from [LocomotionWithNP3O](https://github.com/zeonsunlightyu/LocomotionWithNP3O). Special thanks to the contributors of the original repository for their work and contributions. 
Our code has been modified based on this. [Click here to download](https://drive.google.com/file/d/1LdauN7O6L77jsrmTSDgzHp0mcgKvIAJ_/view?usp=sharing).

**Performance on the real robot** please check out the link below:  
[Code Repository Update Series 1: Check it out! GitHub: LocomotionWithNP3O - Bilibili](https://b23.tv/haLM4jg)

## Coordinate System Definition
First, export the URDF and use RViz to review the coordinate system and angles, mainly to increase joint limits, angular velocities, and maximum torque. The URDF and XML files for Tinker are as follows:  
You can download the file from [thinker.zip](https://drive.google.com/file/d/1ZrNIlMniP54uTsEq2xIo4VjpPapP6Isk/view?usp=drive_link).

To view the URDF in RViz, use the following command:
```bash
roslaunch urdf_tutorial display.launch model:=/home/pi/Downloads/LocomotionWithNP3O-master/resources//tinker/urdf/tinker_urdf.urdf
```
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/development/1.PNG" height="300" />
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/development/2.PNG" height="300" />
</div>

## Environment Setup
Follow the commands below to set up the environment, and refer to online tutorials to install IsaacGym in the virtual environment:
```bash
conda create -n Tinker python=3.8.10
conda activate Tinker
pip install torchvision -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install torch -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install pyquaternion -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install pyyaml -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install rospkg -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install pexpect -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install mujoco==2.3.7 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install mujoco-py -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install mujoco-python-viewer -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install dm_control==1.0.14 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install opencv-python -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install matplotlib -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install einops -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install tqdm -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install packaging -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install h5py -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install ipython -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install getkey -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install wandb -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install chardet -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install numpy==1.23.2 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install h5py_cache -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install opencv-python -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install tensorboard -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install lcm -i https://pypi.tuna.tsinghua.edu.cn/simple
```

Download IsaacGym from the official website:
```bash
cd isaccgym/python && pip install -e .
```

Activate the virtual environment:
```bash
conda activate Tinker
```

Add shortcuts to `.bashrc` for refreshing environment variables:
```bash
alias sd="source devel/setup.bash"
alias ss="source ~/.bashrc"
alias a1="conda activate Tinker"
```

## Software Usage

### Train the Model:
After setting up the environment and activating the virtual space, run the script for training:
```bash
python train.py
```
The trained model will be updated here:  
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/development/3.png" height="300" />
</div>

To test the model, first modify the model file used in `simple_play.py`:
```python
model_dict = torch.load(os.path.join(ROOT_DIR, '/home/pi/Downloads/back_good/LocomotionWithNP3O-masteroldx/logs/rough_go2_constraint/Oct09_10-35-52_test_barlowtwins/model_3000.pt'))
```
Then run the script:
```bash
python simple_play.py
```

### Sim2Sim Testing
After training with Isaac, the model must be transferred. Sim2Sim involves building a framework on the controller side to run the neural network and feed the necessary feedback data. Using the Human-Gym as a reference, Mujoco simulator enables Sim2Sim transfer. For real-world transfer, additional software in C++ may be required. Typical transfer frameworks can be:
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/development/4.png" height="300" />
</div>

- **a. Using Mujoco Python/C++ simulation**: Embedding the network I/O in the Mujoco interface, preferred for semi-physical transfer.
- **b. Using Mujoco C++ simulation with LCM/ROS**: Running the Mujoco simulation asynchronously, interacting with C++ and Pytorch via LCM, suited for real-world transfer.

Before transfer, ensure the `default_dof_pos` matches the Isaac simulation:
```python
default_dof_pos = [0.0,-0.0,0.56,-1.12,0.57,0.0,0.0,0.56,-1.12,0.57]
```
Match the model path:
```bash
parser.add_argument('--load_model', type=str, default='/home/pi/Downloads/LocomotionWithNP3O-masteroldx/modelt.pt')
```
Update KP and KD to match training:
```python
class robot_config:
    kp_all = 9.0
    kd_all = 0.6
    kps = np.array([kp_all]*10, dtype=np.double)
    kds = np.array([kd_all]*10, dtype=np.double)
    tau_limit = 12. * np.ones(10, dtype=np.double)
```
Then run the transfer script:
```bash
python sim2sim_tinker.py
```

### Prototype Inference Test
For prototype testing, connect the robot to the training server via Ethernet, or deploy the model on Jetson Nano for edge deployment.
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/development/5.png" height="150" />
</div>
First, compile the `sim2sim_lcm` build folder, ensuring that **libtorch** and **cuDNN** are installed. Then, modify the `udp_publisher_tinker.cpp` to set the robot's IP address:
```cpp
string UDP_IP="192.168.1.242";
int SERV_PORT= 10000;
```
Modify the model path:
```cpp
model_path = "/home/pi/Downloads/back_good/LocomotionWithNP3O-master/model_jitt.pt";
load_policy();
```
Run the publisher:
```bash
./udp_publisher_tinker
```

### Robot Operation
After completing Model Training, robot installation and assembly, and migrating software package compilation, you can start testing the gait. First, select an IP name in the image file txt document of the host computer and modify the address to the master IP. Then, select the corresponding name from the drop-down connection menu of the host computer.
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/development/6.png" height="150" />
</div>
Before opening the host computer, insert the USB handle, connect to WIFI, and select the corresponding IP.
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/development/7.png" height="150" />
</div>
If the angle displayed by the host computer is 333, the controller software has already run.
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/development/8.png" height="300" />
</div>
If you press the reset button on the main control STM32 carrier board to reset, the above joint angle and posture of the upper computer will have normal data.
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/development/9.png" height="300" />
</div>
Power on:
Before powering on, it is necessary to ensure that the robot joints have been calibrated according to the assembly instructions. Lift the robot with both legs in a vertical position, long press the X button, and the robot will retract its legs to a squatting angle. At this time, the robot should be able to be placed normally on the ground to achieve locked standing.
If there is an abnormality and the motor rotates, press the button ↓ to turn off the power
Start RL program:
Start the migration software on the server or JetsonNano side, and confirm that the data is refreshed
Press X again in standing mode, and the robot will use RL data for gait driving. At this time, the left joystick corresponds to the XY speed command, the left and right triggers at the back of the handle correspond to the heading command, and the handle and joystick correspond to the robot's head posture. Press B to re-enter the locked state to achieve standing, and the power-off protection is under the button

# V1.1 Version Update Notes

## Updates
- Added gait movement and standing functions.
- Enabled quick configuration through a unified `global_config.py` file.


---


# 4. Software Usage

## 4.1 V1.1 Version Configuration

Modify the `global_config.py` file to quickly configure the training object and model files:

```python
import os
ROOT_DIR = os.path.dirname(__file__)
ENVS_DIR = os.path.join(ROOT_DIR, 'Env')

# Select robot: Taitan / Tinker / Tinymal
ROBOT_SEL = 'Tinker'

# Select gait: Trot / Stand
GAIT_SEL = 'Trot'

# Model file path
PLAY_DIR = 'XXX.pt'  

# Sim2Sim commands
SPD_X = 0.3
SPD_Y = 0.0
SPD_YAW = 0

# Training parameters
MAX_ITER = 30000
SAVE_DIV = 5000
```


## 4.2 Common Script Files

| File Name           | Function                                  |
|---------------------|-------------------------------------------|
| `train.py`          | Train the model                           |
| `play.py`           | Test the model and export `.pt` file      |
| `sim2sim_tinker.py` | Mujoco simulation testing                 |
| `pt2tvm.py`         | Convert model format to TVM for robots    |
| `exp_draw.py`       | Plot reward curves and tuning parameters  |

<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/development/2025040401.png" height="300" />
</div>

## 4.3 Deployment Instructions

After completing the robot training and model export:

1. Convert the model to TVM format (`policy_arm64_cpu.so`)
2. Use WinSCP or other tools to upload it to the Model directory in the robot's control files
3. Ensure the file name matches the exported model

## 4.4 Development Process

<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/development/whiteboard_exported_image.png" height="100" />
</div>

## 4.5 Tinker Robot Model Folder Structure

The following directories contain different gait models:

| Directory | Function                  |
|-----------|---------------------------|
| `Trot`    | Gait movement TVM model   |
| `Stand`   | Standing TVM model        |
| `Dance`   | Dance TVM model           |
```

