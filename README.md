HPDK

1 Introduction

This is the implementation of the paper "HPDK: A Hybrid PM-DRAM Key-Value Store for High I/O
Throughput". Now we only provide the compiled files, so you can skip step 3.1. we will open the source later.

We implement HPDK based on LevelDB.

2 Compilation and Run (ready for run)

2.1 Configuration of Persistent Memory

To access Persistent Memory, HPDK uses the PMDK library, which provides functions to manage the create, delete, modify pools of PM. To run HPDK, please configure PM first. If you do not have a persistent memory, you can emulate one. Then, you can create a DAX filesystem using the '/dev/pmem0' device and mount the system using the '-o dax' flag.

> su
> mkfs.ext4 -b 4096 -E stride=512 -F /dev/pmem0
> mkdir /mnt/mem
> mount -o dax /dev/pmem0 /mnt/mem/

2.2 Installing Dependency Packages

PMDK install:

> su
> git clone https://github.com/pmem/pmdk
> make
> make install
3 Compilation and Run
3.1 compilation
> su
> mkdir cmake-build
> cd cmake-build
> cmake ..
> make

The generated 'db_bench' is the db_bench micro-benchmark.

3.2 db_bench

There are some options for 'db_bench'.

--value_size=<size>         # value size
--db=<path>                 # HPDK path, default path : /mnt/mem/lcdbtest-%d/dbbench# hpdk
