---
title: Power of Four | LeetCode 342 | C
date: 2023-09-12 20:47:23
tags: [LeetCode, C, Math, Bit Manipulation, Recursion]
categories: LeetCode
---

Given an integer n, return true if it is a power of four. Otherwise, return false.

An integer n is a power of four, if there exists an integer x such that n == 4x.

Example 1:

```
Input: n = 16
Output: true
```

Example 2:

```
Input: n = 5
Output: false
```

Example 3:

```
Input: n = 1
Output: true
```

Constraints:

```
-231 <= n <= 231 - 1
```

Approach

```
If an integer is a power of four, only one bit is 1, others will be 0.
If an integer is a power of four, the only one bit is an even bit. 
```

Algorithm

```
Check if the bit is an even bit and make sure only one bit is 1.
```

Implementation

```
bool isPowerOfFour(int n){
    int shift = 0, bit = 0, count =0;
    while(n>0)
    {
        bit = n&1;
        if(bit){
            count++;
            if(shift%2!=0)
                return false;
            if(count!=1)
                return false;
        }
        n>>=1;
        shift++;
    }
    return ((shift-1)%2==0)?true:false;
}
```