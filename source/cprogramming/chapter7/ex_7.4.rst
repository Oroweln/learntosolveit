=======================================
Exercise 7.4 - private version of scanf
=======================================


Question
========

Write a private version of scanf analogous to minprintf from the previous
section.

.. literalinclude:: cprogs/ex_7.4.c
   :language: c
   :tab-width: 4

Explanation
===========

The Headers

`#include <stdarg.h>`

This header provides functionality for functions with variable arguments (variadic functions)
It defines va_list, va_start, va_arg, and va_end macros which are used to handle variable arguments
Essential for implementing functions like scanf/printf that can take varying numbers of arguments


`#include <stdio.h>`

This is the standard input/output header
Provides functions like printf, sscanf, putchar used in the program
Necessary for basic input/output operations

This program implements a functionality similar to scanf, by taking a variable number of args and prints them to output.

`#include <stdlib.h>` for the malloc macro.

The key components are

::

    va_list ap;  // Declares a variable to hold the argument list
    va_start(ap, fmt);  // Initializes ap to point to first unnamed argument
    va_arg(ap, type);   // Returns next argument of specified type
    va_end(ap);         // Cleanup of argument list



Visualize
=========

.. raw:: html

    <iframe width="100%" height="800" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=/*%20minscanf%3A%20minimalistic%20scanf%20function%20*/%0A%23include%20%3Cstdarg.h%3E%0A%23include%20%3Cstdio.h%3E%0A%0Avoid%20minscanf%28char%20*fmt,%20...%29%3B%0A%0Aint%20main%28void%29%20%7B%0A%0A%20%20%20%20int%20i%3B%0A%20%20%20%20minscanf%28%22%25d%22,%20%26i%29%3B%0A%20%20%20%20printf%28%22minscanf%20input%3A%20%25d%5Cn%22,%20i%29%3B%0A%0A%20%20%20%20char%20*a%20%3D%20NULL%3B%0A%20%20%20%20minscanf%28%22%25s%22,%20a%29%3B%0A%20%20%20%20printf%28%22minscanf%20input%3A%20%25s%5Cn%22,%20a%29%3B%0A%0A%20%20%20%20float%20f%3B%0A%20%20%20%20minscanf%28%22%25f%22,%20%26f%29%3B%0A%20%20%20%20printf%28%22minscanf%20input%3A%20%25f%5Cn%22,%20f%29%3B%0A%0A%20%20%20%20int%20o%3B%0A%20%20%20%20minscanf%28%22%25o%22,%20%26o%29%3B%0A%20%20%20%20printf%28%22minscanf%20input%20in%20octal%20%25o,%20in%20decimal%20%25d%5Cn%22,%20o,%20o%29%3B%0A%0A%20%20%20%20int%20x%3B%0A%20%20%20%20minscanf%28%22%25x%22,%20%26x%29%3B%0A%20%20%20%20printf%28%22minscanf%20input%20in%20hex%20%25x,%20in%20decimal%20%25d%5Cn%22,%20x,%20x%29%3B%0A%20%20%20%20return%200%3B%0A%7D%0A%0Avoid%20minscanf%28char%20*fmt,%20...%29%20%7B%0A%20%20%20%20va_list%20ap%3B%20/*%20points%20to%20each%20unnamed%20arg%20in%20turn%20*/%0A%20%20%20%20char%20*p,%20*sval%3B%0A%20%20%20%20int%20*ival%3B%0A%20%20%20%20float%20*dval%3B%0A%0A%20%20%20%20va_start%28ap,%20fmt%29%3B%20/*%20make%20ap%20point%20to%201st%20unnamed%20arg%20*/%0A%0A%20%20%20%20for%20%28p%20%3D%20fmt%3B%20*p%3B%20p%2B%2B%29%20%7B%0A%20%20%20%20%20%20%20%20if%20%28*p%20!%3D%20'%25'%29%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20continue%3B%0A%20%20%20%20%20%20%20%20%7D%0A%0A%20%20%20%20%20%20%20%20switch%20%28*%2B%2Bp%29%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20case%20'd'%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20ival%20%3D%20va_arg%28ap,%20int%20*%29%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20char%20*d%20%3D%20%2244%22%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20sscanf%28d,%20%22%25d%22,%20ival%29%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20break%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20case%20'f'%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20dval%20%3D%20va_arg%28ap,%20float%20*%29%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20char%20*f%20%3D%20%225.33%22%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20sscanf%28f,%20%22%25f%22,%20dval%29%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20break%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20case%20's'%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20sval%20%3D%20va_arg%28ap,%20char%20*%29%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20sscanf%28%22test%20char%22,%20%22%25s%22,%20sval%29%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20break%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20case%20'o'%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20ival%20%3D%20va_arg%28ap,%20int%20*%29%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20char%20*o%20%3D%20%22011%22%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20sscanf%28o,%20%22%25o%22,%20ival%29%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20break%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20case%20'x'%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20ival%20%3D%20va_arg%28ap,%20int%20*%29%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20char%20*x%20%3D%20%221a%22%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20sscanf%28x,%20%22%25x%22,%20ival%29%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20break%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20default%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20putchar%28*p%29%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20break%3B%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%20%20va_end%28ap%29%3B%20/*%20clean%20up%20when%20done%20*/%0A%7D&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=c_gcc9.3.0&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>


