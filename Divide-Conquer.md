# Divide and Conquer

## 各种怪题

### 493. Reverse Pairs

这题目太离谱了，居然连BST都会超时，可以算leetcode上最难最扯淡的几个题目了。数组树太麻烦了，咱用简单算法

使用合并排序的思想，学名叫分割重现关系(Partition Recurrence Relation)，用式子表示是T(i, j) = T(i, m) + T(m+1, j) + C。这里的C就是处理合并两个部分的子问题，用文字来描述就是“已知翻转对的两个数字分别在子数组nums[i, m]和nums[m+1, j]之中，求满足要求的翻转对的个数”

在合并排序的递归函数中，对于有序的两个子数组进行统计翻转对的个数，然后再逐层返回，这就实现了上述的分割重现关系的思想。

```py
def __init__(self):
    self.cnt = 0
def reversePairs(self, nums):
    def msort(lst):
        # merge sort body
        L = len(lst)
        if L <= 1:                          # base case
            return lst
        else:                               # recursive case
            return merger(msort(lst[:int(L/2)]), msort(lst[int(L/2):]))
    def merger(left, right):
        # merger
        l, r = 0, 0                         # increase l and r iteratively
        while l < len(left) and r < len(right):
            if left[l] <= 2*right[r]:
                l += 1
            else:
                self.cnt += len(left)-l     # add here
                r += 1
        return sorted(left+right)           # I can't avoid TLE without timsort...

    msort(nums)
    return self.cnt
```

### 241. Different Ways to Add Parentheses

这题目看代码就好，讲解也讲不明白……实际上是个简单的分治

```py
def diffWaysToCompute(self, input):
    res = []
    for i in range(0, len(input)):
        c = input[i]
        if c == '+' or c == '-' or c == '*':
            a, b = input[0:i], input[i+1:]
            al, bl = self.diffWaysToCompute(a), self.diffWaysToCompute(b)
            for x in al:
                for y in bl:
                    if c == '-':
                        res.append(x-y)
                    elif c == '+':
                        res.append(x+y)
                    elif c == '*':
                        res.append(x*y)
    if len(res) == 0:
        res.append(int(input))
    return res
```
