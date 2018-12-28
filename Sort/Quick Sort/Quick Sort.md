# Quick Sort

&#160;&#160;&#160;&#160;&#160;**Quicksort** (sometimes called **partition-exchange sort**) is an **O(N log N)** [efficient](https://en.wikipedia.org/wiki/Algorithmic_efficiency) [sorting algorithm](https://en.wikipedia.org/wiki/Sorting_algorithm), serving as a systematic method for placing the elements of an [array](https://en.wikipedia.org/wiki/Array_data_structure) in order. Developed by British computer scientist [Tony Hoare](https://en.wikipedia.org/wiki/Tony_Hoare) in 1959 and published in 1961, it is still a commonly used algorithm for sorting. When implemented well, it can be about two or three times faster than its main competitors, [merge sort](https://en.wikipedia.org/wiki/Merge_sort) and [heapsort](https://en.wikipedia.org/wiki/Heapsort).

&#160;&#160;&#160;&#160;&#160;The above paragraph is from Wikipedia, but I think it is difficult for many people to understand. That is a very official and rigid introduction. So let me simplify it!

----------

&#160;&#160;&#160;&#160;&#160;**Bubble sorting** solves the problem of **barrel sorting** wasting space, but it sacrifices a lot in the execution efficiency of the algorithm, and its time complexity reaches **O(N^2)**. If our computer can run 1 billion times per second, then sort 100 million numbers, bucket sorting only takes 0.1 seconds, and bubble sorting takes 10 million seconds, reaching 115 days, is it very scary. The sorting algorithm that neither wastes space nor can be faster is "quick sorting"!

----------

&#160;&#160;&#160;&#160;&#160;Suppose we now sort the 10 numbers `6 1 2 7 9 3 4 5 10 8`. First, figure out a number in this sequence as a **reference number** (a number used for reference). For convenience, let the first number 6 to be used as the reference number. Next, you need to put all the numbers in this sequence larger than the reference number to the right of 6, and the number smaller than the reference number to the left of 6, similar to the following arrangement.

```
3  1  2  5  4  6  9  7  10  8
```

&#160;&#160;&#160;&#160;&#160;In the initial state, the number 6 is at the first bit of the sequence. Our goal is to move 6 to a position in the middle of the sequence, assuming this position is k. Now you need to find this k, with the k th position as the demarcation point, the number on the left is less than or equal to 6, and the number on the right is greater than or equal to 6.

&#160;&#160;&#160;&#160;&#160;Recalling the bubble sorting, how to make each number homing steps by step through "swap". At this point, the "exchange" method can also be used to achieve the goal.

&#160;&#160;&#160;&#160;&#160;The method is actually very simple: **"Probe"** is started from both ends of the initial sequence `6 1 2 7 9 3 4 5 10 8`. First find a number less than 6 from right to left, then find a number greater than 6 from left to right, and then exchange them. Here we can use two variables i and j, pointing to the leftmost and rightmost of the sequence. We have a nice name for these two variables, **"Sentinel i"** and **"Sentinel j"**. At the beginning, let the sentinel i point to the far left of the sequence (ie i=1), pointing to the number 6. Let the sentinel j point to the far right of the sequence (ie j=10), pointing to the number 8.

![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Quick%20Sort/Quick%20Sort%20p1.png)

&#160;&#160;&#160;&#160;&#160;First the sentinel j began to move. Since the reference number is the leftmost number, it is important to have the sentinel j move first. The sentinel j moves to the left step by step (ie j--) until it finds a number less than 6 to cease. Then the sentinel i moves to the right step by step (ie i++) until it finds a number greater than 6 to stop. Finally, the sentinel j stopped in front of the number 5, and the sentinel i stopped in front of the number 7.

![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Quick%20Sort/Quick%20Sort%20p2.png)

&#160;&#160;&#160;&#160;&#160;Now exchange the values of the elements pointed to by Sentinel i and Sentinel j. The sequence after the exchange is as follows.

```
6  1  2  5  9  3  4  7  10  8
```

