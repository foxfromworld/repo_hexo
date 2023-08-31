---
title: Number of Even and Odd Bits | LeetCode 2595 | C
date: 2023-08-30 11:57:57
tags: [LeetCode, C, Bit Manipulation]
categories: LeetCode
---

You are given a positive integer n.

Let even denote the number of even indices in the binary representation of n (0-indexed) with value 1.

Let odd denote the number of odd indices in the binary representation of n (0-indexed) with value 1.

Return an integer array answer where answer = [even, odd].

Example 1:

```
Input: n = 17
Output: [2,0]
Explanation: The binary representation of 17 is 10001. 
It contains 1 on the 0th and 4th indices. 
There are 2 even and 0 odd indices.
```

Example 2:

```
Input: n = 2
Output: [0,1]
Explanation: The binary representation of 2 is 10.
It contains 1 on the 1st index. 
There are 0 even and 1 odd indices.
```

Constraints:

```
1 <= n <= 1000
```

Approach

```
Use bitwise operation to get the specific bit.
```

Algorithm

```
1. Get the bit by the "AND" operation.
2. Shift the bit out.
3. Increase the counter.
4. Repeat until the number is eaqul or smaller than 0.
```

Implementation

```
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* evenOddBit(int n, int* returnSize){
  int *result = calloc(2, sizeof(int));
  int index = 0;
  while(n>0)
  {
    if(n & 1==1)
    {
      result[index%2]++;
    }
    n = n>>1;
    index++;
  }
  *returnSize = 2;
  return result;
}
```