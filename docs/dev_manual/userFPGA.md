# 生成FPGA平台文件

## 1. MATLAB更新FPGA代码

## 2. Vivado编译生成xsa文件
打开vivado打开FPGA工程
![](../img-large/vivado_build1.png)

找到工程启动文件
![](../img-large/vivado_build2.png)

如下图操作，可以看到FPGA即PL端的顶层逻辑
![](../img-large/vivado_build3.png)

综合
![](../img-large/vivado_build4.png)

综合完成后，可根据提示进入下一步。或者手动选择下一步。如图
![](../img-large/vivado_build5.png)

![](../img-large/vivado_build6.png)

完成后，取消
![](../img-large/vivado_build7.png)

生成bit流文件
![](../img-large/vivado_build8.png)

!!! NOTE "在执行步骤的等待过程中可以按照下图操作查看进度"
	![](../img-large/vivado_build9.png)

!!! TIP "生成导出.xsa文件"
	![](../img-large/vivado_build10.png)

	![](../img-large/vivado_build11.png)

	![](../img-large/vivado_build12.png)

	![](../img-large/vivado_build13.png)
