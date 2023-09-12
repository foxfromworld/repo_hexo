---
title: Matrix Diagonal Sum | LeetCode 1572 | C
date: 2023-09-08 21:07:08
tags: [LeetCode, C, Array, Matrix]
categories: LeetCode
---

Given a square matrix mat, return the sum of the matrix diagonals.

Only include the sum of all the elements on the primary diagonal and all the elements on the secondary diagonal that are not part of the primary diagonal.

Example 1:

![](sample_1911.png)

```
Input: mat = [[1,2,3],
              [4,5,6],
              [7,8,9]]
Output: 25
Explanation: Diagonals sum: 1 + 5 + 9 + 3 + 7 = 25
Notice that element mat[1][1] = 5 is counted only once.
```

Example 2:

```
Input: mat = [[1,1,1,1],
              [1,1,1,1],
              [1,1,1,1],
              [1,1,1,1]]
Output: 8
```

Example 3:

```
Input: mat = [[5]]
Output: 5
``` 

Constraints:

```
n == mat.length == mat[i].length
1 <= n <= 100
1 <= mat[i][j] <= 100
```

Approach

```
Collect the sum of the primary and the secondary diagonals. Subtract the reapeatedly added center element if the matSize is odd.
```

Algorithm

```
1. Go through the matrix from the first column to the last column.
2. subtract the repeatedly added value.
```

Implementation

```
int diagonalSum(int** mat, int matSize, int* matColSize){
    int sum = 0;
    for(int i;i<matSize;i++)
    {
        sum += mat[i][i];
        sum += mat[i][matSize-i-1];
    }
    if((*matColSize % 2)!=0){
        sum -= mat[*matColSize/2][matSize/2];
    }
    return sum;
}
```