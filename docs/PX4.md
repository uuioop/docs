PX4 是一个开源的、高性能的飞控固件。[PX4官网](https://docs.px4.io/main/zh/)

- **在本项目的角色**:
    
    - `PX4` 是飞行的执行者。它接收来自`MAVSDK` 的高层指令，并负责将其解算为毫秒级的电机控制信号。
        
- **关键模式：Offboard Mode**
    
    - `Offboard` (外部控制) 模式是实现机载计算机控制的关键。
        
    - 在此模式下，`PX4` 期望外部源（即我们的 [[MAVSDK]]或[[MAVROS]]桥接模块`）以高频率（例如 >2Hz）持续发送控制设定点（Setpoint）。
        
    - 如果指令流中断，`PX4` 将触发安全机制（如悬停或返航）。
        
- **仿真**:
    
    - `PX4` 提供了强大的 [[SITL (Software-In-The-Loop)]] 模式，使其能与 [[Gazebo 仿真]] 完美配合。
        

**关联: [[2. 核心技术栈]], [[MAVSDK]], [[SITL (Software-In-The-Loop)]]**