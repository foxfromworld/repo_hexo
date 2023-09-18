---
title: Maximum Average Subarray I | LeetCode 643  | C
date: 2023-09-15 16:35:43
tags: [LeetCode, C, Array, Sliding Window]
categories: LeetCode
---
You are given an integer array nums consisting of n elements, and an integer k.

Find a contiguous subarray whose length is equal to k that has the maximum average value and return this value. Any answer with a calculation error less than 10-5 will be accepted.

Example 1:

```
Input: nums = [1,12,-5,-6,50,3], k = 4
Output: 12.75000
Explanation: Maximum average is (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75
```

Example 2:

```
Input: nums = [5], k = 1
Output: 5.00000
```

Constraints:

```
n == nums.length
1 <= k <= n <= 105
-104 <= nums[i] <= 104
```

Approach

```
Calculate the average of every k elements and find the max value.
```

Algorithm

```
Go through the list with a sliding window of size k and keep the max value.
```

Implementation

```
#include <float.h>

double findMaxAverage(int* nums, int numsSize, int k){
  int sum = 0, index = 0;
  double result = -DBL_MAX, temp = 0;
  if(numsSize==1)
    return nums[0];
  for(int i = 0; i<numsSize; i++){
    sum += nums[i];
    if(i>=k-1){
      temp = (double)sum/k;
      result =  temp > result?temp:result;
      sum -= nums[index];
      index++;
    }
  }
  return result;
}
```