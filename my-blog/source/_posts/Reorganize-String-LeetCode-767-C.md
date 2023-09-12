---
title: Reorganize String | LeetCode 767  | C
date: 2023-09-12 21:12:05
tags: [LeetCode, C, Hash Table, String, Greedy, Sorting, Heap (Priority Queue), Counting]
categories: LeetCode
---

Given a string s, rearrange the characters of s so that any two adjacent characters are not the same.

Return any possible rearrangement of s or return "" if not possible.

Example 1:

```
Input: s = "aab"
Output: "aba"
```

Example 2:

```
Input: s = "aaab"
Output: ""
```

Constraints:

```
1 <= s.length <= 500
s consists of lowercase English letters.
```

Approach

```
Find the char with the highest fequency. Fill the string with the char every 2 indixes. Fill the rest of the chars.
```

Algorithm

```
1. Count the frequency of each char and find the char with the highest frequency.
2. Return "" if the frequency is too high because it's possible that two adjacent characters will be the same.
3. Fill the string with the char every 2 indixes.
4. Similarly, fill the rest of the chars.
```

Implementation

```
char * reorganizeString(char * s){
  int hashTable[26] = {0};
  int len = strlen(s), max = 0, index = 0, j = 0, p = 0;
  char *result = malloc((len+1)*sizeof(char));
  result[len] = '\0';

  for(int i = 0; i<len;i++)
  {
    j = s[i]-'a';
    hashTable[j]++;
    if(hashTable[j]>max){
      max = hashTable[j];
      index = j;
    }
  }
  if(max > (len+1)/2)
    return "";
  while(hashTable[index]>0){
    result[p] = index + 'a';
    hashTable[index]--;
    p+=2;
    if (p >= len)
      p = 1;
  }
  for(j = 0; j< 26;j++){
    while(hashTable[j]>0){
      hashTable[j]--;
      result[p] = j + 'a';
      p+=2;
      if (p >= len)
        p = 1;
    }
  }
  return result;
}
```