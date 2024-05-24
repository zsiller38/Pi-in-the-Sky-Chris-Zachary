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
Create a two-stage rocket that will house a pico in the nose cone. The rocket will launch and collect data, then the stages will separate and the pico will land safely with a Parachute.

### Bill of Materials
- PICO
- MPU650
- Altimeter
- Body Tube
- Estes E12 Roctet Engine
- Garbage Bag (parachute)
- Basswood
- 3d Printed Parts
- Nylon Cord
- Screw
- Guide tube
- Ignitor

## Weekly updates
### January
Week 1-2 
- Finalized two-stage rocket design and what sensors we are using.
- Decided on rocket motors and proportions of the rocket.
- Began CAD design for nose cone that will house electronics.  

Week 3-4 

- Ordered fuselage tube and parachute.
- Worked on nose cone design to house electronics.
- Began writing code for altimeter and mpu 6050.

### February 

Weeks 1-2 
- Got the 3D-printed internals designed and tested.
- Finished the initial code and began to plan the sodering and final electronics
- Started simulations for the rocket and measured ideal performance.

Weeks 3-4 
- Reworked the soldering as it turned out that the way that it was done was improper.
- Finished all of the rocket body construction.

### March
Weeks 1-2 
- Finally figured out the soldering and code and made them work together.
- Started on fins

Weeks 3-4
- Lost the code and had to start over
- Finished fins and attached them to body
- Finished the code and tested it

### April

Weeks 1-3
- Worked out all the minor prelaunch problems.
- Acquired the things necessary to launch ( launch platform, a working launcher, igniters, safety glasses, etc.)
- Painted the rocket in some cool designs.

Week 4 
- Finish all the prep and find a place to launch.
- Launch


## Design

### Simulations
To ensure that our rocket would fly properly and get a rough estimate of the height and range it would travel. To do this we used the software OpenRocket. OpenRocket is a free software that runs flight simulations on rocket models. In OpenRocket you can build a rocket to your specifications and then run simulations on it.

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/SIM%20Images/Openrockethome.PNG?raw=true" alt="ButtonCounter" style="width:500px;">

**OpenRocket home screen**

OpenRocket has all of the parts needed to create a rocket like, body tubes, fins, nose cones, parachutes, shockcords, and stage connectors. In addition, there is the ability to add weighted objects to simulate the pico. All of these features allowed us to create a complete rocket in onshape to run simulations on. 
**Note Open Rocket does not create a CAD model that can be used to cut or print parts. Those parts must be recreated in onshape.**

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/SIM%20Images/Upperstagedesign.png?raw=true" alt="ButtonCounter" style="width:500px;">

**Our rocket design**

We then ran simulations using the upper stage of the rocket(only E motor) and the full rocket(D and E motor).

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/SIM%20Images/Upperstagesim.png?raw=true" alt="ButtonCounter" style="width:500px;">

**Only E motor**

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/SIM%20Images/Fullrocketsim.png?raw=true" alt="ButtonCounter" style="width:500px;">

**D and E motor**

A very important step in building a rocket is stability. There are two important parts of stability: the center of pressure and the center of gravity. The center of pressure is the average point of pressure exerted on the rocket. The center of gravity is the average point of all the mass or balancing points. For a rocket to be stable the center of pressure must be 1-2 rocket diameters behind the center of gravity. If this is not the case the rocket can start tumbling or do something called weather cocking where the rocket will turn and fly into the headwind. OpenRocket allowed us to test the stability of our rocket before we launched it and gave us a rough estimate for the launch apogee. The software is very good considering it is free and we would definitely use it again for flight simulations.

