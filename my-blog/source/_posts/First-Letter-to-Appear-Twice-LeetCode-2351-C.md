---
title: First Letter to Appear Twice | LeetCode 2351 | C
date: 2023-08-30 10:52:35
tags: [LeetCode, C, Counting]
categories: LeetCode
---

Given a string s consisting of lowercase English letters, return the first letter to appear twice.

Note:

A letter a appears twice before another letter b if the second occurrence of a is before the second occurrence of b.
s will contain at least one letter that appears twice.
 

Example 1:

```
Input: s = "abccbaacz"
Output: "c"
Explanation:
The letter 'a' appears on the indexes 0, 5 and 6.
The letter 'b' appears on the indexes 1 and 4.
The letter 'c' appears on the indexes 2, 3 and 7.
The letter 'z' appears on the index 8.
The letter 'c' is the first letter to appear twice, because out of all the letters the index of its second occurrence is the smallest.
```

Example 2:

```
Input: s = "abcdd"
Output: "d"
Explanation:
The only letter that appears twice is 'd' so we return 'd'.
```

Constraints:

```
2 <= s.length <= 100
s consists of lowercase English letters.
s has at least one repeated letter.
```

Approach

```
Create a array for counting. When the letter appears, increase the value of the counter by 1. If the value is 2, return the letter.
```

Algorithm

```
1. Create an array.
2. Use the index to find the corresponding counter.
3. Check if the value of the counter is 2.
```

Implementation

```
char repeatedCharacter(char * s){
    int count[26] = {0};
    int index = 0;
    int i=0;
    for(i=0;i<strlen(s);i++)
    {
        index = s[i]-'a';
        count[index]++;
        if(count[index] == 2)
            break;
    }
    return s[i];
}
```