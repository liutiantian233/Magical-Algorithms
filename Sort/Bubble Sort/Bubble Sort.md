# Bubble Sort

&#160;&#160;&#160;&#160;&#160;**Bubble sort**, sometimes referred to as **sinking sort**, is a simple [sorting algorithm](https://en.wikipedia.org/wiki/Sorting_algorithm) that repeatedly steps through the list, compares adjacent pairs and [swaps](https://en.wikipedia.org/wiki/Swap_(computer_programming)) them if they are in the wrong order. The pass through the list is repeated until the list is sorted. The algorithm, which is a [comparison sort](https://en.wikipedia.org/wiki/Comparison_sort), is named for the way smaller or larger elements "bubble" to the top of the list. Although the algorithm is simple, it is too slow and impractical for most problems even when compared to [insertion sort](https://en.wikipedia.org/wiki/Insertion_sort). Bubble sort can be practical if the input is in mostly sorted order with some out-of-order elements nearly in position. -- [Wikipedia](https://en.wikipedia.org/wiki/Bubble_sort)

&#160;&#160;&#160;&#160;&#160;The above paragraph is from Wikipedia, but I think it is difficult for many people to understand. That is a very official and rigid introduction. So let me simplify it!

----------

&#160;&#160;&#160;&#160;&#160;The most important thing about Bucket Sort is that it wastes space! For example, if the range of sorting needs to be between 0 and 2100000000, then you need to apply 2100000001 variables, which mean to write `int a[2100000001]`. Because we need to go to 2100000001 "buckets" to store the number of occurrences of each number between 0 and 2100000000. Even if you only sort 5 numbers (for instance, the 5 numbers are 1, 1912345678, 2100000000, 18000000, and 912345678), you still need 2100000001 "buckets", which is a waste of space! Also, If you need to sort now, not an integer but some decimals, such as sorting the five numbers 5.56789, 2.12, 1.1, 3.123, 4.1234 from small to large? Bubble sorting can solve these two questions.

&#160;&#160;&#160;&#160;&#160;**The basic idea of bubble sorting is to "receive two adjacent elements each time and swap them if they are in the wrong order"**

----------

&#160;&#160;&#160;&#160;&#160;For example, we need to sort the 5 numbers of 12 35 99 18 76 from large to small. Since it is sorted from big to small, that is, **the smaller in the end**, the more you feel that I am talking nonsense, but this sentence is very important.

&#160;&#160;&#160;&#160;&#160;First compare the size of the 1st and 2nd bits, now the first bit is 12 and the second bit is 35. It is found that 12 is smaller than 35, because we want the smaller in the end, so we need in order to swap the positions of these two numbers. The order of the five numbers after the exchange is 35 **12** 99 18 76.

&#160;&#160;&#160;&#160;&#160;Follow the previous method and continue to compare the size of bits 2 and 3. The second bit is 12 and the third bit is 99. 12 is smaller than 99, so you are required to swap the positions of these two numbers. The order of the five numbers after the exchange is 35 99 **12** 18 76.

&#160;&#160;&#160;&#160;&#160;According to the previous rule, continue to compare the size of the 3rd and 4th digits. If the 3rd digit is smaller than the 4th digit, the position is exchanged. The order of the five numbers after the exchange is 35 99 18 **12** 76.

&#160;&#160;&#160;&#160;&#160;Finally, compare the 4th and 5th bits. The order of 5 numbers after 4 comparisons is 35 99 18 76 **12**.

&#160;&#160;&#160;&#160;&#160;After 4 comparisons, we found that the smallest number is already (already in the last bit, please note the movement of 12 this number), is it amazing? Now recalls the process of the comparison. Each time, **the two adjacent numbers are comparable**. If the latter number is larger than the previous number, the positions of the two numbers are exchanged. It has been compared until the last two numbers are comparable, and the smallest number is in the last one. It's like a bubble, stepping back and forth, until the last one. So this sorting method has a nice name **"bubble sorting"**.

![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Bubble%20Sort/Bubble%20Sort.png)

&#160;&#160;&#160;&#160;&#160;In fact, our sorting is just to home the smallest of the five numbers. Every time we return a number, we call it "once." Below we will continue to repeat the previous process, homing the remaining 4 numbers one by one.

&#160;&#160;&#160;&#160;&#160;Ok, now it’s the “second time” and the goal is tantamount to put the second smallest number back. First, compare the first and second digits first. If the first digit is smaller than the second digit, the position is swapped. The order of the five numbers after the exchange is 99 35 18 76 12. Next, you should compare the 2nd and 3rd, 3rd and 4th. Note that it is no longer necessary to compare the 4th and 5th bits. Because after the first end, it can be determined that the number placed in the 5th position is the smallest. The order of the five numbers after the second end is 99 35 76 18 12.

