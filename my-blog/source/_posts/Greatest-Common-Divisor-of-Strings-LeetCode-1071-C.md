---
title: Greatest Common Divisor of Strings | LeetCode 1071 | C
date: 2023-09-01 17:07:32
tags: [LeetCode, C, String, Recursion]
categories: LeetCode
---

For two strings s and t, we say "t divides s" if and only if s = t + ... + t (i.e., t is concatenated with itself one or more times).

Given two strings str1 and str2, return the largest string x such that x divides both str1 and str2.

Example 1:

```
Input: str1 = "ABCABC", str2 = "ABC"
Output: "ABC"
```

Example 2:

```
Input: str1 = "ABABAB", str2 = "ABAB"
Output: "AB"
```

Example 3:

```
Input: str1 = "LEET", str2 = "CODE"
Output: ""
```

Constraints:

```
1 <= str1.length, str2.length <= 1000
str1 and str2 consist of English uppercase letters.
```

Approach

```
Use recursion to go thourh the longer arrray with the shorter array.
```

Algorithm

```
1. If the first letters of both are not the same, they don't have the common substring.
2. If the length of string1 is shorter than string2, swap the strings.
3. If string1 + string2 is not equal to string2 + string1, return "".
4. If string1 and string2 have the common substring, the new substring (string1 but starts from the length of string2) and string2 should have the common substring.
5. Repeat the process until the substring is found.
```

Implementation

```
char * gcdOfStrings(char * str1, char * str2){
    if(str1[0] != str2[0])
        return "";
    int len1 = strlen(str1), len2 = strlen(str2);
    char *combine1 = malloc((len1 + len2 + 1)*sizeof(char));
    char *combine2 = malloc((len1 + len2 + 1)*sizeof(char));
    strcpy(combine1, str1);strcat(combine1, str2);
    strcpy(combine2, str2);strcat(combine2, str1);
    if(strcmp(combine1, combine2))
        return "";
    if(len1 < len2)
        return gcdOfStrings(str2, str1);        
    if(!strcmp(str1, str2))
        return str1;
    return gcdOfStrings(str1 + len2, str2);
}
```