&#160;&#160;&#160;&#160;&#160;At this point, the first exchange is done. Next, the sentinel j is still move to the left (reminder! Every time it must be the sentinel j first). He found 4 (smaller than the benchmark 6, meeting the requirements) and then stopped. Sentinel i also continued to move to the right, he found 9 (larger than the benchmark number 6, to meet the requirements) and then stopped. At this time, the exchange is performed again, and the sequence after the exchange is reproduced below.

```
6  1  2  5  4  3  9  7  10  8
```

![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Quick%20Sort/Quick%20Sort%20p3.png)

&#160;&#160;&#160;&#160;&#160;The subsequent exchange ends and the "probe" continues. The sentinel j continued to be move to the left, and he found 3 (smaller than the baseline number 6, meeting the requirements) and then stopped. Sentinel i continues to move to the right. Bad! At this point, the sentinel i and the sentinel j met, and the sentinel i and the sentinel j both went to 3. Explain that the "probe" ends. We exchange benchmarks 6 and 3. The sequence after the exchange is reproduced below.

```
3  1  2  5  4  6  9  7  10  8
```

![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Quick%20Sort/Quick%20Sort%20p4.png)

![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Quick%20Sort/Quick%20Sort%20p5.png)

&#160;&#160;&#160;&#160;&#160;At this point, the first round of "probe" really ended. At this time, the reference number 6 serves as the demarcation point, and the number on the left side of 6 is less than or equal to 6, and the number on the right side of 6 is greater than or equal to 6. Looking back at the process, in fact, the mission of the sentinel j is to find a number less than the benchmark number, and the mission of the sentinel i is to find a number greater than the benchmark number until i and j meet.

&#160;&#160;&#160;&#160;&#160;OK, the explanation is completed. Now that the benchmark number 6 has been homing, it is in the sixth place in the sequence. At this point, we have split the original sequence into two sequences with a dividing point of 6. The sequence on the left is `3 1 2 5 4` and the sequence on the right is `9 7 10 8`. Next, you need to process the two sequences separately. Because the sequence of the left and right of 6 are still very confusing. But it doesn't matter, I have mastered the method, and then just simulate the previous method to process the left and right sequences separately. Now go to deal with the sequence on the left of 6.

&#160;&#160;&#160;&#160;&#160;The sequence on the left is `3 1 2 5 4`. Please adjust this sequence to 3, so that the number on the left of 3 is less than or equal to 3, and the number on the right of 3 is greater than or equal to 3. The order of the sequences after the adjustment is completed should be like this.

```
2  1  3  5  4
```

&#160;&#160;&#160;&#160;&#160;OK, now 3 has been returned. Next, we need to process the sequence `2 1` on the left and the sequence `5 4` on the right. The sequence `2 1` is adjusted with reference to 2, and the sequence after the processing is completed is `1 2`, and 2 has been homing. The sequence `1` has only one number and does not prescribe any processing. So far we have completely processed the sequence `2 1` and the sequence is `1 2`. The processing of the sequence `5 4` is also modeled after this method, and the resulting sequence is reproduced below.

```
1  2  3  4  5  6  9  7  10  8
```

&#160;&#160;&#160;&#160;&#160;The sequence `9 7 10 8` also simulates the previous process until a new subsequence cannot be split. The sequence will eventually be obtained as follows.

```
1  2  3  4  5  6  7  8  9  10
```

&#160;&#160;&#160;&#160;&#160;At this point, the sorting is completely over. Each round of quick sorting is actually homing the baseline number of this round until all the numbers are put in place, and the sorting is over. The following is the processing of the entire algorithm.

