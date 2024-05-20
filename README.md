# Pi in the Sky

## Table of Contents
* [Planning](#Planning)
* [Design](#Design)
* [Code](#Code)
* [Wiring](#Wiring)
* [Construction](#Construction)  
* [Launch](#Launch)
* [Reflection](#Reflection)


## Planning
See [Engineering 3 planning doc](https://docs.google.com/document/d/17WwYuRgZeO-M28lSW4JHtBa9JSogwiJhs65o3TL73Uk/edit#heading=h.ukbi0a75zb46) and planning Readme

### Objective
To measure and record flight data using a flying machine.
### Solution
Create a two stage rocket that will house a pico in the nose cone. The rocket will launch and collect data, then the stages will seperate and the pico will land safely with a Parachute

### Bill of Materials

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
As mentioned earlier the goal of OpenRocket is not as a 3d design software so although we have the template of the rocket is the simulator we cannot directly make parts from that. We still had to use Onshape to create 3d model of the rocket to print. But, because we had the optimal dimensions in the OpenRocket design creating the parts in onshape was very simple.
| Booster Cap | Booster Stage Connector | Second Motor Holder | Upper Stage Connector |
| ---- | ---- | ---- | ---- |
| <img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/CAD%20Images%201/Boostercap.png" alt="picture" style"width:100px;"> | <img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/CAD%20Images%201/Lowerconnection.png" alt="picture" style"width:100px;"> | <img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/CAD%20Images%201/Engineholder.png" alt="picture" style"width:100px;"> | <img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/CAD%20Images%201/Upperconnection.png" alt="picture" style"width:100px;"> |

One onshape feature that was cool to use was the exploded view. It allowed us to view how the rocket stages would fit together without making th full rocket.
<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/CAD%20Images%201/Explodedviewrocket.png?raw=true" alt="picture" style"width:500px;">
The design process for this project was much different than other projects I had done. Aside from initial planning nearly the entire design process took place in OpenRocket and was then translated to onshape. It was also unique in the fact that the design was not technically challeging (the modeling process was not hard or technical) but the process to find the ideal dimensions for the fins, nose cones, and body tube took a long time and required a lot of tweaking. There is not much to do to streamline this process you kind of have to just try new design shapes and see what improves stability or aerodynamics.

### Simulations
To ensure that our rocket would fly properly and get a rough estimate of the height and range it would travel. To do this we used the software OpenRocket. OpenRocket is a free software that runs flight simulations on rocket models. In OpenRocket you can build a rocket to your specifications and then run simulations on it.

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/SIM%20Images/Openrockethome.PNG?raw=true" alt="ButtonCounter" style="width:500px;">

**OpenRocket home screen**
OpenRocket has all of the parts needed to create a rocket like, body tubes, fins, nose cones, parachutes, shockcords, and stage connectors. In addition there is the ability to add weighted objects to simulate the pico. All of these features allowed us to create a complete rocket in onshape to run simulations on. **Note open rocket does not create a cad model that can be used to cut or print parts. Those parts must be recreated in onshape.**

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/SIM%20Images/Upperstagedesign.png?raw=true" alt="ButtonCounter" style="width:500px;">

**Our rocket design**

We then ran simulations using the upper stage of the rocket(only E motor) and the full rocket(D and E motor).

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/SIM%20Images/Upperstagesim.png?raw=true" alt="ButtonCounter" style="width:500px;">

**Only E motor**

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/SIM%20Images/Fullrocketsim.png?raw=true" alt="ButtonCounter" style="width:500px;">

**D and E motor**

A very important step in building a rocket is stability. There are two important parts of stability: center of pressure and center of gravity. Center of pressure is the average point of pressure exerted on the rocket. Center of gravity is average point of all the mass or balancing point. For a rocket to be stable the center of pressure must be 1-2 rocket diameters ahead of the center of gravity. If this is not the case the rocket can start tumbling or do something called weather cocking where the rocket will turn and fly into the headwind. OpenRocket allowed us to test the stability of our rocket before we launched it and gave us a rough estimate for the launch apogee. The software is very good considering it is free and we would definitely use it again for flight simulations.


## Code

### Goal of the Code

### Commented Code

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
### Reflection
The code in this project wasn't super difficult although it did need us to cover new concepts that we hadn't before. We used both an altimeter and accerlerometer and had them both copy values into a file held on the pico. Some problems that I did run into were making the boot file work so that there would be a code and data mode and having both the accelerometer and altimeter work on the same SCL and SDA. The boot file took many attempts and was really only a matter of trial and error until it finaly worked. Mr. Miller explained how it worked to me about four times but on the fifth time i got it and it worked. I recorded data in the lab that was then safely saved onto the pico now suspended in a tree. The SDA and SCL working together was much more a syntax issue of figuring out how I2C worked. 
Initialy we needed to make a code for the altimeter and accerlorometer seperately, We had alread done a project with an accerlometer but the altimeter needed more work. 

## Wiring

### Description of Wiring Components

### Wiring Diagram
![WIN_20240222_13_32_27_Pro](https://github.com/cprocino/PiInTheSky/assets/71406784/fc46c44f-9fdc-4f43-b80d-ba51456fbb50)

### Reflection
The wiring was probably the simplest  part of this and only required minimal knowledge to complete but took a few attempts to solder. The one problem that i did run into was making it all solder the way in which Matthew Miller wanted it to be. It took may attempts to make the solder work the way the wanted it to, and in the future i definately need to plan out more clearly what i am soldering. 

## Construction
The rocket has several parts that were not as simple as printing or cutting a part and boom your done. Each of the following parts fit this bill and had unique challenges.

### Body Tube
The body tube was purchased online as the ones we had in the lab were to small and making our own tube would take to long and yield and inferior result. The tobe was cut using a band saw and tape was wrapped around the section of tube being cut to create cleaner cut edges. 
picture of tube
The tube we got was slightly wider than it needed to be because we overestimated how much space we would need to fit the pico. This contributed to a heavier rocket and more work for us. We also had difficulty figuring out where to cut the tube to form each stage. The middle section needed to house the second stage, wadding, parachute, and shock cord. It the space is to small the Parachute won't deploy properly and if it is to big the Parachute also won't deploy properly.

### Parachute
We considered two parachutes for our design. The first one we bought and the second one we made.
Pictures of both.
We used the Parachute made because we were concerned the other one would be to small and the nose cone would depend too quickly. The one we used was made from a garbage bag and some twine. We did some math (website name) to find the approximate diameter our Parachute should be. After that we cut the garbage bag to size and attached the strings. 

### Fins
The fins are arguably the most important part of our rocket. If they break or are incorrectly shaped our rocket could tumble and crash. The fins are made from basswood because of its flexibility. Basswood can be bent without permanent deformation. 
picture of fins
We used the laser cutter to cut out the fin shape and then sanded the edges to create and airfoil. An airfoil is a type of fin taper that drastically increase the apogee of the rocket(website)

### Nose Cone and Shock Cord


## Launch
We launched on april 30th to mixed result, on the one hand the rocket preformed wonderfully and the average position of the rocket was exactly were we wanted it to be. On the other the rocket split in two and one part ended up stuck in a tree and the other lost in the woods(see picture) 

![Screenshot 2024-05-07 132944](https://github.com/cprocino/PiInTheSky/assets/71406784/a22ea83e-a512-4837-898e-5f8d7d3cde0d)
the middle dot is where we launched from, the top dot is where the nose cone and electronics landed and the bottom dot is the estimated position of the bottom half is. 

Here is the nose stuck in the tree

![Screenshot 2024-05-14 130019](https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/assets/71406784/42faeb18-75a2-4e6f-a125-73a535b3219d)

In the future of our rocket building careers we should probably find a bigger place to launch and make sure that our rocket doesn't break apart. 

## Reflection

### Overview
This was a very good learning experience as it tought us many lessons, one important one was to doccument more often. We lost all of our data in a tree, and in the future we need to launch in a safer place and also doccument all we can when we can. Both of those problem can and could have been solved with careful planning but tragicly we did not plan very well and now are rocket is split in two and stuck in the woods. 

### Lessons Learned


