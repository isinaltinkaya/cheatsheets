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
