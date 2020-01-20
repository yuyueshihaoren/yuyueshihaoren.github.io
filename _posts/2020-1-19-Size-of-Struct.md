---
layout: post
title:  "Size of a Struct"
date:   2020-01-19
categories: [programming]
id: 5
comment: false
---

# On a 64-bit machine
On a 64-bit machine, the word length is 64 bits, 8 bytes.
Thus the pointer size is 8 bytes.

## 1. Size of a struct containing a single variable
```c
struct {
    int a;
}
```
`4`  
Size is 4 bytes, because int type is 32-bit.

```c
struct {
    int *a;
}
```
`8`  
Size is 8 bytes, as expected on a 64-bit machine / OS.
```c
struct {
    char a;
}
```
`1`  

```c
struct {
    int a[4];
}
```
`16`  
4 * 4 = 16.


## 1. Size of a struct containing two variables
First, intuitive ones.
```c
struct {
    int a;
    int b;
}
```
`8`  
Size is 8 bytes, 4 + 4 = 8.

Then, counter-intuitive ones.
```c
struct {
    int a;
    char b;
}
```
`8`  
Size is 8 bytes. 8 > 4 + 1. This is due to alignment.
The size of a struct will be the multiple of size of the biggest main type.
Here `int` has the bigger size, 4 bytes. 
The smallest multiple of 4 that is greater or equal to 5 is  4 * 2 = 8 .
So, the struct size is 8.

```c
struct {
    short a;
    char b[15];
    int *c;
}
```
`32`  
- `short a` : 2
- `char b[7]` : 15 * 1 = 15
- `int *t` : 8
- total: 2 + 15 + 8 = 25

Although `char b[15]` is biggest, of size 15, its main type size is 1.
So, the biggest base type size is the size of the pointer type, 8.
Thus, the size of the struct is 4 * 8 = 32. (3 * 8 < 25 < 4 * 85).

Finally, a bizarre but logical one.
```c
struct st_a{
    short a;
    char b[15];
    int *c;
};
struct {
    struct st_a a[8];
}
```
`256`  
The first struct is of size 32 as we analyzed.
The second of is just an array of the first struct.
So, it's size is 32 * 8 = 256.

If the word length of a machine is 32-bit long, the only difference is the pointer size is now 4 bytes instead of 8 bytes.