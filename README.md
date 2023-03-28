# CircuitPython
This repository will actually serve as a aid to help you get started with your own template.  You should copy the raw form of this readme into your own, and use this template to write your own.  If you want to draw inspiration from other classmates, feel free to check [this directory of all students!](https://github.com/chssigma/Class_Accounts).
## Table of Contents
* [Table of Contents](#TableOfContents)
* [Hello_CircuitPython](#Hello_CircuitPython)
* [CircuitPython_Servo](#CircuitPython_Servo)
* [CircuitPython_DistanceSensor](#CircuitPython_DistanceSensor)
* [CircuitPython_LCD](#CircuitPython_LCD)
* [MotorControl](#MotorControl)
* [TemperatureSensor](#TemperatureSensor)
---

## Hello_CircuitPython

### Description & Code
This assignment was our intro assignment to circuitpython. Our job was to get the neopixel to blink and change colors. 



```python
import board
import neopixel
import time 

dot = neopixel.NeoPixel(board.NEOPIXEL, 1)
dot.brightness = 0.5 
while True:
    dot.fill((0, 0, 255))
    time.sleep(0.5)
    dot.fill((255, 255, 255))
    time.sleep(0.5)
```


### Evidence


![Untitled_ Sep 27, 2022 3_18 PM (1)](https://user-images.githubusercontent.com/112961430/193047596-eea5442e-cbe6-4e91-b174-e436803c214c.gif)



Image credit goes to [Kaz S](https://github.com/kshinoz98/CircuitPython#Hello_CircuitPython)


### Wiring
There wasn't any wiring required in this assignment.

### Reflection
This assignment took longer than needed, because of the initial importing of functions into cirucuit python. I also had trouble using the serial monitor as well.




## CircuitPython_Servo

### Description & Code

```python
import time
import board
import pwmio
from adafruit_motor import servo


pwm = pwmio.PWMOut(board.D7, duty_cycle=2 ** 15, frequency=50)


my_servo = servo.Servo(pwm)

while True:
    for angle in range(0, 180, 5):  
        my_servo.angle = angle
        time.sleep(0.05)
    for angle in range(180, 0, -5):
        my_servo.angle = angle
        time.sleep(0.05)

```

### Evidence
![192808365-425dc20f-adb3-4a49-96a3-89f3e8195865](https://user-images.githubusercontent.com/112961430/193279528-e7ac47fa-6eab-4d70-bdb7-e64ca753205b.gif)

Image credit goes to [Elias G](https://github.com/egarcia28/CircuitPython#evidence)
### Wiring!
![193279935-20da45e1-807a-4585-bdf1-f059e2371185](https://user-images.githubusercontent.com/112961430/193280272-701fa51d-ea67-4ab9-994e-ea3d98bdfe4a.png)

Image credit goes to [Elias G](https://github.com/egarcia28/CircuitPython#wiring)
### Reflection
This assignment's wiring was pretty easy, because there was no extra wires needed. I got help with my code from [Grant G](https://github.com/ggastin30/CPython#description--code-1)


## CircuitPython_DistanceSensor 

### Description & Code

```python
import board
import adafruit_hcsr04
import neopixel
import time
import simpleio

sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D7, echo_pin=board.D6)
klee = neopixel.NeoPixel(board.NEOPIXEL, 1)
klee.brightness = .3  
red=0
blue=0
green=0
while True:
    try:
        cm = sonar.distance
        print((sonar.distance))
        time.sleep(0.01)
        if cm < 5:
            klee.fill((255, 0, 0))
        if cm > 5 and cm <20:
         red=simpleio.map_range(cm,5,20,255,0)
         green=0
         blue=simpleio.map_range(cm,5,20,0,255)
         klee.fill((red,green,blue))
      
       
        if cm > 20 and cm < 35:
         red=0
         green=simpleio.map_range(cm,5,20,0,255)
         blue=simpleio.map_range(cm,5,20,0,255)
         klee.fill((green,blue,red))
    except RuntimeError:
        print("Retrying!")
        pass

    time.sleep(0.1)

```

### Evidence
https://user-images.githubusercontent.com/112961430/197537552-06cd7599-9af8-4e84-b464-2d35bc7e5d57.mp4

### Wiring
![193045742-26a5ac02-6881-416c-9d54-af293deceae0](https://user-images.githubusercontent.com/112961430/197537630-7a8b370f-e29f-4c5f-ad99-c78c346eddf5.png)
Image credit goes to [Elias G](https://github.com/egarcia28/CircuitPython#wiring-2)
### Reflection
This assignment was good, because it relied more on the code than the wiring. The hardest part was finding the values to put in for the colors, and when the colors would change. I also learned that it's really hard to input each value into a code, than make a code that runs through all the values instead. 



## CircuitPython_LCD

### Description & Code

```python
import board
import math
import time
from lcd.lcd import LCD                                     
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface   
from digitalio import DigitalInOut, Direction, Pull
i2c = board.I2C()
lcd = LCD(I2CPCF8574Interface(i2c, 0x27), num_rows=2, num_cols=16)
btn = DigitalInOut(board.D3)
btn2 = DigitalInOut(board.D2)
btn.direction = Direction.INPUT
btn2.direction = Direction.INPUT
btn.pull = Pull.UP
btn2.pull = Pull.UP
num = 0                     
Redo = True                   

lcd.print("Starting")
while True:                                 
    if btn.value == True and Redo == True:   
        if btn2.value == True:                     
            num = num - 1
        else:
            num = num + 1                                   
        lcd.clear()
        lcd.print(str(num))
        Redo = False
        time.sleep(.1)
    elif btn.value == False and Redo == False:
        Redo = True

```
Code from [Kaz S](https://github.com/kshinoz98/CircuitPython#description--code-2)
### Evidence

![ezgif-2 (1)](https://user-images.githubusercontent.com/112961430/193049640-d5c38adf-456b-498e-aed0-5d23ada84e12.gif)

Image credit goes to [Kaz S](https://github.com/kshinoz98/CircuitPython#evidence-2)
### Wiring
![Screenshot 2022-09-27 144318](https://user-images.githubusercontent.com/112961430/193284020-f79d8161-2984-4a45-8ada-ca9f64faefc4.png)

Image credit goes to [Kaz S](https://github.com/kshinoz98/CircuitPython#wiring-1)
### Reflection
This assignment was challenging for me, because of the time it took to map the sensor. It also took a while to make the led work with the buttons. This assignment was good, because it taught me how to count down with another button, which I have never done before. The last part I struggled with, was finding the right amount of time between each button push. If the time was too short, then the numbers would go up twice when I pressed once. But if the time was too long, then the next time I pressed the button, the button wouldn't be registered. 

## MotorControl

### Description & Code
This assignment was to wire a 6 volt battery pack to a motor, and code the motor to speed up or slow down with a potentiometer. 
```python 
import simpleio
import board
import time
from analogio import AnalogOut, AnalogIn

motor = AnalogOut(board.A5) # assigning motor a pin
pot = AnalogIn(board.A0) # assigning potentiometer a pin

while True:
    print(simpleio.map_range(pot.value, 96, 65520, 0, 65535))
    motor.value = int(simpleio.map_range(pot.value, 96, 65520, 0, 65535)) # maps the motor value to the potentiometer
    time.sleep(0.1)
  ```
  credit goes to [Sofie Chen](https://github.com/sechen12/CircutPython#description--code-4)
### Evidence
https://user-images.githubusercontent.com/112961430/201939869-76edb460-2b1b-4d08-89ad-654778561698.mp4
### Wiring
![2222](https://user-images.githubusercontent.com/112961430/200873816-817fa4d7-c342-4601-816c-1a7b69553254.PNG)
Image credit goes to [google](https://tinyurl.com/45jm7wwn)
### Reflection
This assignment's hardest part was the wiring, because how I needed to use 4 lanes of gnd and 5v on my breadboard, instead of the usual 2 lanes. Another hard part of this assignment, was the wiring of the transistor. I didn't really know how to wire it, until after this assignment. My favorite part of the assignment, was seeing the motor's speed changing when I finished. 

## TemperatureSensor

### Description & Code 
This assignment was to wire a temperature sensor with an lcd to show the temperature on the lcd.
```python
#ctrl alt r
import board
from lcd.lcd import LCD
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface
import time
import analogio

lcdPower = digitalio.DigitalInOut(board.D8)
lcdPower.direction = digitalio.Direction.INPUT
lcdPower.pull = digitalio.Pull.DOWN

TMP36_PIN = board.A0  # Analog input connected to TMP36 output.
i2c = board.I2C()


# Function to simplify the math of reading the temperature.
def tmp36_temperature_C(analogin):
    millivolts = analogin.value * (analogin.reference_voltage * 1000 / 65535)
    return (millivolts - 500) / 10

lcd = LCD(I2CPCF8574Interface(i2c, 0x27), num_rows=2, num_cols=16)
# Create TMP36 analog input.
tmp36 = analogio.AnalogIn(TMP36_PIN)

# Loop forever.
while True:
    lcd.clear()
    lcd.print("Klei")
    # Read the temperature in Celsius.
    temp_C = tmp36_temperature_C(tmp36)
    # Convert to Fahrenheit.
    temp_F = (temp_C * 9/5) + 32
    # Print out the value and delay a second before looping again.
    print("Temperature: {}C {}F".format(temp_C, temp_F))
    time.sleep(1.0)
    
 ```
    
    
### Evidence 
https://user-images.githubusercontent.com/112961430/228257639-0ed277ac-6e27-421a-a1fa-9b5ca44c8bb7.mp4

Image credit goes to [Sofie Chen](https://github.com/sechen12/CircutPython#evidence-5)
### Wiring 
![image](https://user-images.githubusercontent.com/112961430/228250058-b6dfd8ab-b892-461c-b744-1fe0ca629b5e.png)

Video credit goes to [Sofie Chen](https://github.com/sechen12/CircutPython#evidence-5)
### Reflection 
This assignment was definetly the most annoying, because I had to wait until vscode would work with my lcd. The hardest part of the assignment was definetly the lcd. I had trouble connecting the lcd to the arduino and placing the sensors readings on it. My favorite part of the assignment was seeing it work. 

