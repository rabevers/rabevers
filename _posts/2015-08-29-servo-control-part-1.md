---
layout: post
title: Servo controller part 1
---

There are several types of servos that can be used as actuators for a mobile robot. Analog servos being the most common and cheapest. Next are digital servos. They are
more expensive, work the same way as analog servos but have several advantages with regards to torque and reaction time. The most expensive, but probably the best for
robot applications are the [Dynamixel smart servo motors](http://en.robotis.com/index/). They are also by far the most expensive and hardly realistic for a hobby robot
builder.

The servo controller I intend to build will therefor be working with analog servos since they are more widely available, accepted and cheaper.

# Control theory

The theory behind controlling an analog servo is relatively easy. They respond to a 50hz pwm signal. That means a signal must be repeated every 20ms. The length
of the pulse within the 20ms determine the position the servo will attempt to reach. If the servo is already at that position it will remain there.

![Servo pwm diagram](/images/servo-pwm.png)

Period (P) will occur 50 times in one second. The amplitude in our case will be the voltage level in the MSP430’s I intend to use. Which is 3.3V. The duty cycle
is the important part in this story since it determines the position of the servo.

Some reading has shown me that the center servo position is often reached by setting a 1.5 ms duty cycle. Once at that position the duty cycle must remain
the same in order to keep it at that position.


Setting a smaller duty cycle the servo will turn left to the corresponding position, setting a larger duty cycle will turn the servo right to the corresponding
position.

**Please keep in mind that the center or neutral position does not always correspond to 1.5ms pulses, this seems to be related to the degrees of motion a particular
servo has. In order to find the center position one would have to calibrate the servo controller for a servo.**

This theory controls a single servo. If we wish to control more than one servo (which we do) we will need to do this for each one. Since the pulse train is
continuous a single micro controller could fill up all of its time controlling just the single servo.

This means we have to get creative with how we make the micro controller spend its time. As much as I would like to take credit for all this information I have
to admit most of it comes from other sources.

The people over at [Pololu](https://www.pololu.com/) wrote an excellent series of blog posts about servo control. starting with
[Servo, servo motor, servomotor (definitely not server)](https://www.pololu.com/blog/15/servo-servo-motor-servomotor-definitely-not-server).
Another Important source is [l'Hexapod](http://www.lhexapod.com/blog/). A blog by Len Holgate on his own endeavor to create a hexapod robot.

Both sources are several years old 2011 and 2010 respectively but still valid today. Both seem to have chosen a different way of accomplishing
the control of multiple servos with a single micro controller.

I was some time ago that I read the Pololu series. I will read their solution again and determine what my solution will be. That is for a next post.
