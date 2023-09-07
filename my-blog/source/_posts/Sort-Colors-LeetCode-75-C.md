---
title: Sort Colors | LeetCode 75 | C
date: 2023-09-07 10:23:22
tags: [LeetCode, C, Array, Two Pointers, Sorting]
categories: LeetCode
---

Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

Example 1:

```
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

Example 2:

```
Input: nums = [2,0,1]
Output: [0,1,2]
``` 

Constraints:

```
n == nums.length
1 <= n <= 300
nums[i] is either 0, 1, or 2.
```

Approach

```
Use two pointers to keep 0 and 2 at the beginning and the end of the array.
```

Algorithm

```
1. Go through the list. If encounter 2, swap the current element and the right element. Move the right pointer to the left.
2. If encounter 2, swap the current element and the left element. Move the left pointer to the right. Mover the current pointer to the right too.
3. If the current element is neither 0 nor 2, move the current pointer to the right only.
```

Implementation

```
void swap(int* nums, int x, int y) {
    int temp = nums[x];
    nums[x] = nums[y];
    nums[y] = temp;
}
void sortColors(int* nums, int numsSize){
    int left = 0, right = numsSize - 1, curr = 0;
    int temp;
    while(curr<=right){
        if(nums[curr] == 0)
        {
            swap(nums, left, curr);
            curr++;
            left++;
        }
        else if (nums[curr] == 2)
        {
            swap(nums, right, curr);       
            right--;
        }
        else
            curr++;
    }
}
```