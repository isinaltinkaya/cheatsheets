# makefile

x is evaluated immediately even if it's not used.

`x := $(shell sleep 42)`
`:=` -> run only once

`x = $(shell sleep 42)`
`=` -> run each time it's called
