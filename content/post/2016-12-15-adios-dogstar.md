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
CC=mpicc LIBS="-lpthread" CFLAGS="-fPIC" LDFLAGS="-fPIC" ./configure --prefix=$HOME/local/adios

```

For DS:

```
 CC=mpicc CFLAGS="-fPIC $($HOME/local/adios/bin/adios_config -c )" LDFLAGS="$($HOME/local/adios/bin/adios_config -l) -fPIC" ./configure --prefix=$HOME/local/dogstar --with-adios_dir=$HOME/local/adios/
```
