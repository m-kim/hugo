+++
date = "2018-07-18T21:00:09-04:00"
draft = false
title = "VTK-m and the interactive C++ interpreter Cling"
tags = ["vtkm","vtk-m","cling","C++","jupyter","jupyter notebook"]

comments = false
share = false
menu = "main"
+++

I spend my time developing for [VTK-m](m.vtk.org/). VTk-m is a toolkit for manycore/multicore scientific visualization in HPC. About a year ago I came across [Cling](https://root.cern.ch/cling), an interactive C++ compiler from the fine scientists at [CERN.](https://home.cern/) I put it in the back of my mind as a "That's really cool!" thing that I should experiment with. Cling comes with an interactive command line similar to iPython. And, there is also a [Jupyter Notebook](https://jupyter.org/) plug-in for Cling, [xeus-cling](https://github.com/QuantStack/xeus-cling) from [QuantStack](http://quantstack.net/). QuantStack is also the developers of [xeus](http://quantstack.net/xeus) a C++ implementation of the Jupyter kernel. 

Recently, I found some time to see if Cling and VTK-m would play well together. And, they do! Which means you can play with VTK-m directly from [mybinder.org.](https://mybinder.org/) in Jupyter Notebook. My [example at mybinder](https://mybinder.org/v2/gh/m-kim/vtkm-jupyter/master?filepath=notebooks) is generated from this [github repo](https://github.com/m-kim/vtkm-jupyter). The notebook "VTK-m using Cling and Xeus for Jupyter Notebook.ipynb" is adapted from a unit test [rt_reg3d](https://gitlab.kitware.com/vtk/vtk-m/blob/master/vtkm/rendering/testing/UnitTestMapperRayTracer.cxx) within VTK-m. In particular, I adapted [vtkm::cont::rendering::RenderTest::Render](https://gitlab.kitware.com/vtk/vtk-m/blob/master/vtkm/rendering/testing/RenderTest.h) to work with Jupyter Notebook. Since rendering in VTK-m produces pnm files, I redirect that framebuffer to a [nlohmann/json](https://nlohmann.github.io/json/) to display a png in Jupyter Notebook. The notebook "VTK-m Cling Xeus Jupyter data parallel algorithms.ipynb" tests some of the parallel primitives functionality within VTK-m. Finally, "Xeus-cling and javascript and d3" is a notebook to try to get d3 and xeus-cling to play together. 

I think this is a nice demonstration of how powerful modern C++ is in terms of usefulness through a Jupyter Notebook interface. Kudos to the QuantStack folks as well for building the xeus-cling interface.