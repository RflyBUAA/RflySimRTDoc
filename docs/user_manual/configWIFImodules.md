# 配置WIFI模块

请自行准备USB转串口模块

## 初次使用
第一次使用设置：无线模块连接到局域网路由器中（COM-SAT模式）采用UDP模式。PC通过USB转串口与wifi模块连接，通过串口AT指令配置。模块出厂**默认波特率115200：**

1. **AT+CWMODE=1**  设置wifi模式为SAT，也就是作为网卡连接局域网
2. **AT+RST** 重启模块并生效
3. **AT+CWJAP="E603","buaae603"**  指定wifi名称和密码
4. **AT+CIPMUX=0**   开启单连接
5. **AT+CIPSTART="UDP","192.168.1.XXX",14550 **指定模块要转发的目标机地址和目标端口号

## 更换网络后：
具体端口号需要根据自己的需要设置，文档中的14550只是QGC用的端口号，Rflysim3D用的（可能）是20010。同样使用串口AT指令设置：

- **退出透传模式：**+++(不包括换行符，否则无效)
- **获得连接状态：AT+CIPSTATUS**

<!-- ![image.png](https://cdn.nlark.com/yuque/0/2020/png/1166025/1603357693609-64b1ba55-ad10-44d0-be4e-4cc18b0ce256.png#averageHue=%230d490d&height=66&id=KS4JA&originHeight=78&originWidth=391&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7433&status=done&style=none&title=&width=333) -->

- **获取模块 IP 地址：AT+CIFSR**  

<!-- ![image.png](https://cdn.nlark.com/yuque/0/2020/png/1166025/1603357074005-f527bd1d-80c8-4aa8-b2d5-4fd8572fae8f.png#averageHue=%230e4a0e&height=66&id=w2dJj&originHeight=74&originWidth=371&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7563&status=done&style=none&title=&width=333) -->

- **指定（修改）WIFI名称和密码：   AT+CWJAP="E603","buaae603"** 
- **指定上电透传模式参数：AT+SAVETRANSLINK=1,"192.168.199.246",14550,"UDP",14551 **指令参数依次表示：**是否自动进入透传模式（1或0）、目标IP、目标端口号、TCP或者UDP、TCP侦测（默认为关闭，可不写）、本地端口号**
- **修改串口比特率**：**AT+UART=921600,8,1,0,0**

<!-- ![image.png](https://cdn.nlark.com/yuque/0/2020/png/1166025/1603357052829-c00b0375-f6bc-44e8-ba03-71b9f71b58d6.png#averageHue=%23074507&height=45&id=oevYq&originHeight=50&originWidth=366&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3230&status=done&style=none&title=&width=329) -->

- **退出开机透传模式：AT+SAVETRANSLINK=0**



## 更多设置请参考：
[ATK-ESP8266 WIFI用户手册_V1.3.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/1166025/1663297701072-8afc670e-7056-4274-bc65-264ab8bc136a.pdf)



