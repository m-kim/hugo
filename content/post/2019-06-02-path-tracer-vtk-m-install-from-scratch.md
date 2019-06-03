+++
date = "2019-06-02T21:00:09-04:00"
draft = false
title = "Building my VTK-m Path tracer from scratch"
tags = ["vtkm","vtk-m", "path tracer", "path tracing"]

comments = false
share = false
menu = "main"
+++

A quick tutorial to install my path tracer from scratch.

##### Build and Install VTK-m
How to install my VTK-m path tracer from scratch. To avoid some hassles with security on my work desktop, I install vtk-m to a local directory, usually `~/local`. Also, to avoid some of the pain of VTK-m's fast paced development, I've pegged my code v1.3.0.  To get VTK-m v1.3.0 

```console
wget https://gitlab.kitware.com/vtk/vtk-m/repository/v1.3.0/archive.tar.bz2
bunzip2 archive.tar.bz2
tar -xvf archive.tar
```
Now, we must build VTK-m. VTK-m uses CMake for its build system. Do not do in-place builds with CMake. That's why we're creating a `build` directory. Also, I use ninja because from personal experience it does better parallel builds than `make -j`. If you don't have ninja install, then ignore `-GNInja` and it CMake will default to make.

```console
cd vtk-m-v1.3.0-a8da749e71583f14bd8ed53609cb135878fa6578/
mkdir build
cd build
cmake ../ -GNinja -DCMAKE_INSTALL_PREFIX=~/local/vtk-m -DVTKm_ENABLE_TESTING=OFF
ninja install
```

A quick breakdown: `-DCMAKE_INSTALL_PREFIX` informs CMake where VTK-m should be installed. `VTKm_ENABLE_TESTING`is turned off because testing requires over 1000 different files to be compiled, which takes fooooooeeeeevvvverrrrr. Instead, we just compile the libraries we need, `libvtkm_rendering` and `libvtkm_cont` and call it a day.



##### Retrieve and Build Pathtracer Code
Now that VTK-m is installed, we'll need to get the path tracer code from github. From the command line:

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
cmake ../ -DVTKm_DIR=~/local/vtk-m/lib/cmake/vtkm-1.3/
make
```
Note, if NVidia CUDA was installed (and VTK-m was compiled to support CUDA), an environmental variable could be set to inform CMake to compile the pathtracer with CUDA enabled. That would be:

```
CUDACXX=/usr/local/cuda/bin/nvcc cmake ../../ -DVTKm_DIR=~/local/vtk-m/lib/cmake/vtkm-1.3/
```

##### Running the path tracer
CMake will generate a makefile to build the CornellBox executable. When it finishes, there will be two executables: CornellBox (and CornellBox_CUDA if CUDA is installed and configured with VTK-m). CornellBox/CornellBox_CUDA have command line inteface (CLI) inputs: `-x`, `-y`, `-raydepth`, `-samplecount`, and `-hemisphere`. 

```console
./CornellBox -x 512 -y 512 -samplecount 1024 -raydepth 64 -hemisphere
```

`-x` and `-y` set the width and the height of the output image, respectively. `-raydepth` is the number of times a ray will recurse before it will stop if it doesn't hit a light source. `-samplecount` is the number of rays we want to send. Finally, `-hemisphere` will generate a hemisphere worth of images around a fixed point.
