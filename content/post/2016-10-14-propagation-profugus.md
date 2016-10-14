+++
date = "2016-10-14T16:50:09-04:00"
draft = false
title = "ray propagation"
tags = ["pin-cell","pin","cell"]

comments = false
share = false
menu = "main"
+++

Looking at Profugus more, I don't know how they propagate the ray through.
The example is ```MC/geometry/test/testRTK_Array.cc```. In particular, it calculates 
the distance to the next boundary, moves the particle to the next boundary and 
crosses over the surface. 

Well, it's a bit "duh." In each direction, the slope is known so the other side
of the box can be computed. Then, some updates happen in the background to change
the current region/face/segment.