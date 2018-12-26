# Bubble Sort

&#160;&#160;&#160;&#160;&#160;**Bubble sort**, sometimes referred to as **sinking sort**, is a simple [sorting algorithm](https://en.wikipedia.org/wiki/Sorting_algorithm) that repeatedly steps through the list, compares adjacent pairs and [swaps](https://en.wikipedia.org/wiki/Swap_(computer_programming)) them if they are in the wrong order. The pass through the list is repeated until the list is sorted. The algorithm, which is a [comparison sort](https://en.wikipedia.org/wiki/Comparison_sort), is named for the way smaller or larger elements "bubble" to the top of the list. Although the algorithm is simple, it is too slow and impractical for most problems even when compared to [insertion sort](https://en.wikipedia.org/wiki/Insertion_sort). Bubble sort can be practical if the input is in mostly sorted order with some out-of-order elements nearly in position. -- [Wikipedia](https://en.wikipedia.org/wiki/Bubble_sort)

&#160;&#160;&#160;&#160;&#160;The above paragraph is from Wikipedia, but I think it is difficult for many people to understand. That is a very official and rigid introduction. So let me simplify it!

----------

&#160;&#160;&#160;&#160;&#160;The most important thing about Bucket Sort is that it wastes space! For example, if the range of sorting needs to be between 0 and 2100000000, then you need to apply 2100000001 variables, which mean to write `int a[2100000001]`. Because we need to go to 2100000001 "buckets" to store the number of occurrences of each number between 0 and 2100000000. Even if you only sort 5 numbers (for instance, the 5 numbers are 1, 1912345678, 2100000000, 18000000, and 912345678), you still need 2100000001 "buckets", which is a waste of space! Also, what if you need to sort now instead of integers but some decimals, such as sorting the five numbers 5.56789, 2.12, 1.1, 3.123, 4.1234 from small to large? Bubble sorting can solve these two questions.

&#160;&#160;&#160;&#160;&#160;**The basic idea of bubble sorting is to "receive two adjacent elements each time and swap them if they are in the wrong order"**

----------

&#160;&#160;&#160;&#160;&#160;For example, we need to sort the 5 numbers of 12 35 99 18 76 from large to small. Since it is sorted from big to small, that is, **the smaller in the end**, you think I am talking nonsense, but this sentence is very important.

&#160;&#160;&#160;&#160;&#160;First compare the size of the 1st and 2nd bits, now the first bit is 12 and the second bit is 35. It is found that 12 is smaller than 35, because we want the smaller in the end, so we need in order to swap the positions of these two numbers. The order of the five numbers after the exchange is 35 **12** 99 18 76.

&#160;&#160;&#160;&#160;&#160;Follow the preceding method and continue to compare the size of bits 2 and 3. The second bit is 12 and the third bit is 99. 12 is smaller than 99, so you are required to swap the positions of these two numbers. The order of the five numbers after the exchange is 35 99 **12** 18 76.

&#160;&#160;&#160;&#160;&#160;According to the previous rule, continue to compare the size of the 3rd and 4th digits. If the 3rd digit is smaller than the 4th digit, the position is exchanged. The order of the five numbers after the exchange is 35 99 18 **12** 76.

&#160;&#160;&#160;&#160;&#160;Finally, compare the 4th and 5th bits. The order of 5 numbers after 4 comparisons is 35 99 18 76 **12**.

&#160;&#160;&#160;&#160;&#160;After 4 comparisons, we found that the smallest number is already (already in the last bit, please note the movement of 12 this number), is it amazing? Now recalls the process of comparison. Each time, **the two adjacent numbers are comparable**. If the latter number is larger than the previous number, the positions of the two numbers are exchanged. It has been compared until the last two numbers are comparable, and the smallest number is in the last one. It's like a bubble, stepping back and forth, until the last one. So this sorting method has a nice name "bubble sorting".

![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Bubble%20Sort/Bubble%20Sort.png)

&#160;&#160;&#160;&#160;&#160;In fact, our sorting only homing the smallest of the five numbers. Every time we return a number, we call it "one time." Below we will continue to repeat the previous process, homing the remaining 4 numbers one by one.

&#160;&#160;&#160;&#160;&#160;First, compare the first digit is smaller than the second digit, the position is swapped. The order of The five numbers after the exchange is 99 35 18 76 12. The next step should be to compare the 2nd and 3rd, 3rd and 4th. Note that it is no longer necessary to compare the 4th and 5th bits. Because after the end of the First pass, it can be determined that the 5th position is the smallest. The order of the five numbers after the end of the second pass is 99 35 76 18 12.