![image](https://github.com/liutiantian233/Magical-Algorithms/blob/master/Sort/Quick%20Sort/Quick%20Sort%20p6.png)

&#160;&#160;&#160;&#160;&#160;Quick sorting is faster because each swap is skipped compared to bubble sorting. **Set a reference point each time you sort, put all the numbers less than or equal to the reference point to the left of the reference point, and put all the numbers greater than or equal to the reference point to the right of the reference point.** In this way, each time you exchange, you can't exchange between adjacent numbers like a bubble sort, and the exchange distance is much larger. Therefore, the total number of comparisons and exchanges is reduced, and the speed naturally increases. Of course, in the worst case, it is still possible that two adjacent numbers are exchanged. So, the worst time complexity of Quick sorting and the bubble sorting are the same as O(N^2), and its average time complexity is O(N log N). In fact, quick sorting is based on an idea called "dichotomy." Code shows as below.

```c
#include <stdio.h>
int a[101],n;

void quicksort(int left,int right)
{
  int i,j,t,temp;
  if(left>right)
    return;
    
  temp=a[left];
  i=left;
  j=right;
  
  while(i!=j)
  {
    while(a[j]>=temp && i<j)
      j--;
    
    while(a[i]<=temp && i<j)
      i++;
      
    if(i<j)
    {
      t=a[i];
      a[i]=a[j];
      a[j]=t;
    }
  }
  
  a[left]=a[i];
  a[i]=temp;
  quicksort(left,i-1);
  quicksort(i+1,right);
}

int main()
{
  int i,j,t;
  scanf("%d",&n);
  
  for(i=1;i<=n;i++)
    scanf("%d",&a[i]);
  
  quicksort(1,n);
  
  for(i=1;i<=n;i++)
    printf("%d ",a[i]);
  
  getchar();getchar();
  return 0;
}
```

&#160;&#160;&#160;&#160;&#160;Can enter the following data for verification:

```
10
6  1  2  7  9  3  4  5  10  8
```

&#160;&#160;&#160;&#160;&#160;The result of the operation is:

```
1 2 3 4 5 6 7 8 9 10
```

&#160;&#160;&#160;&#160;&#160;The following is the change process of array a during program execution.

```
6 1 2 7 9 3 4 5 10 8
3 1 2 5 4 6 9 7 10 8
2 1 3 5 4 6 9 7 10 8
1 2 3 5 4 6 9 7 10 8
1 2 3 5 4 6 9 7 10 8
1 2 3 4 5 6 9 7 10 8
1 2 3 4 5 6 9 7 10 8
1 2 3 4 5 6 8 7 9 10
1 2 3 4 5 6 7 8 9 10
1 2 3 4 5 6 7 8 9 10
1 2 3 4 5 6 7 8 9 10
```

&#160;&#160;&#160;&#160;&#160;The quick sort was proposed by **C. A. R. Hoare (Charles Antony Richard Hoare)** in 1960, and many others have been further optimized. If you are interested in quick sorting, you can check out the paper "Quicksort" published by Hoare in the **_Computer Journal_** in 1962 and the seventh chapter of "Introduction to Algorithms".

&#160;&#160;&#160;&#160;&#160;The quick sorting algorithm was only the first time that Hoare was able to show his talents in the computer field. Later he was appreciated and reused by the boss. The company hopes that he will design a new high-level language for the original machine. Be aware that there are no high-level languages like **PASCAL** or **C** at the time.

&#160;&#160;&#160;&#160;&#160;Later, Hoare participated in the **"ALGOL 60"** training course organized by **Edsger Wybe Dijkstra (the Turing Award winner in 1972)**. He felt that he did not be too confident as he was to design a new language. It was best to carry out the existing **"ALGOL 60"**. Improved so that it can be used on the company's latest machines. So he designed a subset of the **"ALGOL 60"** version.

&#160;&#160;&#160;&#160;&#160;This version is the perfect in the implementation of **"ALGOL 60"** in terms of efficiency and reliability, so Hoare has received the attention of the international academic community.

&#160;&#160;&#160;&#160;&#160;Then, he also invented the well-known **"case" statement** in the design of **"ALGOL X"**, which was later widely used in various high-level languages, such as **PASCAL**, **C**, **Java**, and so on. Of course, Hoare has a lot of contributions in the computer field. He won the **Turing Award** in 1980.

---------

## Feedback and suggestions
- E-mail：<liutia20@msu.edu>

---------

Thank you for reading my notes and ideas.
