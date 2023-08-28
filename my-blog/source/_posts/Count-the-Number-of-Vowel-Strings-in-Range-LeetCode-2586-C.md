---
title: Count the Number of Vowel Strings in Range | LeetCode 2586 | C
date: 2023-08-28 16:39:27
tags: [LeetCode, C, String]
categories: LeetCode
---

You are given a 0-indexed array of string words and two integers left and right.

A string is called a vowel string if it starts with a vowel character and ends with a vowel character where vowel characters are 'a', 'e', 'i', 'o', and 'u'.

Return the number of vowel strings words[i] where i belongs to the inclusive range [left, right].

Example 1:

```
Input: words = ["are","amy","u"], left = 0, right = 2
Output: 2
Explanation: 
- "are" is a vowel string because it starts with 'a' and ends with 'e'.
- "amy" is not a vowel string because it does not end with a vowel.
- "u" is a vowel string because it starts with 'u' and ends with 'u'.
The number of vowel strings in the mentioned range is 2.
```

Example 2:

```
Input: words = ["hey","aeo","mu","ooo","artro"], left = 1, right = 4
Output: 3
Explanation: 
- "aeo" is a vowel string because it starts with 'a' and ends with 'o'.
- "mu" is not a vowel string because it does not start with a vowel.
- "ooo" is a vowel string because it starts with 'o' and ends with 'o'.
- "artro" is a vowel string because it starts with 'a' and ends with 'o'.
The number of vowel strings in the mentioned range is 3.
```

Constraints:

```
1 <= words.length <= 1000
1 <= words[i].length <= 10
words[i] consists of only lowercase English letters.
0 <= left <= right < words.length
```

Approach

```
Just determine if a string starts with and ends with are vowel characters.
```

Algorithm

```
Go through the list within the inclusive range.
Get the length of the string to find the index of the last letter.
Check the first letter and the last letter.
If they both are vowel characters, increase the counter.
```

Implementation

```
int vowelStrings(char ** words, int wordsSize, int left, int right){
    int isVowel = 0;
    int len = 0;
    char start;
    char end;
    for(int i = left; i<right+1 ; i++)
    {
        len = strlen(words[i]);
        start = words[i][0];
        end = words[i][len-1];
        if ((start == 'a'||start == 'e'||start == 'i'||start == 'o'||start == 'u') &&
            (end == 'a'||end == 'e'||end == 'i'||end == 'o'||end == 'u'))
            isVowel++;
    }
    return isVowel;
}
```