> [!WARNING] **强烈建议使用 Ubuntu 20.04 (Focal Fossa)** 本构建流程在 Ubuntu 20.04 上经过完整测试。使用其他版本（如 22.04）可能会因为 Gazebo 版本不兼容、依赖库缺失等问题导致构建失败。

这是从 [[PX4]] 源码在 Ubuntu (Linux) 上构建 [[SITL (Software-In-The-Loop)]] 仿真环境的详细步骤。

## 1. 下载 PX4 源码

确保已安装 `git`。然后克隆 `PX4-Autopilot` 仓库，注意需要 `--recursive` 参数来下载所有子模块。

```
git clone [https://github.com/PX4/PX4-Autopilot.git](https://github.com/PX4/PX4-Autopilot.git) --recursive
```

## 2. 运行 Ubuntu 安装脚本

PX4 源码中提供了一个方便的设置脚本，它会自动安装包括 [[Gazebo 仿真]] (Classic 11) 在内的大部分依赖。

```
bash ./PX4-Autopilot/Tools/setup/ubuntu.sh --no-nuttx
```

## 3. 重启计算机

安装完成后，需要重启以使所有更改生效。

```
sudo reboot
```

## 4. 更新子模块和依赖

重启后，进入源码目录，再次确保子模块已更新，并安装一些额外的编译依赖。

```
# 进入源码目录
cd PX4-Autopilot

# 更新子模块
git submodule update --init --recursive  

# 下载 protobuf, eigen, opencv 等依赖
sudo apt-get install protobuf-compiler libeigen3-dev libopencv-dev -y
```

## 5. 构建并运行仿真

最后，编译 `px4_sitl_default` 目标，并指定 `gazebo` 作为后端。

```
make px4_sitl_default gazebo
```

如果一切顺利，Gazebo 窗口将会启动，无人机模型会出现在仿真世界中。

## 6. 常见问题 (Troubleshooting)

在构建过程中，你可能会遇到一些环境导致的问题（这些问题需通过终端输出判断）：

1. **网络问题 (GitHub 访问)**
    
    - **现象**: `git clone` 或 `git submodule update` 速度极慢或失败。
        
    - **解决**: `git` 需要配置代理或修改DNS和host文件（前者成功率高）才能正常访问 GitHub。
        
2. **源问题 (apt / pip)**
    
    - **现象**: 执行 `ubuntu.sh` 脚本时，`apt-get install` 或 `pip install` 报错，提示无法下载某些包。
        
    - **解决**: `apt` 和 `pip` 可能需要更换为国内的镜像源（如清华源、阿里源）。
        
3. **构建卡住 (权限或依赖问题)**
    
    - **现象**: `make` 过程长时间卡住不动，或者报错退出。
        
    - **解决**:
        
        - **权限问题**: 可能是某些脚本没有执行权限。
            
        - **重新构建**: 有时构建过程会因意外中断而出错，可以尝试**删除 `build` 目录**或直接**再次运行 `make px4_sitl_default gazebo` 命令**。
            
        - **报错分析**: 仔细查看终端输出。例如，之前我们遇到过的类似下面的报错，就是由于 Python 脚本执行失败导致的：

**关联: [[4. 仿真与测试]], [[PX4]]** **返回: [[index]]**