&#160;&#160;&#160;&#160;&#160;The "third time" is the same. The order of the five numbers after the third time is 99 76 35 18 12.

&#160;&#160;&#160;&#160;&#160;Now! It is the last "fourth time". Do you want to continue? Of course, this is merely coincidental. If you use other numbers, you may not be.

&#160;&#160;&#160;&#160;&#160;The principle of "bubble sorting" is "every time you can only determine to home a number." That is, for the first time, you can only determine that the number of the last digit (ie, the fifth digit) is homed. The second time, you can only return the number on the second digit of the last digit (that is, the fourth digit). The third time can only be used. The number in the third digit of the countdown (ie, the third digit) is homed, and there are still two positions in the front that is not homed, so we still need to do the "fourth."

&#160;&#160;&#160;&#160;&#160;The “fourth time” only is required to compare the size of the first and second digits. Since the numbers in the last three positions have been homing, the first bit is now 99 and the second bit is 76, no swapping is required. The order of these five numbers remains the same as 99 76 35 18 12. At this point, the sorting is perfectly finished. There are already 4 numbers in the 5 numbers, and the last number can only be put in the 1st place.

&#160;&#160;&#160;&#160;&#160;**Finally, let's summarize**: If there are n numbers to sort, just homing n-1 numbers, that is, n-1 operations. "Every time" need to compare the two adjacent numbers starting from the first digit, and put the smaller one on the back. After the comparison is expected to be completed, move one bit backward to continue comparing the size of the two adjacent numbers below. Repeat this step, until the **last number that has not been homed**, and the number that has been homed does not need to be compared.

----------

&#160;&#160;&#160;&#160;&#160;Is this algorithm very powerful? I remember that every time I took a group photo, I was always replaced by someone else. It was especially annoying. I do not know whether the inspiration for the person who invented this algorithm came from this. Below is the code to look at how I implemented it.

```c
#include <stdio.h>
int main()
{
  int a[100],i,j,t,n;
  
  scanf("%d",&n);
  
  for(i=1;i<=n;i++)
    scanf("%d",&a[i]);
  
  for(i=1;i<=n-1;i++)
  {
    for(j=1;j<=n-i;j++)
    {
      if(a[j]<a[j+1])
      {
        t=a[j];
        a[j]=a[j+1];
        a[j+1]=t;
      }
    }
  }
  for(i=1;i<=n;i++)
    printf("%d ",a[i]);
  
  getchar();getchar();
  return 0;
}
```

&#160;&#160;&#160;&#160;&#160;Can enter the following data for verification.

```
10
8 100 50 22 15 6 1 1000 999 0
```

&#160;&#160;&#160;&#160;&#160;The result of the operation is:

```
0 1 6 8 15 22 50 100 999 1000
```

&#160;&#160;&#160;&#160;&#160;By modifying the above code slightly, can solve the remaining problems, as follows.

```c
#include <stdio.h>

struct student
{
  char name[21];
  char score;
};

int main()
{
  struct student a[100],t;
  int i,j,n;
  scanf("%d",&n);
  
  for(i=1;i<=n;i++)
    scanf("%s %d",a[i].name,&a[i].score);
  
  for(i=1;i<=n-1;i++)
  {
    for(j=1;j<=n-i;j++)
    {
      if(a[j].score<a[j+1].score)
      {
        t=a[j];
        a[j]=a[j+1];
        a[j+1]=t;
      }
    }
  }
  for(i=1;i<=n;i++)
    printf("%s\n",a[i].name);
  
  getchar();getchar();
  return 0;
}
```

&#160;&#160;&#160;&#160;&#160;Can enter the following data for verification.

```
5
huhu 5
haha 3
xixi 5
hengheng 2
gaoshou 8
```

&#160;&#160;&#160;&#160;&#160;The result of the operation is:

```
gaoshou
huhu
xixi
haha
hengheng
```

&#160;&#160;&#160;&#160;&#160;The core part of bubble sorting is a double nested loop. It is not difficult to see that the time complexity of bubble sorting is **O(N^2)**. This is a very high time complexity. The bubble sorting began as early as 1956, and many people have tried to improve the bubble sorting, but the results are disappointing. As Donald E. Knuth (the Turing Award winner in 1974) said. “There is nothing to recommend in addition to its fascinating name and some interesting theoretical issues. ” You may have to ask: Is there a better sorting algorithm? Don't worry, see the next section -- **Quick Sorting**.

---------

## Feedback and suggestions
- E-mail：<liutia20@msu.edu>

---------

Thank you for reading my notes and ideas.
