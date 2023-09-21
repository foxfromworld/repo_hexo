---
title: Minimum Recolors to Get K Consecutive Black Blocks | LeetCode 2379  | C
date: 2023-09-19 15:43:17
tags: [LeetCode, C, String, Sliding Window]
categories: LeetCode
---

You are given a 0-indexed string blocks of length n, where blocks[i] is either 'W' or 'B', representing the color of the ith block. The characters 'W' and 'B' denote the colors white and black, respectively.

You are also given an integer k, which is the desired number of consecutive black blocks.

In one operation, you can recolor a white block such that it becomes a black block.

Return the minimum number of operations needed such that there is at least one occurrence of k consecutive black blocks.

Example 1:

```
Input: blocks = "WBBWWBBWBW", k = 7
Output: 3
Explanation:
One way to achieve 7 consecutive black blocks is to recolor the 0th, 3rd, and 4th blocks
so that blocks = "BBBBBBBWBW". 
It can be shown that there is no way to achieve 7 consecutive black blocks in less than 3 operations.
Therefore, we return 3.
```

Example 2:

```
Input: blocks = "WBWBBBW", k = 2
Output: 0
Explanation:
No changes need to be made, since 2 consecutive black blocks already exist.
Therefore, we return 0.
``` 

Constraints:

```
n == blocks.length
1 <= n <= 100
blocks[i] is either 'W' or 'B'.
1 <= k <= n
```

Approach

```
Use the sliding window to keep the count of 'W'.
```

Algorithm

```
Go throught the list and count the occurence of 'W'. Find the minimun count in each window of the lenght of k.
```

Implementation

```
int minimumRecolors(char * blocks, int k){
    int occur = 0, result = strlen(blocks), len = result, idx = 0;
    for(int i = 0; i < len; i++){
        if(i >= k)
        {
            if(occur < result)
                result = occur;
            if(blocks[idx] == 'W')
                occur--;
            idx++;
        }
        if((blocks[i]) == 'W')
            occur++;
    }
    if(occur < result)
        result = occur;
    return (len == k)?occur:result;
}
```