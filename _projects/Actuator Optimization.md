---
layout: project
title: Actuator Optimization
description: Optimizing the weight/height of a weight on the end of a bar.
technologies: [python]
image: https://drive.google.com/file/d/1Cl6nXDQFrBNmpyZlJTQFniID-xDC9Tk6/view?usp=sharing

---


The object of this assignment was to optimize the height difference and weight exerted on a bar as it was pushed upwards by an actuator. To do this, I started by completing a rough sketch of the system with all relevant variables. Once I had these variables, I decided to focus on optimizing weight, so I decided to give my actuator the greatest lever arm by placing it at the end of the bar, where the weight was placed. I also wanted to eliminate the angle phi from my sketch, so I set phi to equal 90-theta (creating a perpendicular angle). Then I was able to create the equation in one of the above images by taking the moment about the left-bottom corner, which I designated as the origin.

I used an IMA 33 3-stack, which had an inital length of 21.67cm and a peak thrust force of 11.1KN.

From there, I created the following python code in pycharm to plug random values in for the unknown variables, in order to optimize the problem:

import random
import math

Fa=11.1
w=0
wmax=w
iterations=1000000
bestp=0
bestL=0
bestx=0
a=0
cnt=0

for i in range(iterations):

    #Finding max weight

    p=random.uniform(0,(math.pi)/2)  #angle theta

    Ly=50*math.sin(p)
    Lx=150*math.cos(p)
    L=math.sqrt(Lx**2+Ly**2)

    x=L*random.random()


    w=(Fa*math.sin((math.pi)-p)*(L-x)*(math.cos(p))-(Fa*math.cos((math.pi)-p)*(L-x)*math.sin(p)))/(L*math.cos(p))

    #restricting based on constraints

    m=Ly/Lx

    xactuator=-m*(-Ly-(Lx/m))


    if w>wmax and xactuator<150:

        wmax=w
        bestp=p*(180/(math.pi))
        bestL=L
        bestx=x
        aLy=Ly
        aLx=Lx


print(f'''
    The optimal weight is {wmax:.2f}\n
    The optimal angle (degrees) is {bestp:.2f}\n
    The optimal L value is {bestL:.2f}\n
    The optimal x value is {bestx:.2f}\n
    The bar meets the ceiling at the point ({aLx:.2f}, {aLy:.2f})''')

The output of this code is as follows:

    The optimal weight is 22.01

    The optimal angle (degrees) is 82.67

    The optimal L value is 53.15

    The optimal x value is 0.02

    The bar meets the ceiling at the point (19.13, 49.59)

(There is some slight variation in outputs because of the random nature of the script.)

Now that I created these values, I was able to create a drawing to scale for the scenario based on my assumptions (pictured above).

Through this, I was able to find that the optimal weight is 22.01, and my max height was a change of 47.2cm.


