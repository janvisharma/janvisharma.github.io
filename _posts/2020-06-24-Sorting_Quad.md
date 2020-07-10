---
header:
  overlay_image: /assets/images/sort_quad.jpg
title: Sorting In Quadratic Time
excerpt: "Common techniques to sort in quadratic time."
---
Problem Statement: You are given 'n' elements and we have no prior information
about the nature of these elements nor do we know of any structure/order that these elements might be in. The task is to sort these elements in ascending order.

Comparison Model: The only way to get information about the order of two elements 'a' and 'b' is by comparing them. Comparison could yield one of the following 3 conclusions: (1) $$a>b$$ (2) $$a<b$$ (3) $$a=b$$ 

<h1>Bubble Sort</h1>
An intuitve approach to sort would be to continuously compare adjacent elements and swap elements that are out of order. This is precisely the idea behind Bubble Sort.

We start by comparing the first two elements, if they are out of order we swap them, then we compare the second and the third elements and so on. 

This way, elements 'bubble' to their correct position by contiuous swaps.

Code for Bubble Sort in Python:
{% highlight wl linenos %}
{% raw %}
def bubbleSort(lst_nums):
    i = 0 
    j = 0 
    for i in range(len(lst_nums)):
        for j in range(0,len(lst_nums)-i-1): 
            if lst_nums[j+1]<lst_nums[j]: # ascending order
                lst_nums[j+1], lst_nums[j] = lst_nums[j], lst_nums[j+1] # swap 
    return lst_nums
{% endraw %}
{% endhighlight %}

<br>
<h1>Time Analysis for Bubble Sort Algorithm</h1>

A simple way to calculate the time complexity of the bubble sort algorithm is by using the loop rule. The outer for loop runs in O(n) time and the nested j loop runs in O(n) time, thus the complexity of the two loops: 

= (number of iterations of for loop for i)$$*$$(code nested inside the for loop for i )<br>
= O(n)$$*$$(the nested for loop for j iterates n times and the swap statements contribute O(1))<br>
= O(n)*O(n)<br>
= $$O(n^2)$$ <br>

A more analytical way to look at the the time complexity is to consider the inversion argument. <br>
For an element 'x', its inversion is defined as an element 'z' such that:
(1) $$z < x$$
(2) z lies on the right of x

What this means is that 'z' is some element which is **not** in its correct position.

[*Note that we are assuming that we intend to sort the elements in ascending order*]

Now, we should ask ourselves, how many swaps do we need to perform in order to get a sorted array? The answer is equal to the number of inversions in the array! Each inversion needs to bubble to its correct position and each 'swap' that we perform can fix at most 1 inversion.
Thus the number of swaps performed = number of inversions in the array.

<h1>Average Time Complexity of Bubble Sort</h1>
If we are given n numbers, we could generate $$n!$$ possible permutations of those numbers. Let $$S$$ denote the set of all possible inputs i.e. $$S$$ contains all of those $$n!$$ possible permutations of n numbers.

Consider an input $$I$$ and its reverse $$I_{r}$$. Our claim is that each pair of numbers (i,j) $$\epsilon$$ n contributes at most 1 inversion if we consider $$I$$ and $$I_{r}$$. What this is saying is that each pair of (i,j) can only be an inversion in either $$I$$ or its reverse denoted by $$I_{r}$$. 

By earlier discussion we know that number of swaps performed = number of inversions in the array.
So let us calculate the average number of inversions in $$S$$. <br>
Let total number of inversions be denoted by $$N_{I}$$, then<br>
<font size="4"> $$Average\:Number\:of\:Inversions\:=\:\frac{1}{n!}\Sigma_{I \epsilon S} N_{I}$$</font>

Calculating $$N_{I}$$: Since each pair $$(i,j)\:\epsilon\:n$$ contributes exactly 1 inversion in $$I$$ and $$I_{r}$$, the number of Inversions in $$I$$ and $$I_{r}$$ are at most = $$ n \choose 2$$ = $$\frac {n(n-1)}{2}$$.<br>

<font size="4"> $$Average\:Number\:of\:Inversions\:=\:\frac{1}{n!}\Sigma_{I \epsilon S} N_{I}$$
<br> $$=\:\frac{1}{n!}\Sigma_{I \epsilon S} \frac {n(n-1)}{2}$$ <br>
$$=\:\frac{1}{n!}\frac{n!}{2} \frac {n(n-1)}{2}$$ <br>
$$=\: \frac {n(n-1)}{4}$$ 
</font>

$$\therefore$$ the average number of inversions in $$I$$ and $$I_{r}$$ = $$\frac {n(n-1)}{4}\:=\:O(n^2)$$ <br>
Thus we can conclude that the average running time of Bubble Sort = $$O(n^2)$$

<h1>Insertion Sort</h1>
In the insertion sort algorithm we maintain 2 subarrays within the array we aim to sort. The subarray on the left hand side is the 'sorted' array and elements from the left subarray are inserted into their correct position in the right subarray. 

We start with our left array being only the first element, since 1 element is sorted trivially, and then traversing the left subarray to insert the elements in a sorted order (into the left subarray).

*[Note: Insertion sort algorithm sorts elements in-place i.e. no new copies of the arrays are made]*

