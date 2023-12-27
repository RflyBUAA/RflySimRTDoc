# 配置WIFI模块

这套系统需要使用**串口转WIFI模块**发送模型的位置姿态等用于显示的数据。用户可以使用任何串口转WIFI模块，只需要按照串口正确连接即可。
要求为：串口转WIFI模块配置为波特率921600，并以UDP透传模式向局域网中用户指定主机IP和端口20010发送数据。

这里以正点原子的[ATK-ESP8266](https://detail.tmall.com/item.htm?spm=a230r.1.14.18.69a09754bcIZd5&id=609757779633&ns=1&abbucket=8&skuId=4447338308660)为例说明配置方法。其他模块配置要求类似，但是用到的指令可能有所区别。
配置前需要自行准备USB转串口模块，以便与串口转WIFI模块连接配置其参数。

NOTE: 必须使用串口助手来完成设置

初次使用请按照[1 初次使用](../user_manual/configWIFImodules.md#1)和[2 设置网络](../user_manual/configWIFImodules.md#2) 的指引完成操作。后续更换网络连接则只需要按照[2 设置网络](../user_manual/configWIFImodules.md#2)中的步骤操作即可。

## 1 初次使用
目的：需要设置无线模块连接到局域网路由器中（COM-SAT模式）采用UDP模式。这部分操作仅仅面向新购买的串口转WIFI模块。

方法：PC通过USB转串口与WIFI模块连接，通过串口AT指令配置。

NOTE: WIFI模块模块出厂默认波特率115200

1.设置WIFI模式为SAT，也就是作为网卡连接局域网
```
AT+CWMODE=1
```

2.重启模块，使前面的设置生效
```
AT+RST
```

3.指定WIFI名称和密码，将`<wifi-name>`替换为局域网网络名称，将`<password>`替换为局域网密码
```
AT+CWJAP="<wifi-name>","<password>"
```

4.启用单连接模式
```
AT+CIPMUX=0
```

5.指定模块要转发的目标机地址和目标端口号。将`192.168.XXX.XXX`改为目标主机的IP地址，不建议设置为`255.255.255.255`。
```
AT+CIPSTART="UDP","192.168.XXX.XXX",14550
```

## 2 设置网络

如果在使用中更换了局域网络，那么需要重新设置WIFI模块的网络连接。
RflySim3D从端口20010读取飞行器的位置姿态数据。

<!-- TIP: QGC地面站的端口号是14550 -->

!!! TIP
	- QGC地面站的端口号是14550
	- RflySim3D的端口号是**20010**
	- 串口转WIFI模块串口端最终应配置为**921600**波特率

1.退出透传模式（不包括换行符，否则无效）
```
+++
```

2.查看当前连接状态

```
AT+CIPSTATUS
```

<!-- ![image.png](https://cdn.nlark.com/yuque/0/2020/png/1166025/1603357693609-64b1ba55-ad10-44d0-be4e-4cc18b0ce256.png#averageHue=%230d490d&height=66&id=KS4JA&originHeight=78&originWidth=391&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7433&status=done&style=none&title=&width=333) -->

3.获取模块 IP 地址
```
AT+CIFSR
```

<!-- ![image.png](https://cdn.nlark.com/yuque/0/2020/png/1166025/1603357074005-f527bd1d-80c8-4aa8-b2d5-4fd8572fae8f.png#averageHue=%230e4a0e&height=66&id=w2dJj&originHeight=74&originWidth=371&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7563&status=done&style=none&title=&width=333) -->

4.指定（修改）WIFI名称和密码
```
AT+CWJAP="<wifi-name>","<password>"
```

5.指定上电透传模式参数。
```
AT+SAVETRANSLINK=<mode>,<remote IP>,<remote port>,<type>,<TCP keep alive>,<UDP local port>
```

|参数				|说明						|
|---|---|
|<mode\>			|是否上电开启透传，0或者1	|
|<remote IP\>		|远端IP	"192.168.XXX.XXX"	|
|<remote port\>		|远端端口号					|
|<type\>			|"TCP"或者"UDP"				|
|<TCP keep alive\>	|默认关闭，可省略			|
|<UDP local port\>	|UDP模式的本地端口号		|

例如：
```
AT+SAVETRANSLINK=1,"192.168.XXX.XXX",20010,"UDP",20011
```

6.修改串口比特率
```
AT+UART=921600,8,1,0,0
```

<!-- ![image.png](https://cdn.nlark.com/yuque/0/2020/png/1166025/1603357052829-c00b0375-f6bc-44e8-ba03-71b9f71b58d6.png#averageHue=%23074507&height=45&id=oevYq&originHeight=50&originWidth=366&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3230&status=done&style=none&title=&width=329) -->

7.退出开机透传模式
```
AT+SAVETRANSLINK=0
```


## 3 更多设置请参考
[ATK-ESP8266 WIFI用户手册_V1.3.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/1166025/1663297701072-8afc670e-7056-4274-bc65-264ab8bc136a.pdf)
