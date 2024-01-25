# Planning
## Objective
Collect flight data using mpu, barometer, etc., and save it to the pico. Create a mechanism to safely return the pico to the ground so that the flight data can be downloaded.
## Proposed Solutions
We have decided to construct either a one or two-stage rocket to collect flight data. Both rockets will use a parachute to land
| **1 Stage Rocket** | **2 Stage Rocket** |
| ----- | ----- |
|**Pros:** A one-stage rocket is simpler because there is no stage separation. Will not go as high so less space is needed for launch. It uses less material and has only one motor so it will be cheaper | **Pros:** Way cooler and will get much higher allowing us to record more data. |
| **Cons:** Might not get as high | **Cons:** Uses more material and needs more space to launch. If the second stage does not fire at the right time the rocket could fire towards the ground. |

After evaluating the pros and cons of each type of Rocket we decided to make a two-stage rocket because it would challenge our engineering skills. A two-stage rocket, although challenging, has really cool opportunities like attaching a small camera to watch the stages separately. 

## Research
After deciding that we wanted to make a two-stage rocket we had to research how they work. For this [Apogee Rockets](https://www.apogeerockets.com/Tech/How_2-Stage_Rockets_Work) was very helpful.

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/Rocketpic1.png?raw=true" alt="wiring2" style="width:318px;"> 

There are multiple ways to make a two-stage rocket. An electric igniter in the second stage is one way but that requires more electronics and possible issues. Instead, we will be using direct staging. In direct staging, the booster stage motor does not have a clay cap so when the engine fully burns it will eject burning particles to ignite the nest stage.

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/rocketpic3.png?raw=true" alt="wiring2" style="width:318px;"> <img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/rocketpic4.png?raw=true" alt="wiring2" style="width:318px;">

In the images above you can see how the burning of the booster stage ignites the second stage. There is one critical part to note here and that is that the correct motor is used. Most rocket engines have a delay grain and ejection charge. These are used to delay the firing of the nose cone so that the rocket has time to reach its apex and slow down before the parachute is deployed. The booster stage in our rocket cannot have either of these otherwise the direct staging will not work because the stages need to separate immediately after the booster stage has finished firing. 

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/Rocketpic2.png?raw=true" alt="wiring2" style="width:318px;"> 

As part of our research, we also launched a small rocket from a kit. The launch was successful after a few tries, but there were some important lessons and things to note from the experience.

- Read instructions carefully if they are given. Although our rocket worked we did not build it entirely correctly. Not all of this was our fault because the instruction did ask us to use parts of the instruction to complete the rocket, which made it harder to read the instructions.

- Rocket ignitors can be finicky. We had two dud launches because either our trigger was not working or the ignitor was not touching the rocket propellant.

- Bring spare parts to the test launch. For the first two launches, we did not bring spare ignitors or motors, so when an ignitor fired but the rocket didn't start we wasted the whole day doing nothing. The third time we brought a spare ignitor and when the rocket didn't work the first time we replaced the ignitor and it worked.

The test launch was very useful because it helped us get accustomed to rocket launch procedures and troubleshooting which will save us time when we launch our final rocket. 

## Final Plan
- Our final plan will be a two-stage rocket that uses a D-12-0 booster stage rocket and either a C, D, or E upper stage.
- We will use direct staging to ignite the second stage and a small ejection charge in the upper stage motor to deploy the parachute.
- Hopefully, we will be able to fit our electronics (Pico, Altimiter, MPU, and maybe camera) inside of the nose cone, but if we can't we will put them somewhere inside the second stage body.
- [Planning doc link](https://docs.google.com/document/d/17WwYuRgZeO-M28lSW4JHtBa9JSogwiJhs65o3TL73Uk/edit)
<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/rocketplan.jpg?raw=true" alt="wiring2" style="width:318px;">
Possible rocket plan

## Risk Mitigation 
Launching rockets can be dangerous if we aren't careful. Rockets being high speed projectiles that excert large amounts of heat and force must be taken seriously. Here are some things we will do to make sure our rocket launches are safe.

- Always wear saftey glasses while launching the rocket to prevent injuries from debris.
- When launching the rocket follow rocket checklist and stay at least 5 meters from launch site.
- Launch rockets in a safe location that is relatively deserted.
- Make sure wind is not to strong on launch day so that wind will not create a massive recovery radius.
- Run a simulation of rocket flight to get a general idea of range and altitude to prepare for actual launch day.

## Block Code
Block code is a general plan of the code logic and when certain types of data will be recored. 

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/blockcoderocket.jpg?raw=true" alt="wiring2" style="width:250px;">

