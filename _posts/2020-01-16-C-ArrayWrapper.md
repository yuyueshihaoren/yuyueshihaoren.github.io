---
layout: post
title:  "C Array Wrapper"
categories: [programming]
id: 1
comment: true
---

In C, one can't write a function and return a local array.
Instead of creating a dynammic allocated array and pass it to the function by pointer or using static array,
let's try to put the array into a struct so that we can deep copy them.

It's easy to verify that struct elemets are deeply copied.

```c
#include <stdio.h>
struct arrwrap {
    int arr[5];
};

int main() {
    struct arrwrap arr_st;
    for (int i = 0; i < 5; i++) {
        arr_st.arr[i] = i;
    }
    puts("arr_st1");
    for (int i = 0; i < 5; i++) {
        printf("    arr[%d] = %d\n", i, arr_st.arr[i]);
    }
    struct arrwrap arr_st2 = arr_st;
    arr_st2.arr[1] = 123;
    puts("arr_st2 (after change)");
    for (int i = 0; i < 5; i++) {
        printf("    arr[%d] = %d\n", i, arr_st2.arr[i]);
    }
    puts("arr_st1");
    for (int i = 0; i < 5; i++) {
        printf("    arr[%d] = %d\n", i, arr_st.arr[i]);
    }
    return 0;
}

```

Output:
```
arr_st1
    arr[0] = 0
    arr[1] = 1
    arr[2] = 2
    arr[3] = 3
    arr[4] = 4
arr_st2 (after change)
    arr[0] = 0
    arr[1] = 123
    arr[2] = 2
    arr[3] = 3
    arr[4] = 4
arr_st1
    arr[0] = 0
    arr[1] = 1
    arr[2] = 2
    arr[3] = 3
    arr[4] = 4
```

Applied to a simple function that returns 10 1s.
```c
#include <stdio.h>
struct arrwrap {
	int arr[10];
};

struct arrwrap ten1s() {
    struct arrwrap ten1s_st;
    for (int i = 0; i < 10; i++) {
        ten1s_st.arr[i] = 1;
    }
    return ten1s_st;
}

int main() {
	struct arrwrap arr_st = ten1s();
    for (int i = 0; i < 10; i++) {
        printf("%d\n", arr_st.arr[i]);
    }
    return 0;
}
```
Output:
```c
1
1
1
1
1
1
1
1
1
1
```

# Sources:
1. <https://www.geeksforgeeks.org/return-local-array-c-function/>
