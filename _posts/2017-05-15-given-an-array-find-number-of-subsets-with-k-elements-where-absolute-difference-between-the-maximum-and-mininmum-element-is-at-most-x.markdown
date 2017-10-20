---
layout: post
title:  Given an array, find number of subsets with k elements, where absolute difference between the maximum and mininmum element is at most x
date:   2017-05-15 16:49:21 +0000
---


## Problem

Given an Array consisting of N integers, we need to find the number of subsets of this Array of size K, where Absolute difference between the Maximum and Minimum element of the subset is at most X.

<!--more-->
## Explanation
Lets say given Array is `[4 5 1 3 2]` and `K=3` and `X=5`      

number of subsets satisfying given conditions will be `10`      

One of the subset is `[1 2 5]` having K elements and absolute difference between minimum and maximum element
less then X i.e `5-1<X`

## Solution

This problem comes under easy-medium level.                  
Formally a k-combination of a set S is a subset of k distinct elements of S

1. First sort the Array       
`[1 2 3 4 5]`

- Fix the first element.

- Then traverse the array, counting elements whose  difference with fixed element is less than or equal to X.

- Calculate K-1 combinations of (counted elements - fixed element's index), if (counted elements - fixed element's index) is greater then `k-1` .     
 `K-1` because one element is fixed.

- Fix the next element and repeat from step 3.

- Repeat above step `length(array)-1` times.

## Psuedo code

{% highlight python %}
# this function calulates r combinations of n elements
def ncr(n,r):
end

arr=given_array;pointer=0;count=0;answer=0
arr=sort(arr)
N=length(arr)
while(pointer<N):
  while(count<N and arr[count]-arr[pointer]<=X):
    count++
  count--
  if (count-pointer>=K):
    answer+=ncr(count-pointer,K)
  pointer++
print answer    

{% endhighlight %}

## For large arrays using modulo
For arrays small than 20 elemets we can find combinations directly
`nCr = n! / (r! * (n-r)!)`

For arrays large than 20 elements finding combinations goes out of integer limit. So we have to calculate nCr modulo M       

If we have to calcuate nCr mod p(where p is a prime), we can calculate factorial mod p and then use modular inverse to find nCr mod p. If we have to find nCr mod m(where m is not prime), we can factorize m into primes and then use Chinese Remainder Theorem(CRT) to find nCr mod m.

For more info on calculating nCr for large numbers
- [All nCr calculation methods](https://comeoncodeon.wordpress.com/category/algorithm/){:target="_blank"}
