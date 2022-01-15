# General Overview of the System

## History

* early application for UNIX file system was to simplify development of video
  game side project
* UNIX is pun on Multics project
* Thompson accidentally made B while making Fortran compiler for new text
  processing project
* B was interpreted (slow for the time), so Ritchie developed it into C
* rewrote early UNIX into C, unheard of step at time, apparently
* philosophy of simplicity and consistency

## System Structure

* encourages combination of existing programs to accomplish a task

## User Perspective

* devices are treated the same as files; after all, they're just byte streams,
  too
* the bytes of a directory can be directly copied into a regular file, but that
  regular file is not a directory until the "mknod" system call is run on it
* "...philosophy of the UNIX system is to provide operating system primitives
  that enable users to write small, modular programs that can be used as
  building blocks to build more complex programs." (p. 13)
* some building block primatives:
  - redirect I/O
  - pipe

## Operating System Services

* OS offers services needed by user-level programs
* omits anything that can be implemented at user level

## Assumptions about Hardware

* user mode vs. kernel mode
  - user mode processes can access own instructions and data, but nothing in
    kernel mode; kernel mode processes can touch both
  - kernel mode processes can talk directly to hardware, while user mode
    processes cannot
* the kernel distinguishes between processes
* the hardware distinguishes between modes of execution (user/kernel)
* kernel is NOT own process running in parallel to user processes, it is PART of
  each user process
* "the kernel" refers to the kernel mode piece of a particular process, rather
  than a separate process altogether
* exceptions occur DURING instruction execution (internal to process)
* interruptions occur BETWEEN instruction execution (external to process)
