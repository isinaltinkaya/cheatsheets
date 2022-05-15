# makefile



## - Simple assignment `:=`

`x := $(shell sleep 42)`
`:=` -> run only once


## - Recursive assignment `=`

x is evaluated immediately even if it's not used.

evaluate every time x is encountered in the code

`x = $(shell sleep 42)`
`=` -> run each time it's called


## - Conditional assignment `?=`

assign a value to x only if it does not have a value

## - Appending `+=`



### - using phony target

`.PHONY: something`

declare phony targets; make will not check them as actual filenames. it will even if such files exist.

---


### 

### - `CC`
Program for compiling C programs; default `cc`.

### - `CXX`
Program for compiling C++ programs; default `g++`.

### - `CPP`
Program for running the C preprocessor, with results to standard output; default `$(CC) -E`.


### - `CFLAGS` =  Flags to give to C compiler.
CFLAGS is only passed when compiling and linking C.

### - `CXXFLAGS` = Flags to give to the C++ compiler.
CXXFLAGS is only passed when compiling and linking C++.

### - `CPPFLAGS` = Flags to give to the C preprocessor
and programs that use it (the C and Fortran compilers).
CPPFLAGS are for the C [P]re[P]rocessor


https://www.gnu.org/software/make/manual/html_node/Implicit-Variables.html
