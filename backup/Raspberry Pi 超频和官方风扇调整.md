##  处理器超频
1. 超频 Raspberry Pi 5
```bash
sudo nano /boot/firmware/config.txt
``` 
```
[all]
over_voltage=8
arm_freq=3000
gpu_freq=1000
```
🔹 over_voltage=8 → 提高 CPU 电压，避免超频崩溃
🔹 arm_freq=3000 → 超频到 3.0GHz（可以调低，比如 2800）
🔹 gpu_freq=1000 → 提高 GPU 频率，提升图形性能

如果你使用主动散热（风扇），可以尝试更高的 arm_freq，但 3.0GHz 已经是比较极限的值。

### 2.启用电源管理（可选）
在 config.txt 里 添加或修改：
`force_turbo=1`
🔹 force_turbo=1 → 强制锁定最高频率，可能会影响保修，但能保证超频效果。

如果不确定，建议先不加 force_turbo，先看看超频稳定性。

### 3. 应用更改并重启
```bash
sudo reboot
``` 
### 4. 检查超频是否生效
重启后，运行以下命令检查 CPU 频率：
```bash
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq
```
### 5. 监测温度
超频后温度可能会上升，运行：
```bash
vcgencmd measure_temp
```

## 风扇控制
### 1. 确保风扇连接到正确的 GPIO
在 RPi 5 上：

5V 风扇 → 连接 5V（PIN 4 或 2） 和 GND（PIN 6 或 9） → 无法调速，只能一直运行
PWM 风扇 → 连接 GPIO 18（PIN 12） 作为 控制信号
GND → 连接 PIN 6 或 9
🔹 如果风扇只有 2 根线（红黑） → 无法调速，只能开/关。
🔹 如果风扇有 3 根线（红、黑、黄） → 可以控制转速（PWM 控制）。

### 2. 直接手动控制风扇（不调速）
如果风扇接到了 5V PIN（2 或 4），它会一直转动，你可以用 raspi-gpio 控制 开关：
```bash
echo "18" > /sys/class/gpio/export
echo "out" > /sys/class/gpio/gpio18/direction
echo "1" > /sys/class/gpio/gpio18/value  # 开启风扇
echo "0" > /sys/class/gpio/gpio18/value  # 关闭风扇
```
但这样不能调节转速，只能开/关。

### 3. 使用 Raspberry Pi 官方 PWM 控制
#### 启用 PWM 软风扇控制
修改 config.txt：
```bash
sudo nano /boot/firmware/config.txt
```
添加以下内容, 然后重启：
```ini
dtoverlay=pwm-fan
```
重启后，运行：
```bash
cat /sys/class/thermal/cooling_device0/cur_state
```
### 4. 自定义风扇温度控制
修改 /boot/firmware/config.txt, 然后重启：
```ini
dtoverlay=pwm-fan,temps=60000,65000,70000,75000
```
这些值的意思：
- 60000（60°C）→ 最低风扇速度
- 65000（65°C）→ 中等速度
- 70000（70°C）→ 高速
- 75000（75°C）→ 最大转速