# Summary of Sorting Algorithms

&#160;&#160;&#160;&#160;&#160;In [computer science](https://en.wikipedia.org/wiki/Computer_science), a **sorting algorithm** is an [algorithm](https://en.wikipedia.org/wiki/Algorithm) that puts elements of a [list](https://en.wikipedia.org/wiki/List_(abstract_data_type)) in a certain [order](https://en.wikipedia.org/wiki/Total_order). The most frequently used orders are [numerical order](https://en.wikipedia.org/wiki/Sequence#Analysis) and [lexicographical order](https://en.wikipedia.org/wiki/Lexicographical_order). Efficient [sorting](https://en.wikipedia.org/wiki/Sorting) is important for optimizing the efficiency of other algorithms (such as [search](https://en.wikipedia.org/wiki/Search_algorithm) and [merge](https://en.wikipedia.org/wiki/Merge_algorithm) algorithms) which require input data to be in sorted lists. Sorting is also often useful for [canonicalizing](https://en.wikipedia.org/wiki/Canonicalization) data and for producing human-readable output.

&#160;&#160;&#160;&#160;&#160;The above paragraph is from Wikipedia, but I think it is difficult for many people to understand. That is a very official and rigid introduction. So let me simplify it!

----------

&#160;&#160;&#160;&#160;&#160;There are many sorting algorithms, for example [Selection sort](https://en.wikipedia.org/wiki/Selection_sort), [Counting sort](https://en.wikipedia.org/wiki/Counting_sort), [Radix sort](https://en.wikipedia.org/wiki/Radix_sort), [Insertion Sort](https://en.wikipedia.org/wiki/Insertion_sort), [Merge sort](https://en.wikipedia.org/wiki/Merge_sort), [Heapsort](https://en.wikipedia.org/wiki/Heapsort), and so on. Heap sorting is even a sorting based on binary trees.

&#160;&#160;&#160;&#160;&#160;Now let's take a concrete example (adapted from the Youth Informatics Olympic League) to practice these three sorting algorithms. Differences and limitations in the application of three sorts.

----------

&#160;&#160;&#160;&#160;&#160;Tony’s school wanted to set up a book corner. The teacher sent Tony to find some students to do the survey and see which books the students liked. Tony asked each student to write an ISBN number for each book they wanted to read (each book has a unique ISBN number). Of course, there are some good books that many students like, so they will collect a lot of duplicate ISBN numbers.

&#160;&#160;&#160;&#160;&#160;Tony needs to remove the duplicate ISBN number, that is, only one for each ISBN number, which means that the same book only buys one. Then sort these ISBN numbers from small to large, and Tony will go to the bookstore to buy books according to the sorted ISBN number.

&#160;&#160;&#160;&#160;&#160;Please help Tony complete the work of "deduplication" and "sorting"