Code for Insertion sort in Python:
{% highlight wl linenos %}
{% raw %}
def insertionSort(lst_nums):
    i = 0
    for i in range(1, len(lst_nums)):
        key = lst_nums[i]
        j = i - 1

        while(j>0 and lst_nums[j]>key):
            lst_nums[j+1] = lst_nums[j]
            j = j - 1
        lst_nums[j+1] = key 
    return lst_nums # sorted array
{% endraw %}
{% endhighlight %}

The for loop in line 3 runs from the second element (which is at index 2) to the last element. The 'key' is the element in the unsorted part of the array that we want to insert into the sorted array on the left. The inner while loop helps us determine the correct position of the 'key'. 

<h1>Time analysis of Insertion Sort</h1>
Simply by invoking loop rule we can see that due to the nested nature of for loops in the above code, the complexity of Insertion Sort is $$O(n^2)$$.

Another way to look at the time complexity is by looking at how many times line 8 is being executed in the worst case. 
Since we are assuming that we wish to sort the elements in an ascending order, the worst case would happen when the 'key' that we want to insert in the sorted left sub array is the smallest element and hence requires line 8 to be invoked 'i' times for key at position 'i' (starting from index i down to the first element since all elements in the sorted left subarray are greater than the key being inserted).

<font size="4">$$Worst\:Case\:Complexity\:=\:\Sigma_{i=1}^{n-1}i\:=\:\frac{(n-1)*n}{2}\:=\:\theta(n^2)$$</font> 

The average case complexity is found by looking at the average number of times line 8 (copying/swap mechanism) is being invoked. That is also $$\theta(n^2)$$. 

An interesting thing about insertion sort is that it runs in linear time i.e. $$O(n^2)$$ if the input array is almost sorted. What is meant by an almost sorted input? Turns out we can view this argument using the inversion analysis we carried out in the case of Bubble Sort.<br><br>
Look how each iteration of the while loop starting at line 7 can fix 1 inversion only. Basically the copying mechanism in line 8 is invoked if there is an inversion. So we can write the complexity of the full insertion sort code to be the sum of the outer for loop which runs for 'n' iterations (i.e. for all elements) and the number of inversions in the input array. This can be done because if the 'key' is not contributing to an inversion with respect to the left sub array, it means that the key is already in its right position, thus the while loop condition is not met and we skip lines 8-9. However, if there is an inversion, the while loop is invoked. <br><br>
In short, the time complexity of the code = $$O(n + number\:of\:inversions)$$<br><br>
The reason why we got $$O(n^2)$$ earlier was because in the worst case the number of inversions can be of the order $$O(n^2)$$. However, if the number of inversions are linear or $$O(n)$$ then we would get a total run time of the insertion sort algorithm as $$O(2n)$$, ignoring the constant, this is $$O(n)$$!

*Note: By the inversion argument, we can conclude that any algorithm that swaps adjacent elements will be lower bounded by $$n^2$$, i.e. $$\Omega(n^2)$$, on average.*

<h1>Selection Sort</h1>
Onto our final analysis of a sorting technique available to us in the space of quadratic time we have Selection Sort! 
Both Bubble Sort and Insertion Sort were swapping adjacent elements in order to eliminate inversions. Selection sort on the other hand, is going to swap elements that are far away from one another (they may be adjacent!). 

Intuition: You could implement Selection Sort in 2 ways, either by picking the maximum element or by picking the minimum element. For illustration purposes I will be picking the minimum element. So what do I mean by picking the minimum element? 

What we are essentially going to do is start with an empty sorted array on the left and our given unsorted input. *(Note: this unsorted array is imaginary, we are sorting 'in place' so the sorted array will be maintained within the input array at any given time)* 
Now we will run through all the elements in our unsorted array at any given time and find the minimum element among them. We then 'pick' or 'select' this minimum element and place it progressively in the sorted array. 

In short: Maintain a sorted left subarray and run a for loop to progressively find the minimum element in the unsorted right subarray. This element is going to be the 'next' element for the sorted left sub array. In this way, elements are being inserted into their right positions and will not be moved again once inserted in the left sorted sub array.

Code for Selection sort in Python:
{% highlight wl linenos %}
{% raw %}
def selectionSort(lst_nums):
    small = 0
    for i in range(len(lst_nums)):
        small = lst_nums[i]
        pos = i 
        for k in range(i+1, len(lst_nums)): # find the smallest element in the unsorted right subarray
            if lst_nums[k]<small:
                small = lst_nums[k]
                pos = k
                
        lst_nums[i], lst_nums[pos] = lst_nums[pos], lst_nums[i] 
    return lst_nums
{% endraw %}
{% endhighlight %}

<h1>Time Analysis of Selection Sort</h1>

We count the total number of element-element comparisons in this algorithm to get a sense of the time complexity. Think of it this way: when we start, we have no elements in the sorted left subarray so we essentially find the minimum element in an array of 'n' elements which is done in $$O(n)$$ time or n comparisons. The next iteration requires 1 less comparison, thus n-1 and so on. 

Total number of element-element comparisons = n + (n-1) + (n-2) + ...... 1 <br>
We can re-write this sum as = $$\Sigma_{i=1}^{n-1}i\:=\:\frac{(n-1)*n}{2}\:=\:\theta(n^2)$$

An advantage of selection sort over insertion sort is that although the time complexities are similar, selection sort will insert an element into its correct (final) position. So we can avoid repeated copying of elements that is performed by the insertion sort algorithm!

