# Quick Sort

&#160;&#160;&#160;&#160;&#160;**Quicksort** (sometimes called **partition-exchange sort**) is an **O(N log N)** [efficient](https://en.wikipedia.org/wiki/Algorithmic_efficiency) [sorting algorithm](https://en.wikipedia.org/wiki/Sorting_algorithm), serving as a systematic method for placing the elements of an [array](https://en.wikipedia.org/wiki/Array_data_structure) in order. Developed by British computer scientist [Tony Hoare](https://en.wikipedia.org/wiki/Tony_Hoare) in 1959 and published in 1961, it is still a commonly used algorithm for sorting. When implemented well, it can be about two or three times faster than its main competitors, [merge sort](https://en.wikipedia.org/wiki/Merge_sort) and [heapsort](https://en.wikipedia.org/wiki/Heapsort).

&#160;&#160;&#160;&#160;&#160;The above paragraph is from Wikipedia, but I think it is difficult for many people to understand. That is a very official and rigid introduction. So let me simplify it!

----------

&#160;&#160;&#160;&#160;&#160;**Bubble sorting** solves the problem of **barrel sorting** wasting space, but it sacrifices a lot in the execution efficiency of the algorithm, and its time complexity reaches **O(N^2)**. If our computer can run 1 billion times per second, then sort 100 million numbers, bucket sorting only takes 0.1 seconds, and bubble sorting takes 10 million seconds, reaching 115 days, is it very scary. The sorting algorithm that neither wastes space nor can be faster is "quick sorting"!

----------

&#160;&#160;&#160;&#160;&#160;Suppose we now sort the 10 numbers "6 1 2 7 9 3 4 5 10 8". First, figure out a number in this sequence as a **reference number** (a number used for reference). For convenience, let the first number 6 to be used as the reference number. Next, you need to put all the numbers in this sequence larger than the reference number to the right of 6, and the number smaller than the reference number to the left of 6, similar to the following arrangement.

```
3  1  2  5  4  6  9  7  10  8
```

&#160;&#160;&#160;&#160;&#160;In the initial state, the number 6 is at the first bit of the sequence. Our goal is to move 6 to a position in the middle of the sequence, assuming this position is k. Now you need to find this k, with the k th position as the demarcation point, the number on the left is less than or equal to 6, and the number on the right is greater than or equal to 6.

&#160;&#160;&#160;&#160;&#160;Recalling the bubble sorting, how to make each number homing steps by step through "swap". At this point, the "exchange" method can also be used to achieve the goal.

&#160;&#160;&#160;&#160;&#160;The method is actually very simple: "Probe" is started from both ends of the initial sequence "6 1 2 7 9 3 4 5 10 8". First find a number less than 6 from right to left, then find a number greater than 6 from left to right, and then exchange them. Here we can use two variables i and j, pointing to the leftmost and rightmost of the sequence. We have a nice name for these two variables, "Sentinel i" and "Sentinel j". At the beginning, let the sentinel i point to the far left of the sequence (ie i=1), pointing to the number 6. Let the sentinel j point to the far right of the sequence (ie j=10), pointing to the number 8.

<center>![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Quick%20Sort/Quick%20Sort%20p1.png)</center>


