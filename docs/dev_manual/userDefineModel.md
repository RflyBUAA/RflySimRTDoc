# 生成仿真模型

用MATLAB 2021a打开工程文件，该文件位于[PL文件夹中](../dev_manual/envConfig.md#3)，名为`PL.prj`。

打开工程中的文件`.\Tools\CopyModelCode2VitisPrj.m`，该文件用于自动将生成的模型代码拷贝到vitis工程路径中，免去手动繁琐的操作。文件中
```
vitisPrjPath = 'D:\myWorkSpace\RflySimCourse\socfpga-hil-vitis\';
unzip('code\Model.zip','Tools\Model')
delete .\Tools\Model\code\Model_ert_rtw\ert_main.c  .\Tools\Model\code\Model_ert_rtw\buildInfo.mat  .\Tools\Model\code\Model_ert_rtw\defines.txt
copyfile('.\Tools\Model',[vitisPrjPath,'HIL_APP\src\TaskINT\Model'])
rmdir Tools\Model s
```
修改`vitisPrjPath`的值为用户在[导入Vitis工程源码](../dev_manual/envConfig.md#2-vitis)中设置的路径。

设置安装路径（修改下面命令的路径为Xilinx软件的安装路径）
```
hdlsetuptoolpath('ToolName','Xilinx Vivado','ToolPath','D:\Xilinx\Vivado\2020.1\bin\vivado.bat');  
```

依次运行脚本

- PL\Model\H250DegradedParamInit4S.m
- PL\HIL_System\SensorParamInit.m

打开模型文件

- PL\HIL_System\HIL_System.slx

在模型最顶层找到model子系统，在子系统上右键，编译子系统，如下图所示

编译模型
![](../img-large/buildmodel.png)

设置需要可调的参数。注意不要将模型采样时间设置为可调（保持为Inlined），这样会导致错误。
![](../img-large/buildmodel2.png)

编译后会显示生成的代码，可以在右侧查看到。
![](../img-large/buildmodel3.png)

最后运行脚本

- PL\Tools\CopyModelCode2VitisPrj.m

此时，生成的模型文件已经更新到了Vitis工程中。请用户在HIL_System.slx框架内自定义自己的模型，但不要对模型的输入输出接口做任何更改。

后面则是打开Vitis工程并编译，从而生成BOOT.bin文件。将该文件复制到仿真器的SD卡中，不要修改文件名称。