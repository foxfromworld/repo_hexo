---
title: Minimum Penalty for a Shop | LeetCode 2483 | C
date: 2023-09-02 21:52:42
tags: [LeetCode, C, String, Prefix Sum]
categories: LeetCode
---

You are given the customer visit log of a shop represented by a 0-indexed string customers consisting only of characters 'N' and 'Y':

if the ith character is 'Y', it means that customers come at the ith hour
whereas 'N' indicates that no customers come at the ith hour.
If the shop closes at the jth hour (0 <= j <= n), the penalty is calculated as follows:

For every hour when the shop is open and no customers come, the penalty increases by 1.
For every hour when the shop is closed and customers come, the penalty increases by 1.
Return the earliest hour at which the shop must be closed to incur a minimum penalty.

Note that if a shop closes at the jth hour, it means the shop is closed at the hour j.

Example 1:

```
Input: customers = "YYNY"
Output: 2
Explanation: 
- Closing the shop at the 0th hour incurs in 1+1+0+1 = 3 penalty.
- Closing the shop at the 1st hour incurs in 0+1+0+1 = 2 penalty.
- Closing the shop at the 2nd hour incurs in 0+0+0+1 = 1 penalty.
- Closing the shop at the 3rd hour incurs in 0+0+1+1 = 2 penalty.
- Closing the shop at the 4th hour incurs in 0+0+1+0 = 1 penalty.
Closing the shop at 2nd or 4th hour gives a minimum penalty. Since 2 is earlier, the optimal closing time is 2.

Example 2:

```
Input: customers = "NNNNN"
Output: 0
Explanation: It is best to close the shop at the 0th hour as no customers arrive.
```

Example 3:

```
Input: customers = "YYYY"
Output: 4
Explanation: It is best to close the shop at the 4th hour as customers arrive at each hour.
```

Constraints:

```
1 <= customers.length <= 105
customers consists only of characters 'Y' and 'N'.
```

Approach

```
The earliest hour with the minimum penalty can be determined by the appearance of "Y" and "N".
When the "Y" appears, the penalty should decrease. That means when the customer arrive, the shop is still open.
On the contray, when the shop is open and customers didn't come, the penalty should inscrease.
```

Algorithm

```
1. If the letter is "Y", decrease penalty by 1. Otherwise, increase penalty by 1.
2. If the penalty is negative, save i + 1 as the earliest_hour.
```

Implementation

```
int bestClosingTime(char * customers){
    int penalty = 0, earliest_hour = 0, len = strlen(customers);
    for(int i=0; i<len;i++){
        if(customers[i]=='Y') penalty--;
        else penalty++;
        if(penalty<0){
            penalty = 0;
            earliest_hour = i+1;
        }
    }
    return earliest_hour;
}
```
