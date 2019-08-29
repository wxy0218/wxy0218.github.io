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
```c
\* strlen: return length of string s *\
int strlen(char *s)
{
  int n;
  for (n = 0; *s 1= '\0'; s++) 
    n++;
  return n;
}
```

#### 5.4 Address Arithmetic
Example: When `alloc` is asked for n characters, it checks to see if there is enough room left in `allocbuf`. If so, `alloc` returns the current value of `allocp` (i.e., the beginning of the free block), then increments it by n to point to the next free area. `afree(p)` merely sets `allocp` to p if p is inside `allocbuf`.
```c
#define ALLOCSIZE 10000 /* size of available space */ 

static char allocbuf[ALLOCSIZE]; /* storage for alloc */
static char *allocp = allocbuf; /* next free position */

char *alloc(int n) /* return pointer to n characters */ 
{
  if (allocbuf + ALLOCSIZE - allocp >= n) { /* it fits */ 
      allocp += n;
      return allocp - n; /* old p */ 
  } else /* not enough room */
      return 0;
}

void afree(char *p) /* free storage pointed to by p */
{
  if (p >= allocbuf && p < allocbuf + ALLOCSIZE) allocp = p;
}
```
* C guarantees that zero is never a valid address for data, so a return value of zero can be used to signal an abnormal event, in this case, no space. Pointers and integers are not interchangeable. Zero is the sole exception.
* Pointers may be compared under certain circumstances. If p and q point to members of the same array, then works properly.
This fact can be used to write another version of `strlen`:
```c
\* strlen: return length of string s *\ 
int strlen(char *s)
{
  char *p = s;
  while (*p 1= '\0') 
    p++;
  return p - s; //Be careful, could be too large to store in an int
}
```
