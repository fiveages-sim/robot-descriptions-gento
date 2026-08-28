# Gento

Gento 轮式人形：两套整机共用 Linkhou S2 v2 底盘，头部、躯干与手臂各自独立。

| 整机 | 包 | 头 | 躯干 | 手臂 |
|------|-----|------|------|------|
| Skye | `gento_skye_description` | 2-DOF | 3-DOF 腰（升降 + 俯仰 + 偏航） | Tianji M6-CCS |
| Luna | `gento_luna_description` | 2-DOF | 6-DOF 躯干 | Tianji M6S Lite CCS |

底盘复用 `fiveages_w2_common_description` 的 `linkhou_s2_v2`。

```bash
ros2 launch robot_common_launch humanoid.launch.py robot:=gento_skye collider:=simple
ros2 launch robot_common_launch humanoid.launch.py robot:=gento_luna collider:=simple
ros2 launch robot_common_launch component.launch.py robot:=gento_skye type:=head
ros2 launch robot_common_launch component.launch.py robot:=gento_luna type:=head
```
