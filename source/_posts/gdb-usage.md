---
title: 'gdb usage '
date: 2017-04-13 18:24:55
tags: tools
---

  introduce how to use gdb for debugging

<!-- more -->

## prepare
  you have to use '-g' when compiling your project for gdb, '-g' means that the executable file will import source code information so that gdb can find source files.

## commands

### run

``` bash
(gdb) set args [your_args]
```
  set args for your program, the args will be delivered to 'main' function

``` bash
(gdb) start
```
  start executing program and pause at the first line in 'main' function to wait for commands
  
``` bash
(gdb) run
```
  just run program util a break point is triggered

### break point

``` bash
(gdb) break X
```
  add a break point at No.x line of current file

``` bash
(gdb) break func
```
  add a break point at the function named 'func' of current file

``` bash
(gdb) break dir/file.c:X
```
  add a break point at NO.X line of 'dir/file.c'

``` bash
(gdb) break dir/file.c:func
```
  add a break point at the function named 'func' of 'dir/file.c'


### control

``` bash
(gdb) next
```
  execute the next line, and if it is a function invokation, gdb just executes, not enters it

``` bash
(gdb) step
```
  execute the next line, and if it is a function invokation, gdb will enter the function

``` bash
(gdb) finish
```
  run util current function returns
```

``` bash
(gdb) return
```
  force to exit current function

### information

``` bash
(gdb) list
```
  list 10 lines source code

``` bash
(gdb) list X
```
  list X lines source code

``` bash
(gdb) list func
```
  list source code of the function named 'func'

``` bash
(gdb) print v 
```
  print the value of the variable named 'v'

``` bash
(gdb) backtrace
```
  show all function invokations with args

```
(gdb) frame X
```
  show NO.X stack frame

``` bash
(gdb) info
```
  show current stack frame
  
### quit

``` bash
(gdb) quit
```
  exit gdb
