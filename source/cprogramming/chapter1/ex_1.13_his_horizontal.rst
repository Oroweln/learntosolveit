====================================
Exercise 1.13 - Horizontal Histogram
====================================

Question
--------


Write a program to print a histogram of the lengths of words in its input. It is
easy to draw the histogram with the bars horizontal.

Solution
--------

.. literalinclude:: cprogs/ex_1.13_his_horizontal.c
   :language: c

Explanation
===========

We desire the histogram like the following.

If the input is **I love C programming**

The output should be.::

    *
    ****
    *
    ***********

The way it is accomplished in the above program, read each character using
getchar, if it is special character like a space, tab or newline,  go to next
line by printing `\n` otherwise print a `*` character.
