# 如何适配PX4 1.12版本固件

!!! TIP "1.12版本固件相较1.11版本固件有一些变化。以下内容读者了解即可。"
	1. IST8310驱动中增加了对传感器寄存器中数据就绪位和软复位的检查。在新版固件中我对此做了适配。
	2. IST8310驱动中磁场强度的分辨率不同。这点在FPGA端需要注意，模型中增加了对应的参数，且映射到了可调参数中。用户根据不同的固件版本，在参数文件中做调整即可。

以下内容需要用户手动操作，以适配1.12版本的固件。

1.12版本在传感器启动脚本上需要做的改动与1.11版本不同。1.12版本应该修改rc.board_sensors（这里只针对Pixhawk 4，其他硬件用户可据此模仿进行修改）为：
```
#!/bin/sh
#
# PX4 FMUv5 specific board sensors init
#------------------------------------------------------------------------------

board_adc start

if ! icm20689 -S start
then
# Internal SPI bus ICM-20602
icm20602 -s -R 2 -q start

# Internal SPI bus ICM-20689
icm20689 -s -R 2 start

# Internal SPI bus BMI055 accel/gyro
bmi055 -A -R 2 -s start
bmi055 -G -R 2 -s start
fi

if ! ms5611 -X start
then
# Baro on internal SPI
ms5611 -s start
fi

if ! ist8310 -X -R 10 start
then
# internal compass
ist8310 -I -R 10 start

# External compass on GPS1/I2C1 (the 3rd external bus): standard Holybro Pixhawk 4 or CUAV V5 GPS/compass puck (with lights, safety button, and buzzer)
ist8310 -X -b 1 -R 10 start
fi
```

修改后的脚本逻辑是：优先启动外置传感器，如果启动失败则会启动内置传感器。
编译出的固件既可以用于仿真也可以用于实飞，不需要分别编译两个不同的固件。