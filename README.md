MaixPy Documentation 
====== 

|[Read me online (EN)](https://sipeed.github.io/MaixPy_DOC)  | [在线阅读](https://sipeed.github.io/MaixPy_DOC/#/zh/) | 
|------------------------ | -----------| 

## What is MaixPy 
MaixPy is a [Micropython](http://micropython.org/) port for the 64Bit Dual-Core RISC-V [K210](https://kendryte.com/) CPU. 

> MicroPython is a lean and efficient implementation of the Python 3 programming language that includes a small subset of the Python standard library and is optimized to run on microcontrollers and in constrained environments. 

> K210 created for AIOT(AI+IOT) use, it's powerful performance and low cost are very competitive. 

Micropython make programming on the K210 easier, so we built this and open sourced it on [github]((https://github.com/sipeed/MaixPy)) 

For example, if we want to find I2C device, we just need code: 

```python 
from machine import I2C

i2c = I2C(I2C.I2C0, freq=100000, scl=28, sda=29)
devices = i2c.scan()
print(devices)
``` 

If we want to make a `breathing light` via PWM, we just need code: 

```python 
from machine import Timer,PWM
import time


tim = Timer(Timer.TIMER0, Timer.CHANNEL0, mode=Timer.MODE_PWM)
ch = PWM(tim, freq=500000, duty=50, pin=board_info.LED_G)
duty=0
dir = True
while True:
    if dir:
        duty += 10
    else:
        duty -= 10
    if duty>100:
        duty = 100
        dir = False
    elif duty<0:
        duty = 0
        dir = True
    time.sleep(0.05)
    ch.duty(duty)
``` 

## About this documentation 

This documentation contains everything related to Maixpy, mainly about: 
* Where to get the hardware 
* How to get started with MaixPy even if you are not an expert in programming for the hardware. 
* Learn MicroPython basics 
* Libraries(API) reference 
  
## Let's get started 

To get started we need a dev board, the three boards are as follows: 
* Dan dock with Sipeed M1(Dan) module 
![Dan dock](assets/images/Dan_Dock.png) 
* Sipeed Maix BiT 
![BiT](assets/images/BiT.png) 
* Sipeed Go 
![Go](/assets/images/Go.jpg) 

To get these boards, please visit the [Sipeed official website](https://sipeed.com/). 

More hardware information is available [here](en/hardware/hardware.md) 

If you already have a board, head on over to the [getting started](en/get_started.md) page.

## Source code 
MaixPy source code [on github](https://github.com/sipeed/MaixPy) 
------------ 
------------ 
Maintained by ![Sipeed](assets/images/icon_sipeed.png ':size=60x60') Sipeed Co.,Ltd. 
