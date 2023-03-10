# Who Gets the Cake

### Due 01/30 at 11:59pm

Learning Goals 
==============

This assignment asks you to keep track of information using an array.

You need to learn how to write Makefile. This is the last assignment
giving you the complete Makefile. Starting from the next assignment,
you need to write your own Makefile.

Rules
=====

Imagine that there is a piece of cake and several people want it.
They decide who can have it by playing a game: They form a circle and
choose an integer k greater than one. They count 1, 2, 3, ..., k. The
k-th person is eliminated.  They restart from 1 and count to k again
to eliminate the next person whose number is k.  They keep counting
until only one person is left. This person gets the cake.

Please notice that there are different definitions of this
problem. Your solution **must follow the definition here**.  More
precisely, this is how the method works: There are n people,
represented by are n elements in an array. The elements are counted as
1, 2, 3, ... When the value k is counted, this element is removed in
future counting and the next element starts as 1 again. When reaching
the end of the array, the counting *wrap around* to the beginning of
the array (skipping the elements that have already been eliminated).
Please notice that in C arrays, indexes *always* start at zero but in
this problem counting starts at one. Both n and k have to be greater
than one.  It is possible that k is greater than n.

The following is an example when the array has 6 (n is 6) elements and
k is 3.  The eliminated elements in each round are mared by `X`.  The
elements eliminated earlier are marked by `Y`.


array index | 0 | 1 | 2 | 3 | 4 | 5 
------------|---|---|---|---|---|---
count       | 1 | 2 | X | 1 | 2 | X 

Go to the beginning. Since index 2 has already been eliminated, it is
skipped.  Index 3 is eliminated this time.


array index | 0 | 1 | 2 | 3 | 4 | 5 
------------|---|---|---|---|---|---
count       | 1 | 2 | Y | X | 1 | Y 

Index 5 has already been eliminated and it is skipped.  Index 1 is eliminated this time.

array index | 0 | 1 | 2 | 3 | 4 | 5 
------------|---|---|---|---|---|---
count       | 2 | X | Y | Y | 1 | Y

Index 4 is eliminated this  time.

array index | 0 | 1 | 2 | 3 | 4 | 5
------------|---|---|---|---|---|---
count       | 2 | Y | Y | Y | X | Y

The element of index 0 is left.

This is another example. The array has 6 elements and k is 4.

array index | 0 | 1 | 2 | 3 | 4 | 5 
------------|---|---|---|---|---|---
count       | 1 | 2 | 3 | X | 1 | 2 

array index | 0 | 1 | 2 | 3 | 4 | 5 
------------|---|---|---|---|---|---
count       | 3 | X | 1 | Y | 2 | 3 

array index | 0 | 1 | 2 | 3 | 4 | 5 
------------|---|---|---|---|---|---
count       | X | Y | 1 | Y | 2 | 3

array index | 0 | 1 | 2 | 3 | 4 | 5 
------------|---|---|---|---|---|---
count       | Y | Y | X | Y | 1 | 2

array index | 0 | 1 | 2 | 3 | 4 | 5 
------------|---|---|---|---|---|---
count       | Y | Y | Y | Y | 3 | X

The element of index 4 is left.

This is the third example. The array has 25 elements and k is 7.

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | 1 | 2 | 3 | 4 | 5 | 6 | X | 1 | 2 | 3 | 4  | 5  | 6  | X  |  1 | 2  |  3 |  4 | 5  | 6  | X  |  1 | 2  |  3 |  4 


