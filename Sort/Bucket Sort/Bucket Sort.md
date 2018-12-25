# Bucket Sort

&#160;&#160;&#160;&#160;&#160;**Bucket sort**, or **bin sort**, is a [sorting algorithm](https://en.wikipedia.org/wiki/Sorting_algorithm) that works by distributing the elements of an [array](https://en.wikipedia.org/wiki/Array_data_structure) into a number of [buckets](https://en.wikipedia.org/wiki/Bucket_(computing)). Each bucket is then sorted individually, either using a different sorting algorithm, or by recursively applying the bucket sorting algorithm. It is a [distribution sort](https://en.wikipedia.org/wiki/Sorting_algorithm#Distribution_sort), a generalization of [pigeonhole sort](https://en.wikipedia.org/wiki/Pigeonhole_sort), and is a cousin of [radix sort](https://en.wikipedia.org/wiki/Radix_sort) in the most-to-least significant digit flavor. Bucket sort can be implemented with comparisons and therefore can also be considered a [comparison sort](https://en.wikipedia.org/wiki/Comparison_sort) algorithm. The [computational complexity](https://en.wikipedia.org/wiki/Analysis_of_algorithms) depends on the algorithm used to sort each bucket, the number of buckets to use, and whether the input is uniformly distributed. -- [Wikipedia](https://en.wikipedia.org/wiki/Bucket_sort)

&#160;&#160;&#160;&#160;&#160;The above paragraph is from Wikipedia, but I think it is difficult for many people to understand. That is a very official and rigid introduction. So let me simplify it!

----------

&#160;&#160;&#160;&#160;&#160;In the world we live in, there are things that are sorted everywhere. When standing in the team, they will be sorted according to their height. The ranking of the exams needs to be sorted according to the score. When shopping online, they will be sorted by price, and the emails in the email will be sorted by time.

&#160;&#160;&#160;&#160;&#160;In short, many things need to sort, it can be said that sorting is everywhere. Now let's take a concrete example to introduce the sorting algorithm.

----------

&#160;&#160;&#160;&#160;&#160;After the final exam, the teacher will sort the students' scores from high to low. There are only 5 students in Tony's class. The 5 students scored 5 points, 3 points, 5 points, 2 points and 8 points respectively. The score is really terrible (out of 10 points). The scores are then sorted from large to small, sorted to 8 5 5 3 2 . Do you have any good way to write a program that allows the computer to randomly read 5 numbers and then output the 5 numbers from large to small? Please think about it, at least 15 minutes and then look down.

&#160;&#160;&#160;&#160;&#160;We can solve this problem with a one-dimensional array here. Please make sure you really think about it and look down.

&#160;&#160;&#160;&#160;&#160;First we need to apply an array of size 11 int a[11] OK, now you have 11 variables, numbered from a[0]~a[10]. At the beginning, we initialized a[0]~a[10] to 0, indicating that none of these scores have been obtained. For example, if a[0] is equal to 0, it means that no one has ever scored 0. Similarly, a[1] is equal to 0, which means that no one has scored 1 point yet. a[10] equals 0, which means that no one has scored 10 points yet.

![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Bucket%20Sort/Bucket%20Sort%20p1.png)

&#160;&#160;&#160;&#160;&#160;Let's start processing each individual's score. The first person's score is 5 points. We will increase the value of the corresponding a[5] by 1 on the original basis, that is, the value of a[5] is changed from 0 to 1, indicating that 5 points have appeared once.

![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Bucket%20Sort/Bucket%20Sort%20p2.png)

&#160;&#160;&#160;&#160;&#160;The score of the second person is 3 points. We increase the value of the corresponding a[3] by 1 on the original basis, that is, the value of a[3] is changed from 0 to 1, indicating that the 3 points have appeared once.

![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Bucket%20Sort/Bucket%20Sort%20p3.png)

&#160;&#160;&#160;&#160;&#160;Note! The score of the third person is also 5 points, so the value of a[5] needs to be increased by 1 on the basis of this, that is, the value of a[5] is changed from 1 to 2, indicating that 5 points have appeared twice.

![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Bucket%20Sort/Bucket%20Sort%20p4.png)

&#160;&#160;&#160;&#160;&#160;The scores of the fourth and fifth individuals are processed according to the method just described. The end result is the picture below.

![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Bucket%20Sort/Bucket%20Sort%20p5.png)

&#160;&#160;&#160;&#160;&#160;You find that the value in a[0]~a[10] is actually the number of times each score appears from 0 to 10. Next, we only need to print out the scores that have appeared, and print them several times, as shown below.

