---
layout: post
title: Starting up again... kind of
future: true
---

As you may have noticed. It has been a while since my last post. I have thought about starting up again many times sine then. Last week I actually did it.

When I stopped I was still in the process of learning more assembly. Though I understand the concept of setting values in registers, more advanced concepts still elude me.

One of those concepts is variables.

in C I would just provide a type, a name, and default value like so.

```c
int pin3 = 3;
```

In Assembly this is very different. I read about the various sections available and I came across the `.bss` and `.data` sections.

Starting off with `.bss` which is defined as an unitialized section. Usually for uninitialized data. It is declared as follows.

```
.bss name [,size in bytes]
```

The idea now is that servo settings can be configured and stored to persistent flash memory in the `.data` segment.

From there the initial settings can be loaded into the uninitialized `.bss` section for variable use.

For each servo I plan to define a `.bss` section as follows.

```
.bss	servo1,3
```

In it I create a label `servo1` and reserve 3 bytes of memory for it. Why 3, because initially I thought it could hold the desired position, the current position and the number of steps left to get to the desired position. If I ever get this working it will probably need some more bytes of data. The idea of steps cam from another blog, see [l'Hexapod](http://www.lhexapod.com/blog/2009/09/new-servo-controller-commands.html). It is an older and seemingly inactive blog, but it holds a lot of information and insights of a similar project.

Next up... learning to work with the variables. I still need to figure out easy ways to address the other bytes in the defined space. The label seems to only point to the first one.