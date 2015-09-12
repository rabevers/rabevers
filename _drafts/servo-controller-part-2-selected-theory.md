---
layout: post
title: Servo controller part 2 - Theory
---

After reading posts on [Pololu](https://www.pololu.com/blog) and [l'Hexapod](http://www.lhexapod.com/blog/) I decided the control theory of [l'Hexapod](http://www.lhexapod.com/blog/)
seems like a better fit. He seems to have a greater control over the servo timing and pulse train. I'm assuming this control comes at a price, a more complex implementation.

For starters the, the amount of control I would like can only be achieved by ussing Assembly rather than C. Assembly allows me to create smaller and faster code. There is just one problem.
The last time I actually did something with Assembly is over 20 years ago and even then it was just the basics.

## The Theory

The PWM period is 20ms. The max duty cycle however seems to be between _2.1_ and _2.5ms_. That means that for at least 17.5ms the controller would do nothing. So we can break up the 20ms
period in smaller chunks. 2.5ms each would mean we could control


_20 / 2.5 = 8_ servos.


Add Multiplexers to the hardware and we could get up to 64. With my assembly programming skills however I don really think this is feasible... at least not yet.

Lets paint a picture.

In the previous post. I showed this.

![Servo pwm diagram](/images/servo-pwm.png)

The PWM pulse train used to control servos. This image however shows nothing about timing, so here is another one.


![Servo PWM with timing](/images/single-pulse.png)


The image shows the diagram of a single 20ms cycle. All pulses start at the beginning of the cycle. I stated before that the pulse width determines the position of the servo.
Exactly what pulse length correlates to which position seems to differ between servo types. In general though the left extreme position is no less than 0.5ms while the right
extreme position is no more thatn 2.5ms. Please keep in mind that this is just from what I read at various sites on-line.

Anyway, looking at the diagram, one can't help but notice the huge amount of idle time there is between 2.5ms and 20ms. This is where the breaking up comes in to play. Assuming
the max pwm duty cycle is 2.5ms breaking it up in blocks of 2.5 will leave very little time to do anything else. so I decided to break the cycle up into four parts.

![Servo PWM in blocks](/images/quad-pulse.png)

This way we can generate four pulses each cycle, using multiplexers that adds up to 32 servos. That seems like enough to control a hexapod mobile robot.

So lets zoom in on the 5ms each of our cycles will be.
