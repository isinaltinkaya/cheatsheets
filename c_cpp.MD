# C/C++ Programming



### Resources

[Translate C Gibberish to English](https://cdecl.org/)

___

### - Using `#include <cmath>` vs `#include <math.h>`

`cmath` defines symbols in the std namespace, and may also define symbols in the global namespace.
`math.h` defines symbols in the global namespace, and may also define symbols in the std namespace. i


If you use an unqualified symbol, it may compile with one compiler but not with another. 


Therefore better to use `math.h`.

This can also be generalized to such header pairs.

Credit:https://stackoverflow.com/a/10694346/7870777

___
