# Personal-Notes

## 一些套路

### 既有题目思路

1. 不贪图运行时间最快，但算法复杂度需要尽可能低
2. 思路要易于理解，代码要尽可能短，每条思路所对应的代码最好要形成模板

### 新题套路

1. Problem Solving：把新题解释成既有套路的过程
    1. 遇到没思路的新题先举栗子找规律
2. Code Writing：熟练掌握既有套路

### 面试技巧

1. 当你面试时，你在白板上写，写完之后，面试官很可能就立刻开始给你指bug了，你这时有的bug，都算bug！所以，在写完最后一句话前，最好做个大停顿，过一下之前写的，快速检查下。当然你嘴上可以给面试官解释你现在是在做最终检查，不是说卡住不会了。
2. 最好不要说完思路就动笔就写，需要思考不同的解法，并与面试官交流明确：
    1. 要熟悉刷题网站提供的标准解法
    2. 要准备一个面试友好的解法
    3. 要准备时间空间权衡的分析：有的解法可能时间复杂度不高，但空间复杂度很不错

### 面试流程

1. 问题分析
2. 交流阶段：厘清各种条件
3. 提出各种方案，满足面试官要求
4. 如果方案不能再规定时间内写完，与面试官交流选定一个方案
5. coding
6. test & debug
    1. 考虑corner case，做各种assumption
7. follow up: doc, unit test, regression test, performance tuning, benchmarking

## DP

简而言之 DP有六部曲 个人建议面试时写在白板上 清楚明了 一步都不能少 基本上你写出这些 implement起来也非常简单了

1. 定义：dp[j]表示什么含义，比如largest subarray sum ending at arr, and must include arr. 注意语言描述, 包括还是不包括arr/matrix[j]
2. 归纳法则：dp 的 dependency 是怎么样的，依赖于dp[i-1] 还是 dp[i+1] 还是 dp[k] for all k < i or all k > i 等等，试着过几个小例子推导一下
3. 初始态：往往是dp[0]，二维往往是第一行，第一列，也就是dp[0], dp[0][j], dp[i][0]
4. 结果：往往的dp[n], max(dp) 等等, 从definition 出发
5. 填充顺序：从induction rule 的 dependency出发 判断的从左到右 还是 从左上到右下
6. 优化: 分为时间和空间两方面。
    1. 时间的比较难，因为往往需要你重新define dp state 和 induction rule。
    2. 空间比较简单，可以根据induction rule看出来，比如斐波那契数列: dp = dp[i - 1] + dp[i - 2], 那么dp 只依赖于前两个元素，就不需要create 整个 dp array，两个variable即可，空间可以从O(n)优化到O(1)。

最后, 多总题多总结多积累小tips，熟能生巧后dp其实是非常简单，也非常有套路的，一些induction rule 的常见pattern 你一眼就能看出来了。

## String基本操作

```py
s2 = "shaunwei"
s2[-3:] = "wei"
s2[5:8] = "wei"
s2.index('w') = 5  # if not found, return -1
```

## 链表

链表的技巧不多，主要是记忆操作顺序太繁琐，现想其实也是有时间的。

1. 翻转链表
2. 删除节点
3. Dummy Node
4. 快慢指针

## Tree

### 遍历：DFS和BFS

1. 前序
2. 中序
3. 后序
4. BFS

## Sorting

选择排序最好理解，每次迭代都从子数组里寻找最小值即可，第k次迭代抽出来的即是第k小值

```py
def swap(self, arr, i, j):
    temp = arr[j]
    arr[j] = arr[i]
    arr[i] = temp


def selectSort(self, arr):
    l = len(arr)
    for i in range(0, l):
        min = 2 ** 31
        m = 0
        for j in range(i, l):
            if arr[j] < min:
                min = arr[j]
                m = j
        self.swap(arr, i, m)
    return arr
```

插入排序的话需要假设前面第i-1个数字是排好序的，然后把第i个数字插到已经排好序的数组里的恰当位置；既然是插入那么其实用链表比用数组要经济

```py
def insertSort(self, arr):
    l = len(arr)
    for i in range(1, l):
        temp = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > temp:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = temp
    return arr
```

合并排序很容易理解，要点是每排完一个数组就把另一个数组剩余值贴后面

```py
def merge(self, arr1, arr2):
    arr = []
    [l1, l2] = [len(arr1), len(arr2)]
    [i1, i2] = [0, 0]
    while i1 < l1 and i2 < l2:
        if arr1[i1] < arr2[i2]:
            arr.append(arr1[i1])
            i1 += 1
        else:
            arr.append(arr2[i2])
            i2 += 1
    if i1 == l1:
        arr += arr2[i2:]
    else:
        arr += arr1[i1:]
    return arr

def mergeSort(self, arr):
    l = len(arr)
    if l == 1:
        return arr
    elif l == 2:
        if arr[0] > arr[1]:
            self.swap(arr, 0, 1)
        return arr
    else:
        l1 = l // 2
        m1 = self.mergeSort(arr[0:l1])
        m2 = self.mergeSort(arr[l1:])
        return self.merge(m1, m2)
```

快速排序没什么好说的

```py
def quickSort(self, arr):
    l = len(arr)
    if l <= 1:
        return arr
    pivot = arr[int(random.random() * 200) % l]
    a = []
    b = []
    c = []
    for i in arr:
        if i < pivot:
            a.append(i)
        elif i == pivot:
            b.append(i)
        else:
            c.append(i)
    return self.quickSort(a) + b + self.quickSort(c)
```

## Union-find

Quick-find: 确定两个点是否处在同一个连通集里：遍历所有的边(p, q)，每次都把id[p]改成id[q]

```py
class UF:
    id = []
    count = 0

    def __init__(self, N):
        self.count = N
        for i in range(0, N):
            self.id.append(i)

    def dump(self):
        temp = ""
        for i in range(0, self.count):
            temp += (" " + str(i))
        print(temp)
        temp = ""
        for i in self.id:
            temp += (" " + str(i))
        print(temp)
        print()

    def find(self, p):
        return self.id[p]

    def quick_find(self, arr):
        for i in arr:
            pID = self.find(i[0])
            qID = self.find(i[1])
            if pID == qID:
                continue
            else:
                print(pID, qID)
                for j in range(0, self.count):
                    if self.id[j] == pID:
                        self.id[j] = qID
                self.dump()
```

## Hash Table

### 1. Two Sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target. You may assume that each input would have exactly one solution.

从头至尾检索一遍数组，如果Hashmap里没有(target - nums[i])就丢进去{nums[i], i}，否则的话就是遇到了结果，返回(target - nums[i])的角标
（Hashmap.get(target - nums[i])）和当前角标。

```java
public int[] twoSum(int[] nums, int target) {
    if (nums == null || nums.length == 0)
            return new int[]{0, 0};
    Map<Integer, Integer> hashmap = new HashMap<Integer, Integer>();
    int index1 = 0, index2 = 0;
    for (int i = 0; i < nums.length; i++) {
        if (hashmap.containsKey(target - nums[i])) {
            index1 = hashmap.get(target - nums[i]);
            index2 = i;
            return new int[]{index1, index2};
        } else {
            hashmap.put(nums[i], i);
        }
    }
    return new int[]{0, 0};
}
```
