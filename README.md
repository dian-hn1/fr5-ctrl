# Fairino 机械臂手柄遥控项目
通过手柄，控制机械臂的运动与夹爪的张合。

## 安装步骤
```bash
git clone https://github.com/dian-hn1/fr5-ctrl
cd fr5-ctrl
git submodule update --init --recursive

# 运行
catkin_make
source devel/setup.bash
roslaunch fr5_gamepad fr5.launch
```
