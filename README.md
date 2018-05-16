# SENZ011-Environment-Light-Sensor

###### Translation

> For `English`, please click [`here.`](https://github.com/njustcjj/SENZ011-Environment-Light-Sensor/blob/master/README.md)

> For `Chinese`, please click [`here.`](https://github.com/njustcjj/SENZ011-Environment-Light-Sensor/blob/master/README_CN.md)

![](https://github.com/njustcjj/SENZ011-Environment-Light-Sensor/blob/master/pic/SENZ011.jpg "SENZ011")


### Introduction

>  SENZ011 is a environment light intensity sensor breakout board which has a BH1750 chip. A 16 bit AD converter is built-in so that SENZ011 can directly output a digital result in lx(Lux) and doesn't need complicated calculations. This is a more accurate and easier. When objects which are lighted in homogeneous get the 1 luminous flux in one square meter, its illumination  intensity is 1lx. Sometimes to take good advantage of the illuminant, you can add a reflector to the illuminant. So that there will be more luminous flux in some directions and it can increase the ilumination of the target surface. 
>
> Usage : detect the illumination intensity and its variation.



### Specification

- Power supply: +3 ~ 5V
- Interface : I2C
- Measuring range: 1 - 65535 lx
- 2 types of I2C slave-address can be selected
- Small measurement variation (+/- 20%)
- Size: 33 x 15 mm

- Illumination intensity example:
	- Nignt : 0.001 - 0.02; 
	- moonlightnight : 0.02 - 0.3; 
	- cloudy indoor : 5 - 50;
	- cloudy outdoor : 50 - 500;
	- Sunny indoor : 100 - 1000;
	- under the sunlight in summer afternoon : 0.6e5 - 1e5; 
	- reading books:50 - 60;
	- home video : 1400

### Tutorial

#### Wire Definition

|Sensor pin|Ardunio Pin|Function Description|
|-|:-:|-|
|VCC|3.3V~5V|Power|
|GND|GND||
|SCL|Analog pin|I2C bus interface clock|
|SDA|Analog pin|I2C bus interface data|
|ADDR|||

![](https://github.com/njustcjj/SENZ011-Environment-Light-Sensor/blob/master/pic/SENZ011_pin.jpg "Pin Definition") 

#### Connecting Diagram

![](https://github.com/njustcjj/SENZ011-Environment-Light-Sensor/blob/master/pic/SENZ011_connect.png "Connecting Diagram") 

#### Sample Code


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



### Purchasing [*SENZ011 Environment Light Sensor*](https://www.ebay.com/).
