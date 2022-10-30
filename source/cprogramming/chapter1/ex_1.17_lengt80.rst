=========================================================
Exercise 1.17 - Print lines that are longer than 80 chars
=========================================================

Question
--------


Write a program to print all input lines that are longer than 80 characters.

Solution
--------

.. literalinclude:: cprogs/ex_1.17_lengt80.c
   :language: c

Explanation
===========

A string in C is a character array which ends in ``\0``. getline is a function in
our program, which reads one character at a time using getchar and stores it in
a character array called s[] and it returns the length of the array.

When an array is sent as argument to the function, like ``line[MAXLINE]`` is sent
to ``getline`` function, the value is passed by reference, which means that any
changes the function makes will be available to the main program.

``getline`` returns the length of the line and in our main program, if the length
is greater than 80 characters we print it.
