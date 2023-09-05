---
title: Minimum Size Subarray Sum | LeetCode 209 | C
date: 2023-09-04 22:06:43
tags: [LeetCode, C, Array, Sliding Window]
categories: LeetCode
---

Given an array of positive integers nums and a positive integer target, return the minimal length of a 
subarray whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.

Example 1:

```
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
```

Example 2:

```
Input: target = 4, nums = [1,4,4]
Output: 1
```

Example 3:

```
Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0
```

Constraints:

```
1 <= target <= 109
1 <= nums.length <= 105
1 <= nums[i] <= 104
```

Approach

```
Use sliding window to find the subarray.
```

Algorithm

```
1. Add the integers up until the sum is greater than or equal to target.
2. Memorise the lenght of the subarray.
3. Aubtract the current value of nums[start].
4. Repeat the above steps.
```

Implementation

```
int minSubArrayLen(int target, int* nums, int numsSize){
    int sum = 0, start = 0, length = INT_MAX;
    for(int i = 0; i < numsSize; i++)
    {
        sum += nums[i];
        while(sum>=target){
            if (i-start+1 < length)
                length = i-start+1;  
            sum-=nums[start];
            start++;
        }      
    }
    return (length == INT_MAX)?0:length;
}
```