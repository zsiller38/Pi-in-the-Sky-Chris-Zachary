# Planning
## Objective
Collect flight data using mpu, barometer, ect. and save it to the pico. Create a mechanism to safely return the pico to the ground so that the flight data can be downloaded.
## Proposed Solutions
We have decided to construct either a one or two stage rocket to collect flight data. Both rockets will use a parachute to land
| **1 Stage Rocket** | **2 Stage Rocket** |
| ----- | ----- |
|**Pros:** A one stage rocket is simpiler because there is no stage seperation. Will not go as high so less space is needed for launch. Uses less material and has only one motor so it will be cheaper | **Pros:** Way cooler and will get much higher alowing us to record more data. |
| **Cons:** Might not get as high | **Cons:** Uses more material and needs more space to launch. If the second stage does not fire at the right time the rocket could fire towards the ground. |

After evaluating the pros and cons of each type of Rocket we decided to make a two stage rocket because it would challenege our engineering skills. A two stage rocket, although challegeing, has really cool oppertunities like attaching a small camera to watch the stages seperate. 

## Research
After deciding that we wanted to make some kind of two stage rocket we had two reserch how they work. For this [Apogee Rockets](https://www.apogeerockets.com/Tech/How_2-Stage_Rockets_Work) was very helpful.

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/Rocketpic1.png?raw=true" alt="wiring2" style="width:318px;"> 

There are multiple ways to make a two stage rocket. An electric igniter in the second stage is one way but that requires more electronics and possible issues. Instead we will be using direct staging. In direct staging the booster stage motor does not have a clay cap so when the engine fully burns it will eject burning particles to ignite the nest stage.

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/rocketpic3.png?raw=true" alt="wiring2" style="width:318px;"> <img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/rocketpic4.png?raw=true" alt="wiring2" style="width:318px;">

In the images above you can see how the burning of the booster stage ignites the seconds stage. There is one critical part to note here and that is that the correct motor is used. Most rocket engines have a delay grain and ejection charge. These are used to delay the firing of the nose cone so that the rocket has time to reach its apex and slow down before the parachute is deployed. The booster stage in our rocket cannot have either of these otherwise the direct saging will not work because the stages need to seperate imediately after the booster stage has finished firing. 

<img src="https://github.com/zsiller38/Pi-in-the-Sky-Chris-Zachary/blob/main/Images/Rocketpic2.png?raw=true" alt="wiring2" style="width:318px;"> 

Final Plan
- Our final plan will be a two stage rocket that uses a D-12-0 booster stage rocket and either a C, D, or E upper stage.
- We will use direct staging to ignite the second stage and a small ejection charge in the upper stage motor to deploy the parachute.
- Hopefully we will be able to fit our electronics (Pico, Altimiter, MPU, and maybe camera) inside of the nose cone, but is we cant we will put them somewhere inside the second stage body.
- [Planning doc link](https://docs.google.com/document/d/17WwYuRgZeO-M28lSW4JHtBa9JSogwiJhs65o3TL73Uk/edit)
<img src="" alt="wiring2" style="width:318px;">
