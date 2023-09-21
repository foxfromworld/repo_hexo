---
title: Reverse String II | LeetCode 541  | C
date: 2023-09-21 22:05:41
tags: [LeetCode, C, Two Pointers, String]
categories: LeetCode
---

Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.

If there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original.

Example 1:

```
Input: s = "abcdefg", k = 2
Output: "bacdfeg"
```

Example 2:

```
Input: s = "abcd", k = 2
Output: "bacd"
```

Constraints:

```
1 <= s.length <= 104
s consists of only lowercase English letters.
1 <= k <= 104
```

Approach

```
Use two pointers to reverse substring every 2k.
```

Algorithm

```
1. Go through the list
2. Reverse k characters every 2k.
3. Always check if the right pointer exceeds the lenght-1.
```

Implementation

```
char * reverseStr(char * s, int k){
  int gap = 2*k;
  int left, right, len = strlen(s);
  char c = '\0';
  for(int i = 0;i<len;i+=gap)
  {
    left = i;
    right = (i+k<=len-1)?(i+k-1):(len-1);
    while(left<right){
      c = s[left];
      s[left] = s[right];
      s[right] = c;
      left++;
      right--;
    }
  }
  return s;
}
```