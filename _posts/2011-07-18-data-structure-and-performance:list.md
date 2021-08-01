---
title: "Data Structures and Performances: Lists"
tags:
  - algorithms
  - performances
  - data_structures
  - java
---

The goal of this post is to see how a contiguous-memory structure (arrays) compare to a pointer-based
one (linked lists).

# Recap

Let me start by recapping the difference between an array-based list (also called dynamic array) and
a linked list.
The first one is based on the array concept, i.e., store elements contiguously in memory, preserving a given order;
the second one uses pointers to keep track of the order of the elements (see
[here](https://en.wikipedia.org/wiki/Array_data_structure#Efficiency_comparison_with_other_data_structures)
for a quick comparison between linked list and dynamic array).

These different ways of implementing a list provide different performances:
roughly speaking, array list requires less resources to read elements, and more resources to write
elements (adding or removing), vice-versa for the linked list.

# Read/Write performances
In this post we are going to validate this assertion by experimentally comparing the performances of
these data structures. We are going to use the Java language, and the ArrayList and LinkedList class.

We start by comparing a simple read operation (get an element from the middle of a list), and a
simple write operation (add an element to the end of the list). The results are as following:

(x: size of list, y: time in ms)

![Cost of getting the element in the middle](/assets/images/2011-07-18/get_median_element.png)

![Cost of adding an element at tehe end of the list](/assets/images/2011-07-18/add_element_in_the_end.png)

The "read" operation (get the median element) is much faster using an array list.
In fact, getting an element from an array requires constant time. On the other hand, we would
expect the linked list to be faster when adding elements. This is actually not true (as shown in the
second graph): we can explain this considering that adding an element at the end of a list is a
simple append operation which requires no shifting of the other elements even if the array list
has to copy itself when making more spaces for more elements. It is also true that this happens few
times. In particular, if the array doubles its capacity every time, it has to do it only log(n)
times. In fact, we start from capacity 2, then 4, then 8...till n.
The linked list has to deal with pointers, which is always an added "burden" (in terms of space
and time)

In order to validate our assumption about linked list (i.e., linked list perform better when
dealing with "write" operation), we can try to recreate a scenario where the array list performs
worse due to its "less flexible" structure. We can do this by planning an experiment where we
add elements in the middle of the list (which requires the array list to shift all the following
elements to the right, while the linked list can simply change a pointer)

(x: size of list, y: time in ms)

![Cost of adding an element in the middle of the list](/assets/images/2011-07-18/add_element_in_the_middle.png)

Again, the linked list performs worse. This is because before inserting an element, we have to find
the median element, and as we've seen, this is not so easy for a linked structure. So, we could try
removing this problem by adding the element to the beginning of the list; this way the shifting
problem for the array list should remain, while the linked list should be able to access the element
(the first one) in constant time

(x: size of list, y: time in ms)

![Cost of adding an element at the beginning of the list](/assets/images/2011-07-18/add_element_at_the_beginning.png)

In fact, now the linked list performs much better.

Summarizing: it is true that a linked list perform better when dealing with "write" operation, but
it is also true that when accessing elements far from the list start, the element access operation
comes with a high cost, because we must follow the chain of pointers. It is important to highlight
that this is not true for the last elements, in fact the linked list implementation is  (usually)
"smart" enough to start the element research from the nearest endpoint; as we can see from
the following graph, the worst cases for linked list element access are in the list middle

(x: element index; y: time in ms)

![Cost of accessing an element](/assets/images/2011-07-18/element_access_cost.png)

We could consider the linked list "not so useful" because they perform almost always worse than an
array list. As a matter of fact, the only scenario where they perform better is when dealing with
elements at the beginning and at the end of the list. Actually, this scenario is very common; in
fact, when working with stack, we are only interested in getting elements from the first position,
while with queue we are only interested in the first and last position. Because of this, and because
of stack and queue importance, the linked lists are valuable data structure.
