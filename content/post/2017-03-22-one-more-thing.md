+++
date = "2017-03-22T21:00:09-04:00"
draft = false
title = "One more thing for docker, qtcreator, and debuggin"
tags = ["docker","debugging","qtcreator","privileged"]

comments = false
share = false
menu = "main"
+++

Debugging requires a "privileged" docker container:

~~~~
docker run --privileged
~~~~

With other calls (like [proper X display permission](/post/2017-03-19-docker-x2go/)) and passing volumes
into the container, my run looks like:

~~~~
docker run --privileged -it -e DISPLAY=$DISPLAY -v /data:/data -v /tmp/.X11-unix:/tmp/.X11-unix -v /home/mkim/.Xauthority:/home/mark/.Xauthority --net=host adios-vtk
~~~~