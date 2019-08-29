# wxy0218.github.io

### C programming notes

#### 5.3 Pointers and Arrays
If `pa` is a pointer to an integer
```c
  int *pa;
  pa = &a[O]; //pa contains the address of a[0]
  pa = a;  //can also be written as
```
* `pa+i`: the address of `a[i]`
*  `*(pa+i)`: the contents of `a[i]`
* `a[i]`, `*(a+i)` are identical
* `&a[i]`, `a+i` are identical(address)

A pointer is a variable, so `pa=a` and `pa++` are legal. But an array name is not a variable; constructions like `a=pa` and `a++` are illegal.

An array name parameter is a pointer. When an array name is passed to a function, what is passed is the location of the initial element.
* `char s[]` and `char *s;` are equivalent.
* `£(&a[2])` and `£(a+2)` both pass to the function f the address of the subarray that starts at `a[2]`.
