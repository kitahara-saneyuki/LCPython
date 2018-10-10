# Matrix

## 1. 矩阵翻转操作

### 48. Rotate Image

You are given an n x n 2D matrix representing an image. Rotate the image by 90 degrees (clockwise).

顺时针旋转90度 = 逆时针转90度再水平翻转；逆时针转90度就是求转置矩阵

```java
public void rotate(int[][] matrix) {
    // transpose
    for (int i = 0; i<matrix.length; i++)
        for (int j = i; j<matrix[i].length; j++){
            int temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
        }
    // flip
    for (int i = 0; i<matrix.length; i++){
        for (int j = 0; j<matrix[i].length/2; j++){
            int temp = matrix[i][j];
            matrix[i][j] = matrix[i][matrix.length - 1 - j];
            matrix[i][matrix.length - 1 - j] = temp;
        }
    }
}
```

### 54. Spiral Matrix

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

这个题不要想太深，维持四个变量记录接下来的最大行数和列数，然后按顺序每计数完一行（列）就更新这四个变量即可。

```java
public List<Integer> spiralOrder(int[][] matrix) {
    List<Integer> res = new ArrayList<Integer>();
    if (matrix.length == 0)
        return res;
    int rowBegin = 0;
    int rowEnd = matrix.length-1;
    int colBegin = 0;
    int colEnd = matrix[0].length - 1;
    while (rowBegin <= rowEnd && colBegin <= colEnd) {
        for (int j = colBegin; j <= colEnd; j ++)
            res.add(matrix[rowBegin][j]);
        rowBegin++;
        for (int j = rowBegin; j <= rowEnd; j ++)
            res.add(matrix[j][colEnd]);
        colEnd--;
        if (rowBegin <= rowEnd)
            for (int j = colEnd; j >= colBegin; j --)
                res.add(matrix[rowEnd][j]);
        rowEnd--;
        if (colBegin <= colEnd)
            for (int j = rowEnd; j >= rowBegin; j --)
                res.add(matrix[j][colBegin]);
        colBegin++;
    }
    return res;
}
```

### 498. Diagonal Traverse

这个题目需要考虑清楚边界情况，靠边的时候一共是四种情况，不靠边反而只有两种

```py
def findDiagonalOrder(self, matrix):
    """
    :type matrix: List[List[int]]
    :rtype: List[int]
    """
    direction, x, y = True, 0, 0
    #True means upper-right, vice versa
    if len(matrix) == 0:
        return []
    h, w = len(matrix), len(matrix[0])
    ret = []
    while x < w and y < h:
        ret.append(matrix[y][x])
        if y == 0 and direction == True and x != w - 1:
            x += 1
            direction = False
        elif x == 0 and direction == False and y != h - 1:
            y += 1
            direction = True
        elif x == w - 1 and direction == True:
            y += 1
            direction = False
        elif y == h - 1 and direction == False:
            x += 1
            direction = True
        else:
            if direction:
                x += 1
                y -= 1
            else:
                x -= 1
                y += 1
    return ret
```
