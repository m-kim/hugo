+++
date = "2017-03-27T21:00:09-04:00"
draft = false
title = "docker and opengl"
tags = ["docker","debugging","qtcreator","privileged"]

comments = false
share = false
menu = "main"
+++

[Previously](/post/2017-03-19-docker-x2go/) I setup X. Those settings, combined with installing
Nvidia drivers (sans kernel driver) to the docker image means accelerated OpenGL. Cool. It also means launching qtcreator no longer needs "-noload Welcome." Excellent. Everything worked for a while then:


~~~~
:~$ qtcreator
Starting process:  "/opt/cmake/bin/cmake" "--help" 
Segmentation fault (core dumped)
~~~~

That was for launching QtCreator.

I discovered that the system updated the nvidia driver. 
Not cool, Ubuntu, not cool. The driver in the image must match the host, so OpenGL broke which 
lead to that error. O.o Okay.