### CAD
[CAD link](https://cvilleschools.onshape.com/documents/d0422704b3fcc13e8ccf8ef9/w/5dade6d73cbd18de400186fe/e/d3a699f6cfd285245c7cf91a)
As mentioned earlier the goal of OpenRocket is not as a 3d design software so although we have the template of the rocket as the simulator we cannot directly make parts from that. We still had to use Onshape to create a 3d model of the rocket to print. But, because we had the optimal dimensions in the OpenRocket design creating the parts in onshape was very simple.
| Booster Cap | Booster Connector | Motor Holder | Upper Connector |
| ---- | ---- | ---- | ---- |
| <img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/CAD%20Images%201/Boostercap.png" alt="picture" style="width:100px;"> | <img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/CAD%20Images%201/Lowerconnection.png" alt="picture" style="width:100px;"> | <img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/CAD%20Images%201/Engineholder.png" alt="picture" style="width:100px;"> | <img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/CAD%20Images%201/Upperconnection.png" alt="picture" style="width:100px;"> |

One onshape feature that was cool to use was the exploded view. It allowed us to view how the rocket stages would fit together without making the full rocket.

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/CAD%20Images%201/Explodedviewrocket.png?raw=true" alt="picture" style="width:500px;">

**Exploded View**

The design process for this project was much different than other projects I had done. Aside from initial planning nearly the entire design process took place in OpenRocket and was then translated to onshape. It was also unique in the fact that the design was not technically challenging (the modeling process was not hard or technical) but the process of finding the ideal dimensions for the fins, nose cones, and body tube took a long time and required a lot of tweaking. There is not much to do to streamline this process you kind of have to just try new design shapes and see what improves stability or aerodynamics.

## Code

### Goal of the Code
The overarching goal of the project was to collect flight data. We achieved this by collecting acceleration and altitude data. We used an MPU6050 to collect acceleration and an altimeter for altitude. These sensors will record data at certain time intervals and record it in the Pico's memory. Then we can upload the stored data by reconnecting the pico to the computer.

### Commented Code

``` python
# type: ignore 


import adafruit_mpl3115a2
import time
import board # importing the board and all the necessary starting bits
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

            #print(f"x:{ x} y:{y} z:{z}") # This is an F string which lets us put a variable that is changing in our serial monitor or in an OLED or LCD
            time.sleep(.1)

  

    

```

**Code file**

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
**Boot.py file**

### Purpose of Boot.py
Boot.py is a file name that tells the pico to run this code whenever it starts up. This is what allows us to switch between code and data mode. If the file is named anything other than Boot.py it will not work and the file must be saved to the pico before running the rest of the code.

### Reflection
The code in this project wasn't super difficult although it did need us to cover new concepts that we hadn't before. We used both an altimeter and an accelerometer and had them both copy values into a file held on the pico. Some problems that I did run into were making the boot file work so that there would be a code and data mode and having both the accelerometer and altimeter work on the same SCL and SDA. The boot file took many attempts and was really only a matter of trial and error until it finally worked. Mr. Miller explained how it worked to me about four times but on the fifth time I got it and it worked. I recorded data in the lab that was then safely saved onto the pico now suspended in a tree. The SDA and SCL working together was much more a syntax issue of figuring out how I2C worked. 
Initially, we needed to make a code for the altimeter and accelerometer separately, but we had already done a project with an accelerometer but the altimeter needed more work. 

## Wiring

### Description of Wiring Components
The wiring uses a pico, MPU6050, altimeter, and a switch. The MPU6050 and altimeter are both wired to the same SCL and SDA pins. The switch enables us to change between code and data mode.

### Wiring Image

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/assets/71402927/191ded53-5bbe-4360-9958-59edcde8da36" alt="hi" style="width:500;">

**Wiring Diagram**

### Reflection
The wiring was probably the simplest  part of this and only required minimal knowledge to complete but it took a few attempts to solder. The one problem that we did run into was making it all solder the way in which Matthew Miller wanted it to be. It took many attempts to make the solder work the way they wanted it to, and in the future, we definitely need to plan out more clearly what we are soldering. 

## Construction
The rocket has several parts that were not as simple as printing or cutting a part and boom you're done. Each of the following parts fit this bill and had unique challenges.

### Body Tube
The body tube was purchased online as the ones we had in the lab were too small and making our own tube would take too long and yield an inferior result. The tobe was cut using a band saw and tape was wrapped around the section of tube being cut to create cleaner cut edges. 

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/construction/bodytube.jpg?raw=true" alt="ButtonCounter" style="width:250px;">

The tube we got was slightly wider than it needed to be because we overestimated how much space we would need to fit the pico. This contributed to a heavier rocket and more work for us. We also had difficulty figuring out where to cut the tube to form each stage. The middle section needed to house the second stage, wadding, parachute, and shock cord. It the space is to small the Parachute won't deploy properly and if it is too big the Parachute also won't deploy properly.

### Parachute
We considered two parachutes for our design. The first one we bought and the second one we made. We used the Parachute made because we were concerned the other one would be to small and the nose cone would depend too quickly. The one we used was made from a garbage bag and some twine. We did some math (website name) to find the approximate diameter of our Parachute. After that, we cut the garbage bag to size and attached the strings. When we launched the parachute worked a little too well. It deployed perfectly but did not allow for the nose cone to descend fast enough allowing it to get carried into a tree. In hindsight, we should have used the smaller Parachute but we think our concerns about it being too small were justified.

### Fins
The fins are arguably the most important part of our rocket. If they break or are incorrectly shaped our rocket could tumble and crash. The fins are made from basswood because of its flexibility. Basswood can be bent without permanent deformation so if a fin gets bent it is unlikely to permanently damage the rocket. 

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/construction/Finpic.jpg?raw=true" alt="ButtonCounter" style="width:250px;">

We used the laser cutter to cut out the fin shape and then sanded the edges to create an airfoil. An airfoil is a type of fin taper that drastically increases the apogee of the rocket. ([website or airfoils](https://www.apogeerockets.com/education/downloads/Newsletter305.pdf)) The airfoil is something we wish we had never done. Although it undeniably improves aerodynamics, sanding the airfoils without a premade jig was a nightmare and was not worth the effort that it required. An argument can also be made that because the sanding was not uniform it could have worsened the rocket's aerodynamics.

### Shock Cord
A shock cord is a rope that connects the stages that split apart when the parachute is deployed. The upper-stage rocket engine has a bit of black powder that is on a delay that provides the force to pop the nose cone. When the nose cone pops off the shock cord serves two purposes: it connects the stages that separated so they don't land in two places and it allows the force of the separation charge to dissipate without damaging the rocket. The length of the cord should be somewhere around 2 to 3 times the length of the rocket stage. If it is longer than this the cord could get tangled in the parachute and prevent full deployment. If it is shorter when the stages separate they could collide with each other and at this speed that could damage the nose cone, although that is unlikely. There are several material options for shock cords: elastic, kevlar, and nylon. An elastic cord does a better job absorbing forces but it is more prone to snapping. Out of the other two options kevlar, and nylon we chose nylon because we did not need the extra strength required by kevlar. 

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/construction/shockcordpic.jpg?raw=true" alt="ButtonCounter" style="width:250px;">

**Shock Cord Design. The cord was connected to the body tube and nose cone with the parachute connected halfway in between.**
To connect the shock cord to each section of the rocket we inserted it into a hole and then held it in place with a screw. To connect it to the booster stage we used hot glue. When we launched the rocket our shock cord completely failed. The nose cone with the pico disconnected from the main stage. We think this happened because the heat created by the separation melted the hot glue allowing the cord to disconnect for the tube. The cord remained attached to the nose cone because the parachute was still connected to the nose cone and working.


## Launch
We launched on April 30th to mixed results, on the one hand, the rocket performed wonderfully and the average position of the rocket was exactly where we wanted it to be. On the other, the rocket split in two and one part ended up stuck in a tree and the other lost in the woods(see picture) 

<img src="https://github.com/cprocino/PiInTheSky/assets/71406784/a22ea83e-a512-4837-898e-5f8d7d3cde0d" alt="hi" style="width:500;">

**Flight Path**

The middle dot is where we launched from, the top dot is where the nose cone and electronics landed and the bottom dot is the estimated position of the bottom half is. 

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/assets/71406784/42faeb18-75a2-4e6f-a125-73a535b3219d" alt="hi" width="style:500px;">

**Nose cone landing place**

<img src="Images/Launch Images/My Project (9).gif" alt="picture" style="width:900px;">

**Video of Launch**

### What went well
- Our rocket launched first try with no issues with the ignitor or launch button.
- The rocket went high and was stable throughout the flight.
- The stage separated after the correct delay.
- The parachute deployed after the apogee allowing for maximum height.
- Nothing became tangled or prevented stage separation.
- The parachute was large enough to allow for a slow descent. 

### What we think went wrong

There are many small things that could be improved upon that we touched on in earlier sections. Here is a list of the primary issues.
- The shock cord failing meant there was less weight on the parachute (only the nose cone was connected rather than the nose cone and main stage. 
- Because there was less weight on the parachute the descent was slower allowing for the payload to be carried on the wind.
- In theory, we had enough space but the slower descent meant the range was much larger than anticipated.
- We launched in the wrong direction. Our launch site could have been in a better spot that would have given us a large area.

### Fixes
- Pick a spot with more space than you think you need.
- We picked this spot because of its accessibility and convenience, but we should have picked a large spot.
- Spend more time examining the uses of each part. It should have occurred to us that the shock cord linkage points would be exposed to higher heat and pressure than other parts of the rocket so we should have spent more time examining our design.

In the future of our rocket-building careers, we should probably find a bigger place to launch and make sure that our rocket doesn't break apart. 

## Reflection
In conclusion, we enjoyed this project. It was noticeably different from engineering projects we had done in previous years. Building the rocket required a lot of research that other projects did not require. However, certain things we researched like airfoils, exact parachute size, and nose cone geometry, provided marginal improvements that were unnecessary given that we were not trying to create a finely tuned optimized rocket. It was fun to dive into the rabbit hole of rocketry because there is so much to learn.
Here are some tips we would give to future model rocket builders.
- Buy a prefab model. We enjoyed making our own rocket but there are so many other engineering challenges that buying a model will save you time.
- Use OpenRocket: it is a fantastic simulation service especially given it is free.
- The Apogee Peak of Flight newsletter dives into the specifics of designing all parts of a rocket and gives us some very useful advice.

Overall this was a very good learning experience as it taught us many lessons and provided an endless stream of challenges. The launch was so cool but the end result of the pico stuck in a tree was disappointing.





