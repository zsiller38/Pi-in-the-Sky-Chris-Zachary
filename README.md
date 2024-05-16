# Pi in the Sky

# Table of Contents
* [Planning](#Planning)
* [Design](#Design)
* [Code](#Code)
* [Wiring](#Wiring)
* [Construction](#Construction)  
* [Reflection](#Reflection)




## Objective
To measure and record flight data using a flying machine
## Planning
This is our planning document reused from the [Engineering 3 planning doc](https://docs.google.com/document/d/17WwYuRgZeO-M28lSW4JHtBa9JSogwiJhs65o3TL73Uk/edit#heading=h.ukbi0a75zb46).





## Weekly updates
### January
Week 1 (2-5)
- Finalized two-stage rocket design and what sensors we are using.
- Decided on rocket motors and proportions of the rocket.
- Began CAD design for nose cone that will house electronics.  

Week 2 (8-12)

- Ordered fuselage tube and parachute
- Worked on nose cone design to house electronics
- Began writing code for altimeter and mpu 6050.
Week 3 (16-19)

### Febuary 

Weeks 1-2 (2-16)
- got the 3D printed internals designed and tested
- finished the initial code and began to plan the sodering and final electronics
- started simulations for the rocket and mesured ideal performance.

Weeks 3-4 (19-1)
- reworked the soldering as it turned out that the way that it was done was inproper
- finished all of the rocket body construction 
### March
Weeks 1-2 
- finaly figure out the soldering and code and began to make them work together
- started on fins

Weeks 3-4
- lost the code and had to start over
- finished fins and attached them to body
- finished the code and tested it

### April

Weeks 1-3
- worked out all the mino prelaunch problems
- aquired all the things nessecary to launch ( launch platform, a working launcher, ignighters, safety glasses, ect.)
- painted the rocket in some cool designs

Week 4 
- finish all the prep and found a place 
- launched it
  


## Design
### CAD
### Simulations
## Code
### Code
``` python
# type: ignore 


import adafruit_mpl3115a2
import time
import board # importing the board and and all the nessecary starting bits
import digitalio
import adafruit_mpu6050
import busio

sda_pin = board.GP14   # setting up the pin for SDA
scl_pin = board.GP15   #  setting up the pin for Scl
i2c = busio.I2C(scl_pin, sda_pin)    # setting up the i2c var
mpu = adafruit_mpu6050.MPU6050(i2c)  # setting up the mpu var
alt = adafruit_mpl3115a2.MPL3115A2(i2c)
#alt.sealevel_pressure = 103040 

with open("/data.csv", "a") as datalog:
    #this line opens the file data.txt and appends info to the end of it
        while True:
           
            datalog.write(alt)
            
            datalog.flush()
            time.sleep(0.25)
            print(f"X: {mpu.acceleration[0]} m/s^2")   #prints the x values
            print(f"Y: {mpu.acceleration[1]} m/s^2")   #prints the y values
            print(f"Z: {mpu.acceleration[2]} m/s^2")  #prints the z values
            time.sleep(1)
            print()
            
            altitude = alt.altitude
            print('Alt: {0:0.3f} meters'.format(alt.altitude))
        

            # x = round(mpu.acceleration[0],3)
            #y = round(mpu.acceleration[1],3)
            #z = round(mpu.acceleration[2],3)

            #print(f"x:{ x} y:{y} z:{z}") # This is an F string which lets us put a variable that is changing in our serial monitor or in a OLED or LCD
            time.sleep(.1)

  

    

```



``` python
# SPDX-FileCopyrightText: 2021 Kattni Rembor for Adafruit Industries
# Modified by Matthew Miller, Charlottesville High School

# SPDX-License-Identifier: MIT

"""
boot.py file for Pico data logging example. If pin GP0 is connected to GND when
the pico starts up, make the filesystem writeable by CircuitPython.
"""
import board
import digitalio
import storage
import time

write_pin = digitalio.DigitalInOut(board.GP0)
write_pin.direction = digitalio.Direction.INPUT
write_pin.pull = digitalio.Pull.UP

led = digitalio.DigitalInOut(board.LED)
led.direction = digitalio.Direction.OUTPUT
time.sleep(2)

# If write pin is connected to ground on start-up, CircuitPython can write to CIRCUITPY filesystem.
if not write_pin.value: # Data Mode, shown by 10 short blinks
    storage.remount("/", readonly=False)
    for i in range(10):
        led.value = True
        time.sleep(0.1)
        led.value = False
        time.sleep(0.1)
        i = i+1

else: # Code Mode, shown by three long blinks
    for i in range(3):
        led.value = True
        time.sleep(0.5)
        led.value = False
        time.sleep(0.5)
        i = i+1
  

    

```
The code in this project wasn't super difficult although it did need us to cover new concepts that we hadn't before. We used both an altimeter and accerlerometer and had them both copy values into a file held on the pico. Some problems that I did run into were making the boot file work so that there would be a code and data mode and having both the accelerometer and altimeter work on the same SCL and SDA. The boot file took many attempts and was really only a matter of trial and error until it finaly worked. Mr. Miller explained how it worked to me about four times but on the fifth time i got it and it worked. I recorded data in the lab that was then safely saved onto the pico now suspended in a tree. The SDA and SCL working together was much more a syntax issue of figuring out how I2C worked. 
Initialy we needed to make a code for the altimeter and accerlorometer seperately, We had alread done a project with an accerlometer but the altimeter needed more work. 

### Wiring 
The wiring was probably the simplest  part of this and only required minimal knowledge to complete but took a few attempts to solder. 
Here it is on paper:


![WIN_20240222_13_32_27_Pro](https://github.com/cprocino/PiInTheSky/assets/71406784/fc46c44f-9fdc-4f43-b80d-ba51456fbb50)

The one problem that i did run into was making it all solder the way in which Matthew Miller wanted it to be. It took may attempts to make the solder work the way the wanted it to, and in the future i definately need to plan out more clearly what i am soldering. 

## Construction
### Body Tube
### Parachute
### Fins
### Nose Cone and Shock Cord
## Launch
We launched on april 30th to mixed result, on the one hand the rocket preformed wonderfully and the average position of the rocket was exactly were we wanted it to be. On the other the rocket split in two and one part ended up stuck in a tree and the other lost in the woods(see picture) 

![Screenshot 2024-05-07 132944](https://github.com/cprocino/PiInTheSky/assets/71406784/a22ea83e-a512-4837-898e-5f8d7d3cde0d)
the middle dot is where we launched from, the top dot is where the nose cone and electronics landed and the bottom dot is the estimated position of the bottom half is. 

Here is the nose stuck in the tree

![Screenshot 2024-05-14 130019](https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/assets/71406784/42faeb18-75a2-4e6f-a125-73a535b3219d)

In the future of our rocket building careers we should probably find a bigger place to launch and make sure that our rocket doesn't break apart. 

## Reflection



