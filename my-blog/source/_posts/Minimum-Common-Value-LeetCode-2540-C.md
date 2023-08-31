---
title: Minimum Common Value | LeetCode 2540 | C
date: 2023-08-31 22:27:30
tags: [LeetCode, C, Array, Two Pointers]
categories: LeetCode
---

Given two integer arrays nums1 and nums2, sorted in non-decreasing order, return the minimum integer common to both arrays. If there is no common integer amongst nums1 and nums2, return -1.

Note that an integer is said to be common to nums1 and nums2 if both arrays have at least one occurrence of that integer.

Example 1:

```
Input: nums1 = [1,2,3], nums2 = [2,4]
Output: 2
Explanation: The smallest element common to both arrays is 2, so we return 2.
```

Example 2:

```
Input: nums1 = [1,2,3,6], nums2 = [2,3,4,5]
Output: 2
Explanation: There are two common elements in the array 2 and 3 out of which 2 is the smallest, so 2 is returned.
```

Constraints:

```
1 <= nums1.length, nums2.length <= 105
1 <= nums1[i], nums2[j] <= 109
Both nums1 and nums2 are sorted in non-decreasing order.
```

Approach

```
Use the two pointers to go through both lists.
```

Algorithm

```
1. Incresse the index1 if the current value of nums2 is larger. 
2. Increase the index2 if the current value of nums1 is larger.
3. If the values are the same, return the value. Otherwise, return -1.
```

Implementation

```
int getCommon(int* nums1, int nums1Size, int* nums2, int nums2Size){
    int index1 = 0;
    int index2 = 0;
    while(index1<nums1Size &&index2<nums2Size){
        if(nums1[index1] > nums2[index2])
            index2++;
        else if (nums1[index1] < nums2[index2])
            index1++;
        else
            return nums1[index1];
    }
    return -1;
}
```