![](https://raw.githubusercontent.com/liutiantian233/Magical-Algorithms/master/Sort/Summary%20of%20Sorting%20Algorithms/Summary%20of%20Sorting%20Algorithms.png)

&#160;&#160;&#160;&#160;&#160;The input has 2 lines, and the first line is a positive integer, indicating that there are n students participating in the survey (n<=100). Line 2 has n positive integers separated by spaces, which is the ISBN number of each book (assuming the book's ISBN number is between 1 and 1000).

&#160;&#160;&#160;&#160;&#160;The output is also 2 lines, the first line is a positive integer k, indicating how many books need to be bought. The second line is k positive integers separated by spaces, which are the ISBNs of books that need to be purchased from small to large.

&#160;&#160;&#160;&#160;&#160;Such as input

```
10
20 40 32 67 40 20 89 300 400 15
```

&#160;&#160;&#160;&#160;&#160;Then output

```
8
15 20 32 40 67 89 300 400
```

&#160;&#160;&#160;&#160;&#160;Finally, the time limit for running the program is: 1 second.

&#160;&#160;&#160;&#160;&#160;There are roughly two ways to solve this problem. The first method: first remove the ISBN numbers of the n books, and then sort them from small to large and output them. The second method: sort from small to large, and then remove when output. Both methods are fine.

&#160;&#160;&#160;&#160;&#160;Let's look at the first method. We found that modifying bucket sorting can have a deduplication effect, so we can use bucket sorting to solve this problem.

```c
#include <stdio.h>

int main()
{
  int a[1001],n,i,t;
  
  for(i=1;i<=1000;i++)
    a[i]=0;
  
  scanf("%d",&n);
  
  for(i=1;i<=n;i++)
  {
    scanf("%d",&t);
    a[t]=1;
  }
  
  for(i=1;i<=1000;i++)
  {
    if(a[i]==1)
      printf("%d ",i);
  }
  
  getchar();getchar();
  return 0;
}
```

&#160;&#160;&#160;&#160;&#160;**The time complexity of this method same with that the time complexity of bucket sorting is O(N+M).**

&#160;&#160;&#160;&#160;&#160;The second method, we need to sort first and then deduplication. Sorting we can use bubble sorting or quick sorting.

```
20 40 32 67 40 20 89 300 400 15
```

&#160;&#160;&#160;&#160;&#160;Sorting these 10 numbers from small to large is `15 20 20 32 40 40 67 89 300 400`.

&#160;&#160;&#160;&#160;&#160;Next, remove the duplicates at the output. Because we are already in order, the same numbers will be close together. At the time of output, it is judged in advance whether the current number a[i] is the same as the previous number a[i-1]. If they are the same, it means that this number has been output before, and it does not need to be output again. Different means that this number is the first time, you need to output this number.

```c
#include <stdio.h>

int main()
{
  int a[101],n,i,j,t;
  
  scanf("%d",&n);
  
  for(i=1;i<=n;i++)
  {
    scanf("%d",&a[i]);
  }
  
  for(i=1;i<=n-1;i++)
  {
    for(j=1;j<=n-i;j++)
    {
      if(a[j]>a[j+1])
      {
        t=a[j];
        a[j]=a[j+1];
        a[j+1]=t;
      }
    }
  }
  
  printf("%d ",a[1]);
  
  for(i=2;i<=n;i++)
  {
    if(a[i] != a[i-1])
      printf("%d ",a[i]);
  }
  
  getchar();getchar();
  return 0;
}
```

&#160;&#160;&#160;&#160;&#160;The **time complexity** of this method consists of **two parts**, one is that the bubble sorting time complexity is **O(N^2)**, and the other part is that the input and output are both **O(N)**, so the whole algorithm The time complexity is **O(N+N+N^2)**. Relative to N^2, N+N can be ignored (we usually ignore low order), and finally the time complexity of the method is **O(N^2)**.

&#160;&#160;&#160;&#160;&#160;Next we need to look at the data range. The ISBN number of each book is an integer between 1 and 1000, and the number of students participating in the survey does not exceed 100, that is, n <= 100. As I said before, when we roughly calculate the time complexity, we usually think that the computer runs about 1 billion times per second (of course, the actual situation is faster). Therefore, both methods can calculate the solution in 1 second.

&#160;&#160;&#160;&#160;&#160;If the ISBN number of the book is not between 1 and 1000, but between -2147483648 and 2147483647, then the first method is not feasible, because you can't apply for such a large array to mark whether each ISBN has appeared.

&#160;&#160;&#160;&#160;&#160;In addition, if the range of n is not less than or equal to 100 but less than or equal to 100,000, the sorting part of the second method cannot use the bubble sorting. Because the time limit required by the title is 1 second, using a bubble sort to sort 100,000 numbers, the computer needs to run 10 billion times, it takes 10 seconds, and needs to be replaced with Quick sort. Quick sorting only needs 100000×log2100000=100000×17=1.7 million times, which is less than 0.0017 seconds.

&#160;&#160;&#160;&#160;&#160;**Is it amazing, the same problem with different algorithms has such a large time gap, this is the charm of the algorithm!**

&#160;&#160;&#160;&#160;&#160;Let's review the time complexity of the three sorting algorithms. Bucket sorting is the fastest, its time complexity is **O(N+M)**; bubble sorting is **O(N^2)**; Quick sorting is **O(N log N)**.

---------

## Feedback and suggestions

- E-mail：<liutia20@msu.edu>

---------

Thank you for reading my notes and ideas.
