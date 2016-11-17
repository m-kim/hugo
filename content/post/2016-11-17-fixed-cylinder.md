+++
date = "2016-11-17T15:00:09-04:00"
draft = false
title = "Fixed cylinder"

comments = false
share = false
menu = "main"
+++
Fixed the problem: 

![VTK-m CSG ray tracing cylinder fixed](/images/20161117/reg3D_fixed.png)

Checking absolute value of a floating point:
~~~~ 
if (abs(a) < 1.0e-6) {
~~~~

should be...

~~~~ 
if (fabs(a) < 1.0e-6) {
~~~~


![VTK-m CSG ray tracing](/images/20161117/reg3D.png)
