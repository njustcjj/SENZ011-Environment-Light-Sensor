# SENZ011 数字环境光传感器

###### 翻译

> `英文` 请参考 [`这里`](https://github.com/njustcjj/SENZ011-Environment-Light-Sensor/blob/master/README.md)

> `中文` 请参考 [`这里`](https://github.com/njustcjj/SENZ011-Environment-Light-Sensor/blob/master/README_CN.md)

![](https://github.com/njustcjj/SENZ011-Environment-Light-Sensor/blob/master/pic/SENZ010.jpg "SENZ010")
 

### 产品介绍

> SENZ011采用BH1750FVI芯片，内置16位的模数转换器，通过IIC接口能够直接输出一个数字信号，不需要再做复杂的计算。
> 这款环境光传感器能够直接通过光度计来测量。光照度的单位是勒克斯"lx"。当物体在均匀的光照下它能够在每平方米获得1lm的光通量，它的光照度是1lx。
> 有时为了充分利用光源，你可以增加一个光源的反射装置。那样在某些方向就能获得更多的光通量，以增加被照表面的亮度。

> 
> 用途：探测光照度及变化

### 产品参数

* 供电电压：+3-5V
- 接口：I2C
- 量程：1~65535 lx
- 可以选择两种类型的I2C从地址
- 微小的测量变化(+/-20%)
- 尺寸：33 x 15 mm
- 光亮度数据参考：
	- 晚上： 0.001 - 0.02；
	- 月夜： 0.02 - 0.3；
	- 多云室内： 5 - 50；
	- 多云室外： 50 - 500；
	- 晴天室内： 100 - 1000；
	- 夏天中午光照下： 0.6e5 - 1e5；
	- 阅读书籍时的照明度：50 - 60；
	- 家庭录像标准照明度：1400


### 使用教程

#### 引脚定义

|Sensor pin|Ardunio Pin|Function Description|
|-|:-:|-|
|VCC|3.3V~5V|Power|
|GND|GND||
|SCL|Analog pin|I2C bus interface clock|
|SDA|Analog pin|I2C bus interface data|
|ADDR|||


![](https://github.com/njustcjj/SENZ011-Environment-Light-Sensor/blob/master/pic/SENZ011_pin.jpg "引脚定义") 


#### 连线图

![](https://github.com/njustcjj/SENZ011-Environment-Light-Sensor/blob/master/pic/SENZ011_connect.png "连线图") 


### 示例代码

	/*
	 Sample code for the SENZ011 Light sensor
	 Version 0.1
 
	 Connection:
 
	 VCC-5v
	 GND-GND
	 SCL-SCL(analog pin 5)
	 SDA-SDA(analog pin 4)
		 ADD-NC
	 */


	#include <Wire.h> //BH1750 IIC Mode 
	#include <math.h> 
	int BH1750address = 0x23; //setting i2c address

	byte buff[2];
	void setup()
	{
	  Wire.begin();
	  Serial.begin(57600);//init Serail band rate
	}

	void loop()
	{
	  int i;
	  uint16_t val=0;
	  BH1750_Init(BH1750address);
	  delay(200);

	  if(2==BH1750_Read(BH1750address))
	  {
	    val=((buff[0]<<8)|buff[1])/1.2;
	    Serial.print(val,DEC);     
	    Serial.println("[lx]"); 
	  }
	  delay(150);
	}

	int BH1750_Read(int address) //
	{
	  int i=0;
	  Wire.beginTransmission(address);
	  Wire.requestFrom(address, 2);
	  while(Wire.available()) //
	  {
	    buff[i] = Wire.receive();  // receive one byte
	    i++;
	  }
	  Wire.endTransmission();  
	  return i;
	}

	void BH1750_Init(int address) 
	{
	  Wire.beginTransmission(address);
	  Wire.send(0x10);//1lx reolution 120ms
	  Wire.endTransmission();
	}


### 购买[*SENZ011 数字环境光传感器*](https://www.ebay.com/).