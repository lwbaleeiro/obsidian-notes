### What is a pointer?

First of all, to understand pointers we need to learn who memory works.

**Memory**
Memories usually have two features, `adress` and `value`.
*Adress* is de location of the memory, meaning where that memory lives.
*Value* is the data stored at that location, meaning what memories lives there.

Ex:

| ADRESS | VALUE  | DATA                     |
| ------ | ------ | ------------------------ |
| 0X1000 | 0X4    | int x = 4;               |
| 0X1004 | 0X1000 | int \*pX = &xi (pointer) |
| 0X1008 |        |                          |
| 0X100C |        |                          |
| 0X1010 |        |                          |
| 0X1014 |        |                          |
### Pointer Syntax

using C.

Ex:
```c
int x = 4;
int * pX = &x;
```

**int**: variable of type Integer.
\*: It modifies the type, so our variable now is a pointer.
**pX**: variable name.
\= : Is set too.
&: The address of;

### Why use pointers?
