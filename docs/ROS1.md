> [!NOTE] 这是本项目的主线技术方案。
> - 我们将使用Noetic，它适配 Ubuntu 20.04。

[ROS1中文视频教程，1-17讲](https://www.bilibili.com/video/BV1BP4y1o7pw/?spm_id_from=333.337.search-card.all.click&vd_source=e35fecf3ad19c6e478d062509b67923d)

## 安装 ROS 1 Noetic

```
# 添加 ROS 1 软件源
sudo sh -c 'echo "deb [http://packages.ros.org/ros/ubuntu](http://packages.ros.org/ros/ubuntu) $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

# 添加密钥
sudo apt install curl # if you haven't already installed curl
curl -s [https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc](https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc) | sudo apt-key add -

# 安装
sudo apt update
sudo apt install ros-noetic-desktop-full

# 设置环境变量
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc

# 安装依赖
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
sudo apt install python3-rosdep
```



**关联: [[2. 核心技术栈]]** **返回: [[index]]**