array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | 5 | 6 | X | 1 | 2 | 3 | Y | 4 | 5 | 6 | X  |  1 | 2  | Y  |  3 | 4  | 5  | 6  |  X |  1 | Y  |  2 | 3  | 4  |  5

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | 6 | X | Y | 1 | 2 | 3 | Y | 4 | 5 | 6 | Y  | X  | 1  | Y  | 2  | 3  | 4  | 5  |  Y |  6 | Y  |  X | 1  | 2  |  3

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | 4 | Y | Y | 5 | 6 | X | Y | 1 | 2 | 3 | Y  | Y  | 4  | Y  | 5  | 6  | X  | 1  | Y  |  2 | Y  |  Y | 3  | 4  |  5

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | 6 | Y | Y | X | 1 | Y | Y | 2 | 3 | 4 | Y  | Y  | 5  | Y  | 6  | X  | Y  | 1  | Y  |  2 | Y  |  Y | 3  | 4  |  5

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | 6 | Y | Y | Y | X | Y | Y | 1 | 2 | 3 | Y  | Y  | 4  | Y  | 5  | Y  | Y  | 6  | Y  | X  | Y  |  Y | 1  | 2  |  3

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | 4 | Y | Y | Y | Y | Y | Y | 5 | 6 | X | Y  | Y  | 1  | Y  | 2  | Y  | Y  | 3  | Y  | Y  | Y  |  Y | 4  | 5  |  6

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | X | Y | Y | Y | Y | Y | Y | 1 | 2 | Y | Y  | Y  | 3  | Y  | 4  | Y  | Y  | 5  | Y  | Y  | Y  |  Y | 6  | X  |  1

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | Y | Y | Y | Y | Y | Y | Y | 2 | 3 | Y | Y  | Y  | 4  | Y  | 5  | Y  | Y  | 6  | Y  | Y  | Y  |  Y | X  | Y  |  1

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | Y | Y | Y | Y | Y | Y | Y | 2 | 3 | Y | Y  | Y  | 4  | Y  | 5  | Y  | Y  | 6  | Y  | Y  | Y  |  Y | Y  | Y  |  X

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | Y | Y | Y | Y | Y | Y | Y | 1 | 2 | Y | Y  | Y  | 3  | Y  | 4  | Y  | Y  | 5  | Y  | Y  | Y  |  Y | Y  | Y  |  Y

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | Y | Y | Y | Y | Y | Y | Y | 6 | X | Y | Y  | Y  | 1  | Y  | 2  | Y  | Y  | 3  | Y  | Y  | Y  |  Y | Y  | Y  |  Y

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | Y | Y | Y | Y | Y | Y | Y | 4 | Y | Y | Y  | Y  | 5  | Y  | 6  | Y  | Y  | X  | Y  | Y  | Y  |  Y | Y  | Y  |  Y

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | Y | Y | Y | Y | Y | Y | Y | 1 | Y | Y | Y  | Y  | 2  | Y  | 3  | Y  | Y  | Y  | Y  | Y  | Y  |  Y | Y  | Y  |  Y

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | Y | Y | Y | Y | Y | Y | Y | 4 | Y | Y | Y  | Y  | 5  | Y  | 6  | Y  | Y  | Y  | Y  | Y  | Y  |  Y | Y  | Y  |  Y

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | Y | Y | Y | Y | Y | Y | Y | X | Y | Y | Y  | Y  | 1  | Y  | 2  | Y  | Y  | Y  | Y  | Y  | Y  |  Y | Y  | Y  |  Y

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y  | Y  | 3  | Y  | 4  | Y  | Y  | Y  | Y  | Y  | Y  |  Y | Y  | Y  |  Y

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y  | Y  | 5  | Y  | 6  | Y  | Y  | Y  | Y  | Y  | Y  |  Y | Y  | Y  |  Y

array index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 
------------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----
count       | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y  | Y  | X  | Y  | 6  | Y  | Y  | Y  | Y  | Y  | Y  |  Y | Y  | Y  |  Y

The element of index 14 is left.

The table uses `X` and `Y` for clarity.  Your program should use only `X`.

What Do You Need to Do
======================

Write the `eliminate` function and print the index of the eliminated elements.

In the first example, the output is
```
2
5
3
1
4
0
```

In the second example, the output is

```
3
1
0
2
5
4
```

In the third example, the output is

```
6
13
20
2
10
18
1
11
21
5
16
3
15
4
19
9
0
23
22
24
8
17
7
12
14
```

The function is called `eliminate`, not `select` because `select` is a
C function for communication. If you want to know the definition of
the `select` function, search `Linux manual select`.


Submission
==========

As you develop your code, do not forget to use version control. As you solve parts of the problem, use `git add` and `git commit` to preserve the latest version of the code. Periodically use `git push` to sync your code with your GitHub repository.

When you are ready to submit your code for grading, you need to *tag* the version you want us to grade. A tag is a way of assigning a name to a particular version of code. We look for the tag `final_ver` to decide what to grade.

1. Tag your local code: `> git tag final_ver`
2. Push the tag to GitHub: `> git push origin final_ver`

If you later decide you want to update the version you submit, you can tag a different version:

1. Update the tag: `> git tag final_ver -f`
2. Push the tag to GitHub: `git push origin final_ver -f`

We will grade whichever version has the `final_ver` tag at the due date.

Additional Reading
==================

A mathematical question is to determine which element is left
*without* counting 1, 2, ...  If you are interested in this topic,
please read the book Concrete Mathematics by Ronald L. Graham, Donald
E. Knuth, and Oren Patashnik.

Is this a real problem? Is there any real application? Yes. In
distributed systems (such as the Internet), sometimes different
machines need to agree on something. For example, a group of machines
want to find one representative for external communication. It is
better to take turns as the representative. The process of finding a
representative can be achieved in methods similar to this one.


History
=======

This problem is inspired by the "Josephus problem".  History (based on
Wikipedia): Flavius Josephus and 40 soldiers were trapped in a cave by
Roman soldiers. They chose suicide over capture, and decided the order
is determined by the following method: they form a circle and set an
integer k greater than one.  Then, the group starts with 1, 2, ... The
person that counts k is eliminated.  The process continues until all
are eliminated.  The question is where Josephus should stand at the
beginning so that he is the last remaining person.  

