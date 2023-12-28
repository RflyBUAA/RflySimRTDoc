# 欢迎使用RflySim-RT

RflySim-RT是可靠飞行控制研究组开发的一套硬件在环实时仿真平台，即RflySim的实时仿真版本。
与RflySim的核心区别在于，RT版本专注于实时快速仿真，希望能够提供更加真实的仿真效果，更好地服务底层控制。

RflySim-RT基于SocFPGA打造，仿真对象的模型以中断的方式运行在通用计算核心（ARM A53核心）上，同时通过FPGA实现仿真模型与自动驾驶仪的数据交换，完成硬件在环仿真。

## 1.1 现有特性

- [x] ARM A53单核裸机, 采用简单的时间片轮询. 
- [x] [Letter Shell](https://github.com/NevermindZZT/letter-shell)终端支持, 方便用户交互. 网上还有一个叫xc_shell.
- [x]  [FATFS](http://elm-chan.org/fsw/ff/00index_e.html)文件系统实现对SD卡的基本操作 网上还有一个叫littlefs
- [x] 串口wifi模块无线传输显示数据到RflySim3D显示软件, 
- [x] 串口wifi模块参数可以通过串口Shell修改
- [x] 默认2000Hz中断实时运行多旋翼模型
- [x] 模型参数([cJSON](https://github.com/DaveGamble/cJSON))可修改. 模型参数文件预先存放到SD卡, 或者PC端远程修改模型参数, 参数可以远程保存, 多参数文件支持,便于快速切换模型

## 1.2 规划特性 

- [ ] 采用PX4 ulog日志格式, 与飞控的ulog文件采用相同的API处理.
- [ ] 对MAVLINK的支持, QGC地面站修改模型参数, 甚至接入控制台
- [ ] PC端故障注入
- [ ] 更好的交互体验, PC端实现对仿真模型运行的控制(shell和PC上位机), 开发版上电后需要手动选择模型, 手动选择开始仿真, 并且手动停止模型, 软件重置模型.
- [ ] ls cd rm cat等文件操作函数的实现


<!-- ![type:video](https://www.youtube.com/embed/LXb3EKWsInQ) -->

<!-- 在bilibili视频页面选择分享后，从弹出的选项中选择 嵌入代码，可以得到这种嵌入网页的视频链接 -->
<!-- ![type:video](https://player.bilibili.com/player.html?aid=562083014&bvid=BV1Pv4y1D7ge&cid=874731745&p=1) -->

下面视频展示了基于该平台实现的四旋翼飞行器的硬件在环仿真
![type:video](./videos/simplatform.mp4)

---
文档最新提交的变化

<!-- {{ git_latest_release }} -->

{{ latest_changes }}