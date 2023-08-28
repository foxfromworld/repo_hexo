---
title: Excel Sheet Column Title | LeetCode 168 | C
date: 2023-08-24 13:34:03
tags: [LeetCode, C, String]
categories: LeetCode
---

Given an integer columnNumber, return its corresponding column title as it appears in an Excel sheet.

For example:

```
A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28 
...
```

Example 1:
```
Input: columnNumber = 1
Output: "A"
```
Example 2:
```
Input: columnNumber = 28
Output: "AB"
```
Example 3:
```
Input: columnNumber = 701
Output: "ZY"
```

Constraints:

```
1 <= columnNumber <= 231 - 1
```

Approach

The mapping should be like this.
```
A B C D E F G H I J K  L  M  N  O  P  Q  R  S  T  U  V  W  X  Y  Z
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
```

```
Take 701 for example, it can be calculate by the formula: (25 + 1) * 26^1 + (24 + 1) * 26^0 ((Z + 1) * 26^1 + (Y + 1)*26^0).
```

Algorithm

```
1. Initialize  the length as 1 for putting the null character '\0' at the end of the srting.
2. For C language, we need to allocate memory for the string, so we need to find the length of the required memory.
3. Start getting the letter by the formula and the mapping.
```

Implementation

```
char * convertToTitle(int columnNumber){
    int number = columnNumber;
    int length = 1; // Initialize the length as 1
    while (number > 0){
        number = (number-1)/26;
        length++;
    }
    char *title = malloc(length * sizeof(char)); // Allocate the memory

    title[--length] = '\0';
    
    while(columnNumber>0)
    {
        title[--length] = 'A' + ((columnNumber-1)%26); // Map the value to the letter
        columnNumber = (columnNumber-1)/26;
    }
    return title;
}
```