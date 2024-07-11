# Fairino 机械臂手柄遥控项目
这是简介

## 已知问题或修改计划
- [x] 三个摇杆不能同时移动，否则机器人会卡住
- [ ] 配置硬编码在代码中，不能修改
- [ ] 速度不可调
- [ ] 夹爪需手动初始化
- [ ] 夹爪运动时无法移动（似乎是 API 的问题）

## 键位
| 按键   | 功能 |
| :---: | --- |
| START/X | 使能机器人，清除错误 |
| MENU | 终止程序 |
| SELECT | 清除可复位错误 |
| LT+RT | API 急停，下使能 |
| 左摇杆 | 末端平面移动 |
| 右摇杆 | 末端法向量移动 |
| 十字轮盘 | 基坐标系水平面移动 |
| A/B | 基坐标系上下移动 |
| Y | 控制台输出末端位姿 |
| LB/RB | 夹爪开合 |


## 安装步骤
### 环境配置
- ROS-neotic
- Python 3.10.*
- Git

**ROS(noetic) 安装**  
推荐使用 [micromamba](https://mamba.readthedocs.io/en/latest/installation/mamba-installation.html) / [conda](https://www.anaconda.com/download/) 环境  
下文中 `micromamba` 与 `conda` 命令可等效替换

    micromamba env create -n ros-noetic-py10 -c ros-noetic-py10 -c conda-forge python=3.10 ros-noetic-desktop ros-noetic-joy ros-noetic-joystick-drivers
    micromamba activate ros-noetic-py10

如果已有 ROS 环境，只需安装 `ros-noetic-joy` `ros-noetic-joystick-drivers` 即可


**项目配置**  
```bash
git clone https://github.com/dian-hn1/fr5-ctrl
cd fr5-ctrl
git submodule update --init --recursive  # sdk 以子模块的形式嵌入项目

catkin_make  # 生成环境，因为是 python 包，不需要编译
```

## 运行  

    source devel/setup.bash
    roslaunch fr5_gamepad fr5.launch

### 调试运行  
如果要在 IDE 中调试代码，可以手动调起 ROS 服务器。  
需要两个终端，推荐使用 tmux

    micromamba activate ros-noetic-py10
    cd fr5-ctrl
    
    # tmux
    roscore
    rosrun joy joy_node _autorepeat_rate:=125  # 设置采样频率为 125 Hz
    python src/fr5_gamepad/src/main.py