- a[0] is 0, indicating that "0" has not appeared and is not printed.
- a[1] is 0, indicating that "1" has not appeared and is not printed.
- a[2] is 1, indicating that "2" has appeared once and prints 2.
- a[3] is 1, indicating that "3" has appeared once and prints 3.
- a[4] is 0, indicating that "4" has not appeared and is not printed.
- a[5] is 2, indicating that "5" has appeared 2 times and prints 5 5 .
- a[6] is 0, indicating that "6" has not appeared and is not printed.
- a[7] is 0, indicating that "7" has not appeared and is not printed.
- a[8] is 1, indicating that "8" has appeared once, and prints 8.
- a[9] is 0, indicating that "9" has not appeared and is not printed.
- a[10] is 0, indicating that "10" has not appeared and is not printed.

&#160;&#160;&#160;&#160;&#160;The final screen outputs "2 3 5 5 8", the complete code is as follows **use the C**

```c
#include <stdio.h>
int main()
{
    int a[11],i,j,t;
    for(i=0;i<=10;i++)
        a[i]=0;

    for(i=1;i<=5;i++)
    {
        scanf("%d",&t);
        a[t]++;
    }

    for(i=0;i<=10;i++)
        for(j=1;j<=a[i];j++)
            printf("%d ",i);

    getchar();getchar();
    return 0;
}
```

The input data is:

```c
5 3 5 2 8
```

&#160;&#160;&#160;&#160;&#160;A closer look reveals that what was just achieved is the order from small to large. But our request is to sort from big to small, what should we do?

&#160;&#160;&#160;&#160;&#160;it's actually really easy. Just change `for(i=0;i<=10;i++)` to `for(i=10;i>=0;i--)` and it will be OK.

&#160;&#160;&#160;&#160;&#160;This sorting method we call it "bucket sorting" for the time being. Because the real bucket sorting is more complicated than this, we will discuss it in detail later. At present, this algorithm can meet our needs.

&#160;&#160;&#160;&#160;&#160;This algorithm is like having 11 buckets, numbered from 0 to 10. For each number, a small flag is placed in the corresponding numbered bucket. Finally, as long as there are several small flags in each bucket, it is OK. For example, there is a small flag in the No. 2 bucket, which means that 2 appears once; in the No. 3 bucket, there is a small flag, which means that 3 appears once; in the No. 5 bucket, there are 2 small flags, indicating that 5 appears twice; There is a small flag in the 8th barrel, indicating that 8 has appeared once.

![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Bucket%20Sort/Bucket%20Sort%20p6.png)

&#160;&#160;&#160;&#160;&#160;Now can try to enter n integers between 0 and 1000 and sort them from large to small. If need to sort the integers with data range from 0 to 1000, we need 1001 buckets to represent the number of occurrences of each number between 0 and 1000. This must be noted. In addition, the function of each bucket here is actually "marking" the number of occurrences of each number, so I like to replace the previous array 'a' with a more appropriate name book (the word has the Record, the meaning of the mark), the code is implemented. as follows.

```c
#include <stdio.h>
int main()
{
    int book[1001],i,j,t,n;
    for(i=0;i<=1000;i++)
        book[i]=0;

    scanf("%d",&n);

    for(i=1;i<=n;i++)
    {
        scanf("%d",&t);
        book[t]++;
    }

    for(i=1000;i>=0;i--)
        for(j=1;j<=book[i];j++)
            printf("%d ",i);

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
1000 999 100 50 22 15 8 6 1 0
```

&#160;&#160;&#160;&#160;&#160;Finally, let's talk about the complexity of time. The loop in line 6 of the code is looped a total of m times (m is the number of buckets), the code of line 9 is looped n times (n is the number of numbers to be sorted), and lines 14 and 15 are looped together. m+n times. So the entire sorting algorithm performs a total of m+n+m+n times.

&#160;&#160;&#160;&#160;&#160;We use the capital letter O to represent the time complexity, so the time complexity of the algorithm is O(m+n+m+n) or O(2*(m+n)). We can ignore smaller constants when we say time complexity, and the time complexity of bucket sorting is O(m+n). Another point is that when expressing time complexity, n and m are usually in uppercase letters, O(M+N).

&#160;&#160;&#160;&#160;&#160;This is a very fast sorting algorithm. Bucket sorting has been used since 1956, and the basic idea of the algorithm was proposed by EJIssac and RCSingleton. As I said before, this is not really a bucket sorting algorithm. The real bucket sorting algorithm is more complicated than this. One thing to note is that the current simplified version of the bucket sorting algorithm is not really a sorting algorithm in the true sense. why? For example, if you encounter the following example, there is no way.

&#160;&#160;&#160;&#160;&#160;There are now five people's names and scores: huhu 5 points, haha 3 points, xixi 5 points, hengheng 2 points, and gaoshou 8 points. Please output their names according to the score from high to low. Should output gaoshou, huhu, xixi, haha, hengheng. If we use the bucket sorting algorithm we just simplified, we just sort the scores. The final output is just a score, but the people themselves are not sorted. In other words, we don't know which one the sorted score originally corresponds to! What should we do? Don't worry, we still have a bubble sort.

---------

## Feedback and suggestions
- E-mail：<liutia20@msu.edu>

Thanks for reading 
