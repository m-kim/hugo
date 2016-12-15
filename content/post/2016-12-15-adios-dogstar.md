+++
date = "2016-12-15T15:00:09-04:00"
draft = false
title = "zfp and ADIOS"

comments = false
share = false
menu = "main"
+++

Compile options for ADIOS:

```
CC=mpicc LIBS="-lpthread" CFLAGS="-fPIC" LDFLAGS="-fPIC" ./configure --prefix=/home/mark/local/adios

```

For DS:

```
 CC=mpicc CFLAGS="-fPIC $(/home/mark/local/adios/bin/adios_config -c )" LDFLAGS="$(/home/mark/local/adios/bin/adios_config -l) -fPIC" ./configure --prefix=/home/mark/local/ --with-adios_dir=/home/mark/local/adios/
```
