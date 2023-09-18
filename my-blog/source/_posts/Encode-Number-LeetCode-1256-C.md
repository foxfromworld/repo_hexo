---
title: Encode Number | LeetCode 1256  | C
date: 2023-09-18 16:38:01
tags: [LeetCode, C, Math, String, Bit Manipulation]
categories: LeetCode
---

Given a non-negative integer num, Return its encoding string.

The encoding is done by converting the integer to a string using a secret function that you should deduce from the following table:

![](encode_number.png)

Example 1:

```
Input: num = 23
Output: "1000"
```

Example 2:

```
Input: num = 107
Output: "101100"
``` 

Constraints:

```
0 <= num <= 10^9
```

Approach

```
Follow the rule of encoding, we can find the lenght of the output increase by one bit after increase the number by the power of 2. So when the number is 23, we can calculate the lenght of the result by the formula 1 (+1bit) + 2 (+1bit) + 4 (+1bit) + 8 (+1bit). 
```

Algorithm

```
1. Find the largest sum of power of 2 which is smaller than num.
2. We can get bit and allocate the space for the result array.
3. Fill the array with the bits of difference between temp and num.
4. Fill the beginning '0's.
```

Implementation

```
char * encode(int num){
    if(num == 0)  return "";
    else if (num == 1)  return "0";
    else if (num ==2)  return "1";
    int base = 1, bit = 1, temp = 0;
    while((temp+base) <= num){
        temp += base;
        base *= 2;
        bit +=1 ;
    }
    char *result = malloc(bit*sizeof(char));
    result[bit-1] = '\0';
    temp = num-temp;
    bit = bit-1;
    if(temp == 0){
        for(int i = 0;i<bit;i++)
        {
            result[i] = '0';
        }
    }
    while(temp>0){
        result[bit-1] = (temp & 1)+'0';
        temp >>=1;
        bit--;
    }
    while(bit>0)
    {
      result[--bit] = (temp & 1)+'0';
      temp >>=1;
    }
    return result;
}
```

![](screenshot.PNG)