---
title: Degree of an Array | LeetCode 697 | C
date: 2023-09-10 22:02:23
tags: [LeetCode, C, Array, Hash Table]
categories: LeetCode
---

Given a non-empty array of non-negative integers nums, the degree of this array is defined as the maximum frequency of any one of its elements.

Your task is to find the smallest possible length of a (contiguous) subarray of nums, that has the same degree as nums.

Example 1:

```
Input: nums = [1,2,2,3,1]
Output: 2
Explanation: 
The input array has a degree of 2 because both elements 1 and 2 appear twice.
Of the subarrays that have the same degree:
[1, 2, 2, 3, 1], [1, 2, 2, 3], [2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2]
The shortest length is 2. So return 2.
```

Example 2:

```
Input: nums = [1,2,2,3,1,4,2]
Output: 6
Explanation: 
The degree is 3 because the element 2 is repeated 3 times.
So [2,2,3,1,4,2] is the shortest subarray, therefore returning 6.
``` 

Constraints:

```
nums.length will be between 1 and 50,000.
nums[i] will be an integer between 0 and 49,999.
```

Approach

```
Memorise where the element first appears and last apears and how many times the element appears. Find smallest possible length of a subarray by going through the hash table again.
```

Algorithm

```
1. Go through nums to find where the element first appears and last apears and how many times the element appears.
2. Go through the hash table to find the element appears the most.
3. If two elements appear with the same times, keep the subarray with the smallest length.
```

Implementation

```
int findShortestSubArray(int* nums, int numsSize){
    int hashtable[50000][3] = {0};
    int length = 50000, degree = 1;
    for(int i = 0; i < numsSize; i++)
    {
        if(hashtable[nums[i]][0]>0){
            hashtable[nums[i]][1] = i + 1;
            hashtable[nums[i]][2]++;
        }
        else{
            hashtable[nums[i]][0] = i + 1;
            hashtable[nums[i]][2]++;
        }
    }
    for(int i = 0; i < 50000; i++){
        if(hashtable[i][2] > degree){
            length = hashtable[i][1] - hashtable[i][0] + 1;
            degree = hashtable[i][2];
        }else if(hashtable[i][2] == degree && (hashtable[i][1] - hashtable[i][0] + 1) < length)
        {
            length = hashtable[i][1] - hashtable[i][0] + 1;
            degree = hashtable[i][2];
        }
    }
    return length>0?length:1;
}
```
