# 设置可调参数

在更新模型的环节中，我们设置了哪些参数作为全局变量的形式出现，只有以全局变量的形式出现才能够在vitis工程中将其暴露为可修改的参数。

声明这些可调参数的文件位于路径`rfly-sim-rt-vitis\HIL_APP\src\Config\config.c`中。下面给出了一段示例代码。在代码中通过ADD_PARAM()来声明这些可调参数，如果需要自行添加新的参数那么需要在此增加新的声明。这些被声明的参数是在其他c文件中声明过的全局变量。
```C
const ModelParam modelParamList[] =
{
// 四旋翼
		ADD_PARAM(Mass,&ModelParam_Airframe_m,1),
		ADD_PARAM(C_md,ModelParam_envC_md,3),
		ADD_PARAM(J,ModelParam_Airframe_J,9),
		ADD_PARAM(motorCr,&ModelParam_motorCr,1),
		ADD_PARAM(motorFitType,&ModelParam_motorFitType,1),
		ADD_PARAM(motorJm,&ModelParam_motorJm,1),
		ADD_PARAM(motorMinThr,&ModelParam_motorMinThr,1),
		ADD_PARAM(motorRateCurveCoeffi,ModelParam_motorRateCurveCoeffi,3),
		ADD_PARAM(motorTc,&ModelParam_motorTc,1),
		ADD_PARAM(motorWb,&ModelParam_motorWb,1),
		ADD_PARAM(rotorCt,&ModelParam_rotorCt,1),
		ADD_PARAM(NoiseVarAcc0, ModelParam_NoiseVarAcc0,3),
		ADD_PARAM(NoiseVarGyro0, ModelParam_NoiseVarGyro0,3),
		ADD_PARAM(NoiseVarMag0, ModelParam_NoiseVarMag0,3),
		ADD_PARAM(PositionAcc0, ModelParam_PositionAcc0,3),
		ADD_PARAM(DisplayUAVType,&RflySimDisplayUAVType,1),
		ADD_PARAM(CopterID,&RflySimCopterID,1),
		ADD_PARAM(RotorDirection, RotorDirectionVector, 8),
		ADD_PARAM(EfficiencyMatrix, EfficiencyMatrix, 48),
//公共部分
		ADD_PARAM(BoardRotation, BoardRotation,3),
		ADD_PARAM(IST8310_ConvertRatio, &IST8310_ConvertRatio,1),
		ADD_PARAM(Using_OneShot, &Using_OneShot,1)
};
```
ADD_PARAM()的声明如下
```c
#define ADD_PARAM(_name, _addr, _len)\
		{\
				.name = #_name,\
				.addr = (double *)_addr, \
				.len = _len \
		}
```
即ADD_PARAM()内部的三个参数分别是：**参数的名称**、**参数的指针**、**参数的长度**。如果是标量参数那么其具体表示形举例为
```c
ADD_PARAM(Using_OneShot, &Using_OneShot,1)
```
如果是数组（数组c\c++中指针，即名称本省就是指针，不需要添加专门的取址符号），那么具体表示形式举例为
```C
ADD_PARAM(BoardRotation, BoardRotation,3)
```
**参数名称**与[用户手册](../user_manual/modifyModelParam.md)中介绍的json文件中的参数名称对应。在json参数文件不存在或者存在但与这里声明的参数存在不一致的情况下，参数文件会由仿真系统重新创建，在创建过程中就根据**参数名称**生成相应的json参数文件。