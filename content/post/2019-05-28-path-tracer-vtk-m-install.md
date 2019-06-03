+++
date = "2019-05-28T21:00:09-04:00"
draft = false
title = "Building my VTK-m Path tracer using conda (updated 2019-06-02"
tags = ["vtkm","vtk-m", "path tracer", "path tracing", "conda"]

comments = false
share = false
menu = "main"
+++

Update: With Ubuntu 16.04, the g++ from quantstack needs to be installed.

A quick tutorial to install my path tracer using conda.

##### Create a conda Environment
How to install my VTK-m path tracer using conda. First, install conda. Conda is a Python package manager that can also manager C/C++ "packages." It eases (some) of the pain when it comes to deploying software libraries, such as VTK-m.  Once conda is installed let's create an environment to play around in. From the command line:


```console
conda create -n pathtracer
```

This will create a environment called `pathtracer`. To activate the `pathtracer` environment, type in the command line:

```console
conda activate pathtracer
```

and to leave any environment type:

```console
conda deactivate
```

Now that an environment is setup, we'll need to install VTK-m, particularly the CUDA version. Why CUDA? The path tracer is slow, even using CUDA. So, we'll need as much horsepower as possible to generate good images. To install the cuda version of VTK-m, from a command line:

##### Install VTK-m through conda
```console
conda install vtk-m-cuda -c m-kim
conda install gcc-7 -c quantstack -c conda-forge
```

`vtk-m-cuda` is the package name: it is downloaded from anaconda.org and installed in the current environment. The `-c` is the channel, which in conda parlance is the user/group who uploaded it to anaconda.org. In this case, the channel is my personal channel under the user `m-kim.` 

##### Retrieve and Build Pathtracer Code
Now that a CUDA version of VTk-m is installed, we'll need to get the path tracer code from github. From the command line:

```console
git clone git@github.com:m-kim/raytracingtherestofyourlife.git
```

Now we have the code, but we're not on the correct branch, so we need to switch to the branch `vtkm-working.`

```console
cd raytracingtherestofyourlife
git checkout vtkm-working
```

Great, now we're on the correct branch of the source code. Let's compile it. To compile the code, we'll need a version of CMake that's greater than 3.8. 

```
mkdir build
cd build
CUDACXX=/usr/local/cuda/bin/nvcc cmake ../
make
```

##### Running the path tracer
CMake will generate a makefile to build the CornellBox executable. When it finishes, there will be two executables: CornellBox and CornellBox_CUDA. CornellBox/CornellBox_CUDA have command line inteface (CLI) inputs: `-x`, `-y`, `-raydepth`, `-samplecount`, and `-hemisphere`. 

```console
./CornellBox -x 512 -y 512 -samplecount 1024 -raydepth 64 -hemisphere
```

`-x` and `-y` set the width and the height of the output image, respectively. `-raydepth` is the number of times a ray will recurse before it will stop if it doesn't hit a light source. `-samplecount` is the number of rays we want to send. Finally, `-hemisphere` will generate a hemisphere worth of images around a fixed point.

##### TLDR;

```console
conda create -n pathtracer
conda activate pathtracer
conda install vtk-m-cuda -c m-kim
conda install gcc-7 -c quantstack -c conda-forge
git clone git@github.com:m-kim/raytracingtherestofyourlife.git
cd raytracingtherestofyourlife
git checkout vtkm-working
mkdir build
cd build
CUDACXX=/usr/local/cuda/bin/nvcc cmake ../../ 
make
./CornellBox -x 512 -y 512 -samplecount 1024 -raydepth 64 -hemisphere
```