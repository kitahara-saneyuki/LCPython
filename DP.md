# Dynamic Programming

## DP套路

1. 定义：`dp[j]`表示什么含义，比如largest subarray sum ending at arr, and must include arr. 注意语言描述, 包括还是不包括arr/matrix[j]
2. 归纳法则：dp 的 dependency 是怎么样的，依赖于`dp[i-1]`还是`dp[i+1]`还是`dp[k]`for all k < i or all k > i 等等，试着过几个小例子推导一下
3. 初始态：往往是`dp[0]`，二维往往是第一行，第一列，也就是`dp[0], dp[0][j], dp[i][0]`
4. 结果：往往是`dp[n], max(dp)`等等, 从定义出发
5. 填充顺序：从归纳法则的依赖顺序出发判断
6. 优化: 分为时间和空间两方面。
    1. 时间的比较难，因为往往需要你重新定义dp状态和归纳法则。
    2. 空间比较简单，可以根据归纳法则看出来，比如斐波那契数列: `dp = dp[i - 1] + dp[i - 2]`, 那么dp只依赖于前两个元素，就不需要生成整个dp数组，保存两个变量即可，空间可以从`O(n)`优化到`O(1)`。

最后, 多做题多总结多积累小tips，熟能生巧后dp其实是非常简单，也非常有套路的，一些induction rule 的常见pattern 你一眼就能看出来了。

## 1. 一维DP

### 152. Maximum Product Subarray

不管你信不信，此题不是双指针而是dp，姊妹题53. Maximum Subarray，这两题是有一定区别的，负负相乘是正数，所以需要记录乘到此处的最大值和最小值，最小值乘以一个负数没准就变成了最大值呢对不对？

```py
def maxProduct(self, nums):
    if nums is None:
        return 0
    [maxherepre, minherepre, maxsofar] = [nums[0], nums[0], nums[0]]
    for i in range(1, len(nums)):
        maxhere = max(maxherepre * nums[i], minherepre * nums[i], nums[i])
        minhere = min(maxherepre * nums[i], minherepre * nums[i], nums[i])
        maxsofar = max(maxhere, maxsofar)
        maxherepre = maxhere
        minherepre = minhere
    return maxsofar
```

### 139. Word Break I

Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

Note:

- The same word in the dictionary may be reused multiple times in the segmentation.
- You may assume the dictionary does not contain duplicate words.

Example 1:

```md
Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

Example 2:

```md
Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
```

Example 3:

```md
Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false
```

可能是比较简单的动态规划题目，要注意下标变换

```py
def wordBreak(self, s, wordDict):
    l = len(s)
    dp = [False] * l
    for i in range(l):
        for w in wordDict:
            lw = len(w)
            if w == s[i-lw+1:i+1] and (dp[i-lw] or i-lw == -1):
                dp[i] = True
    return dp[-1]
```

### 140. Word Break II

Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

Note:

- The same word in the dictionary may be reused multiple times in the segmentation.
- You may assume the dictionary does not contain duplicate words.

Example 1:

```md
Input:
s = "catsanddog"
wordDict = ["cat", "cats", "and", "sand", "dog"]
Output:
[
  "cats and dog",
  "cat sand dog"
]
```

Example 2:

```md
Input:
s = "pineapplepenapple"
wordDict = ["apple", "pen", "applepen", "pine", "pineapple"]
Output:
[
  "pine apple pen apple",
  "pineapple pen apple",
  "pine applepen apple"
]
Explanation: Note that you are allowed to reuse a dictionary word.
```

Example 3:

```md
s = "catsandog"
wordDict = ["cats", "dog", "sand", "and", "cat"]
Output:
[]
```

这题目实际上是DFS，两个注意事项：

1. 需要剪枝
2. 需要cache否则会TLE

```py
class Solution(object):
    def dfs(self, s, words, start, cache):
        if start in cache:
            return cache[start]
        result = []
        for end in range(start + 1, len(s) + 1):
            word = s[start: end]
            if word not in words:
                continue
            if end == len(s):
                result.append(word)
            else:
                for sub_s in self.dfs(s, words, end, cache):
                    result.append(word + ' ' + sub_s)
        cache[start] = result
        return result

    def wordBreak(self, s, wordDict):
        if not s:
            return []
        words = set(wordDict)
        return self.dfs(s, words, 0, {})
```

### 最大面积系列题

#### 84. Largest Rectangle in Histogram

1. 栈里保存的是升序的建筑
2. 添加一个新建筑之前，把所有比新建筑高的建筑都pop出去
3. 弹出去的建筑指代一个新矩形，左侧为现有的栈顶，右侧为新建筑
4. 原理：栈里永远是从左向右和从小到大的顺序，因此每次弹栈的时候更新的都是更矮和更左的矩形
5. 边界条件：放一个dummy的-1

```py
def largestRectangleArea(self, height):
    height.append(0)
    stack = [-1]
    ans = 0
    for i in xrange(len(height)):
        while height[stack[-1]] > height[i]:
            h = height[stack.pop()]
            w = i - stack[-1] - 1
            ans = max(ans, h * w)
        stack.append(i)
    height.pop()
    return ans
```

#### 85. Maximal Rectangle

这题的精神是跟84一样的，但需要调用一下DP：`height[i]`保存从左到右到i为止有多少个连续的1，复杂度`O(n^2)`

```py
def maximalRectangle(self, matrix):
    if not matrix or not matrix[0]:
        return 0
    n = len(matrix[0])
    height = [0] * (n + 1)
    ans = 0
    for row in matrix:
        for i in range(n):
            height[i] = height[i] + 1 if row[i] == '1' else 0
        stack = [-1]
        for i in range(n + 1):
            while height[i] < height[stack[-1]]:
                h = height[stack.pop()]
                w = i - 1 - stack[-1]
                ans = max(ans, h * w)
            stack.append(i)
    return ans
```

#### 221. Maximal Square

因为是square，所以dp的状态转移方程要考虑`min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1`

```py
class Solution:
    def maximalSquare(self, matrix):
        if not matrix:
            return 0
        m, n = len(matrix), len(matrix[0])
        dp = [[0 if matrix[i][j] == '0' else 1 for j in range(n)] for i in range(m)]

        for i in range(1, m):
            for j in range(1, n):
                if matrix[i][j] == '1':
                    dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1
                else:
                    dp[i][j] = 0

        ans = max([max(i) for i in dp])
        return ans ** 2
```

#### 764. Largest Plus Sign

这题是反向思维，他这map里只有mine是0，那么初始化先构建一个矩阵`dp[i][j]`表示该点最大的十字：

```md
1 1 1 1 1
1 2 2 2 1
1 2 3 2 1
1 2 2 2 1
1 1 1 1 1
```

每一个mine都会影响自己row和col上的每一个dp点，使得该点的最大十字长度不能超过\[该点到mine的距离\]

```py
class Solution(object):
    def orderOfLargestPlusSign(self, N, mines):
        dp = [[min(i, N - 1 - i, j, N - 1 - j) + 1 for j in range(N)] for i in range(N)]
        for (x, y) in mines:
            for i in range(N):
                dp[i][y] = min(dp[i][y], abs(i - x))
                dp[x][i] = min(dp[x][i], abs(i - y))
        return max([max(row) for row in dp])
```

LC修改了测试case导致前一种方法会TLE，我们换个思路，采用dp

1. `dp[i][j]`表示横排或者纵排最近一个0的距离
2. 初始化我们假设不存在0，所以`dp[i][j]`全都是N
3. 对每一行都要双向考虑

```py
def orderOfLargestPlusSign(self, N, mines):
    grid = [[N] * N for i in range(N)]
    for m in mines:
        grid[m[0]][m[1]] = 0
    for i in range(N):
        l, r, u, d = 0, 0, 0, 0
        for j, k in zip(range(N), reversed(range(N))):
            l = l + 1 if grid[i][j] != 0 else 0
            if l < grid[i][j]:
                grid[i][j] = l
            r = r + 1 if grid[i][k] != 0 else 0
            if r < grid[i][k]:
                grid[i][k] = r
            u = u + 1 if grid[j][i] != 0 else 0
            if u < grid[j][i]:
                grid[j][i] = u
            d = d + 1 if grid[k][i] != 0 else 0
            if d < grid[k][i]:
                grid[k][i] = d
    res = 0
    for i in range(N):
        for j in range(N):
            if res < grid[i][j]:
                res = grid[i][j]
    return res
```

### 91. Decode Ways

A message containing letters from A-Z is being encoded to numbers using the following mapping:

```md
'A' -> 1
'B' -> 2
...
'Z' -> 26
Given a non-empty string containing only digits, determine the total number of ways to decode it.
```

Example 1:

```md
Input: "12"
Output: 2
Explanation: It could be decoded as "AB" (1 2) or "L" (12).
```

Example 2:

```md
Input: "226"
Output: 3
Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

可能是比较简单的动态规划题目，考虑两个情况即可

```py
def numDecodings(self, s):
    # dp[i] = dp[i-1] if s[i] != "0"
    #       + dp[i-2] if "09" < s[i-2:i] < "27"
    if s == "": return 0
    dp = [0 for x in range(len(s)+1)]
    dp[0] = 1
    for i in range(1, len(s)+1):
        if s[i-1] != "0":
            dp[i] += dp[i-1]
        if i != 1 and s[i-2:i] < "27" and s[i-2:i] > "09":  # "01"ways = 0
            dp[i] += dp[i-2]
    return dp[len(s)]
```

### 300. Longest Increasing Subsequence

这个题目不简单，需要结合动态规划和二分搜索才能达到O(nlogn)的复杂度。先说动态规划，dp[i]这个数组，第i个记录的，就是0-i这个递增子序列里可能出现的最小值。为什么呢？因为dp[i]是单调递增的

那如何能保证他最小呢？有个简单的办法，就是用二分搜索寻找【目前遇到的数字】的插入点，【小于这个数字的最大值】后面的一格，插入进去，就是最小了。

顺便如果二分搜索搜到了末尾的话，就贴到末尾，说明递增子序列延长了。

```py
def bs(self, arr, target):
    left, right = 0, len(arr)
    m = (left + right) // 2
    while left < right:
        if target == arr[m]:
            return m
        elif target > arr[m]:
            left = m + 1
        else:
            right = m
        m = (left + right) // 2
    return -(m + 1)

def lengthOfLIS(self, nums):
    """
    :type nums: List[int]
    :rtype: int
    """
    dp = []
    for x in nums:
        i = self.bs(dp, x)
        if i < 0:
            i = - (i + 1)
        if i == len(dp):
            dp.append(x)
        else:
            dp[i] = x
    return len(dp)
```

### 494. Target Sum

这题目看图就懂了……
![alt text](https://leetcode.com/uploads/files/1485048726667-screen-shot-2017-01-21-at-8.31.48-pm.jpg "DP 1")

```py
def findTargetSumWays(self, nums, S):
    """
    :type nums: List[int]
    :type S: int
    :rtype: int
    """
    sumN = 0
    for i in nums: sumN += i
    if S > sumN or S < -sumN: return 0
    dp = [0] * (2 * sumN + 1)
    dp[sumN] = 1
    for i in nums:
        nextdp = [0] * (2 * sumN + 1)
        for j in range(0, len(dp)):
            if dp[j] != 0:
                nextdp[j + i] += dp[j]
                nextdp[j - i] += dp[j]
        dp = nextdp
    return dp[sumN + S]
```

## 2. 二维DP

### 62. Unique Paths

A robot is located at the top-left corner of a m x n grid. The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid. How many possible unique paths are there? Note: m and n will be at most 100.

Solution: 这个题目是二维动态规划的“母题”，很简单，想清楚2*2的情况就可以做出来。

ps: 高中讲数学归纳法的意义就在这了，动态规划的思想跟数学归纳法很相似，只需要证明两个情况下（0->1, x->x+1）状态转移方程成立即可。

```java
public int uniquePaths(int m, int n) {
    int[][] dp = new int[m][n];
    for (int i = 0; i<m; i++)
        dp[i][0] = 1;
    for (int i = 0; i<n; i++)
        dp[0][i] = 1;
    for (int i = 1; i<m; i++)
        for (int j = 1; j<n; j++)
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
    return dp[m - 1][n - 1];
}
```

### 64. Minimum Path Sum

```md
Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```

```py
def minPathSum(self, grid):
    if len(grid) == 0:
        return 0
    for i in range(0, len(grid)):
        for j in range(0, len(grid[0])):
            if i == 0 and j != 0:
                grid[i][j] += grid[i][j-1]
            elif j == 0 and i != 0:
                grid[i][j] += grid[i-1][j]
            elif i != 0 and j != 0:
                grid[i][j] += min(grid[i][j-1], grid[i-1][j])
    return grid[len(grid) - 1][len(grid[0]) - 1]
```

### 编辑距离系列题

#### 72. Edit Distance

1. DP定义：`dp[i][j]`指从`word1[0:i]`转变到`word2[0:j]`的最优操作次数
2. 初始化：`dp[i][0] = i`和`dp[0][j] = j`，根据定义
3. 可以做的操作：
    1. delete：`dp[i-1][j] + 1` —— 保留了从`word1[0:i-1]`转变到`word2[0:j]`的最优操作次数，因为我们的 word1 的 0~i-1 已经能够转变到 word2 了，所以我们就直接把 word1 中的最后一个字符删除掉就行了。所以就需要额外进行一个 删除 操作。
    2. insert：`dp[i][j-1] + 1` —— 保留了从 word1[0:i] 转变到 word2[0:j-1] 的最优操作次数，因为我们的 word1 的 0~i 只能转变到 word2 的倒数第二位，所以我们就直接在 word1 的末尾添加一个与 word2 的最后一个字符相同的字符就可以了。所以就需要额外进行一个 插入 操作。
    3. replace：`dp[i-1][j-1] + 1` —— 保留了从 word1[0:i-1] 转变到 word2[0:j-1] 的最优操作次数，因为我们的 word1 的 0~i-1 只能转变到 word2 的倒数第二位，而 word1 的最后一位与 word2 的最后一位是不同的，所以现在的情况只需要额外的一个 替换 操作即可。

```py
class Solution(object):
    def minDistance(self, word1, word2):
        m = len(word1)
        n = len(word2)
        dp = [[i+j for j in range(len(word2)+1)] for i in range(len(word1)+1)]
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if word1[i - 1] == word2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1]
                else:
                    dp[i][j] = 1 + min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1])
        return dp[-1][-1]
```

#### 97. Interleaving String

Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

Solution: 二维DP，这题相对于72要简单一点

1. DP定义：`dp[i][j]`意味着`s1[:i]`和`s2[:j]`可以构成`s3[i+j]`
2. 初始化：根据定义，
    1. `dp[i][0] = s1[:i] == s3[:i]`
    2. `dp[0][j] = s2[:j] == s3[:j]`
3. 递推关系：`dp[i][j] = or(`
    1. `dp[i - 1][j] and s3[i + j - 1] == s1[i - 1]`
    2. `dp[i][j - 1] and s3[i + j - 1] == s2[j - 1]`

```py
def isInterleave(self, s1, s2, s3):
    # edge cases
    if s1 == '':
        return s2 == s3
    if s2 == '':
        return s1 == s3
    if s3 == '':
        return s1 == s2 == ''
    len1, len2, len3 = len(s1), len(s2), len(s3)
    if len3 != len1 + len2:
        return False

    # prepare DP matrix and base case
    dp = [[True] * (len2 + 1) for _ in range(len1 + 1)]
    # base case for s1 & s2
    for i in range(1, len1 + 1):
        dp[i][0] = s1[:i] == s3[:i]
    for j in range(1, len2 + 1):
        dp[0][j] = s2[:j] == s3[:j]
    # non-base case
    for i in range(1, len1 + 1):
        for j in range(1, len2 + 1):
            dp[i][j] = dp[i - 1][j] and s3[i + j - 1] == s1[i - 1] \
                    or dp[i][j - 1] and s3[i + j - 1] == s2[j - 1]
    return dp[len1][len2]
```

#### 583. Delete Operation for Two Strings

```md
Given two words word1 and word2, find the minimum number of steps required to make word1 and word2 the same, where in each step you can delete one character in either string.

Example 1:
Input: "sea", "eat"
Output: 2
Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".
```

Solution: 二维DP，这题目的实质就是Longest common subsequence

1. DP定义：`dp[i][j]`指`w1[0:i]`和`w2[0:j]`的最长公共子序列长度
2. 初始化：根据定义，
    1. `dp[i][0] = 0`
    2. `dp[0][j] = 0`
3. 递推关系：`dp[i][j] = max(`
    1. `dp[i][j - 1]`
    2. `dp[i - 1][j]`
    3. `dp[i - 1][j - 1] + (w1[i] == w2[j])`

```py
def minDistance(self, w1, w2):
    m, n = len(w1), len(w2)
    dp = [[0] * (n + 1) for i in range(m + 1)]
    for i in range(m):
        for j in range(n):
            dp[i + 1][j + 1] = max(dp[i][j + 1], dp[i + 1][j], dp[i][j] + (w1[i] == w2[j]))
    return m + n - 2 * dp[m][n]
```

#### 712. Minimum ASCII Delete Sum for Two Strings

```md
Given two strings s1, s2, find the lowest ASCII sum of deleted characters to make two strings equal.

Example 1:
Input: s1 = "sea", s2 = "eat"
Output: 231
Explanation: Deleting "s" from "sea" adds the ASCII value of "s" (115) to the sum.
Deleting "t" from "eat" adds 116 to the sum.
At the end, both strings are equal, and 115 + 116 = 231 is the minimum sum possible to achieve this.
```

Solution: 二维DP，这题目的实质就是Longest common subsequence

1. DP定义：`dp[i][j]`指`w1[0:i]`和`w2[0:j]`的最长公共子序列长度
2. 初始化：根据定义，
    1. `dp[i][0] = 0`
    2. `dp[0][j] = 0`
3. 递推关系：`dp[i][j] = max(`
    1. 如果`w1[i] == w2[j]`，`dp[i - 1][j - 1] + ord(w1[i])`
    2. `dp[i][j - 1]`
    3. `dp[i - 1][j]`

```py
class Solution(object):
    def minimumDeleteSum(self, s1, s2):
        l1, l2 = len(s1), len(s2)
        dp = [[0] * (l2 + 1) for _ in range(l1 + 1)]
        for i in range(l1):
            for j in range(l2):
                if s1[i] == s2[j]:
                    dp[i + 1][j + 1] = dp[i][j] + ord(s1[i])
                else:
                    dp[i + 1][j + 1] = max(dp[i][j + 1], dp[i + 1][j])
        result = sum(map(ord, s1 + s2)) - dp[l1][l2] * 2
        return result
```

### 10 & 44. Regular Expression / Wildcard Matching

Implement regular expression matching with support for '.' and '*'.

- '.' Matches any single character.
- '*' Matches zero or more of the preceding element.
- The matching should cover the entire input string (not partial).

使用动态规划。字符串为s，正则表达式为p。

预处理：用dp[i][j]表示s串的前i个字符和p串的前j个字符是否匹配。dp[0][0] = true；

如果p[i]为'\*'，则dp[0][i] 需要p一直为'\*'才为真

1. 如果s[i] == p[j]或p[j] == '\.'，dp[i+1][j+1] = dp[i][j]；
2. 如果p[j] == '\*'
    1. 如果s[i] == p[j-1] 或p[j-1] == '\.'，dp[i+1][j+1]取下列三者的或
        1. dp[i][j+1] （a*代表一个a）
        2. dp[i+1][j] （a*代表多个a）
        3. dp[i+1][j-1] （a*不代表a）
    2. 否则的话dp[i+1][j+1] = dp[i+1][j-1] （a*不代表a）

```java
public boolean isMatch(String s, String p) {
    // Corner case
    if (s == null || p == null)
        return false;

    // Preprocessing
    boolean [][] dp = new boolean[s.length() + 1][p.length() + 1];
    dp[0][0] = true;
    for (int i = 0; i <= p.length(); i++) {
        dp[0][i + 1] = (p.charAt(i) == '*' && dp[0][i - 1]);
    }

    for (int i = 0; i < s.length(); i++) {
        for (int j = 0; j < p.length(); j++) {
            if (s.charAt(i) == p.charAt(j) || p.charAt(j) == '.')
                dp[i + 1][j + 1] = dp[i][j];
            else if (p.charAt(j) == '*') {
                if (s.charAt(i) == p.charAt(j - 1) || p.charAt(j - 1) == '.')
                    dp[i + 1][j + 1] = dp[i + 1][j - 1] || dp[i + 1][j] || dp[i][j + 1];
                else
                    dp[i + 1][j + 1] = dp[i + 1][j - 1];
            }
        }
    }
    return dp[s.length()][p.length()];
}
```

Implement wildcard pattern matching with support for '?' and '\*'.

- '?' Matches any single character.
- '\*' Matches any sequence of characters (including the empty sequence).
- The matching should cover the entire input string (not partial).

这题和第10题几乎完全一样，只是关键字略有不同，因为'\*'前面不带任何字，所以：

1. 如果s[i] == p[j-1] 或p[j-1] == '\.'，dp[i+1][j+1]取下列两者的或
    1. dp[i][j+1] （*不代表任何字符）
    2. dp[i+1][j] （*代表多个字符）

```java
public boolean isMatch(String s, String p) {
    boolean[][] dp = new boolean[s.length() + 1][p.length() + 1];
    dp[0][0] = true;
    for (int i = 1; i <= p.length(); i++) {
        dp[0][i] = p.charAt(i-1) == '*' && dp[0][i - 1];
    }
    for (int i = 0; i < s.length(); i++) {
        for (int j = 0; j < p.length(); j++){
            if (s.charAt(i) == p.charAt(j) || p.charAt(j) == '?')
                dp[i + 1][j + 1] = dp[i][j];
            else if (p.charAt(j) == '*')
                dp[i + 1][j + 1] = dp[i + 1][j] || dp[i][j + 1];
        }
    }
    return dp[s.length()][p.length()];
}
```

### 174. Dungeon Game

m*n矩阵，骑士从左上走到右下，只能向右或向下，每个格子为骑士经过这个格子损失或增加的HP值，求骑士必须拥有的起始HP值

1. 最低HP是1，0的话骑士就死了，而且中途不能出现0HP
2. 从最右下到最左上DP
3. 需求的HP就是格子里的HP的负值

```py
def calculateMinimumHP(self, dungeon):
    if not dungeon or not dungeon[0]:
        return 0
    m = len(dungeon)
    n = len(dungeon[0])
    dp=[[2 ** 31 - 1] * (n + 1) for _ in range(m + 1)]
    dp[m][n - 1]=1
    dp[m - 1][n]=1
    for i in range(m - 1, -1, -1):
        for j in range(n - 1, -1, -1):
            need = min(dp[i + 1][j], dp[i][j + 1]) - dungeon[i][j]
            dp[i][j] = 1 if need <= 0 else need
    return dp[0][0]
```

### 121-123 & 188. 股票系列题

1. 只允许交易一次，求最大收益
2. 允许交易无数次，求最大收益
3. 只允许交易2次，求最大收益
4. 允许交易k次，求最大收益

股票系列题里的1和2比较简单就不细说了

```java
public int maxProfit(int[] prices) {
    if (prices.length == 0)
        return 0;
    int min = prices[0];
    int profit = 0;
    for (int i = 1; i < prices.length; i++) {
        if (prices[i] < min)
            min = prices[i];
        else
            if (prices[i] - min > profit)
                profit = prices[i] - min;
    }
    return profit;
}
```

```py
def maxProfit(self, prices):
    ret = 0
    for i in range(1, len(prices)):
        ret += max(0, prices[i] - prices[i-1])
    return ret
```

3跟4先说4

1. 这套题目里所有的股票都是T+1的，所以如果`k >= l / 2`，那么就直接上第2题答案
2. DP：dp[i, j]代表最多i次交易之后在第j个价格的最大收益
    1. 初始化：dp[i, 0] = 0，dp[0, j] = 0，没有买卖就没有杀害
    2. dp[i, j] = max(dp[i, j-1], prices[j] - prices[jj] + dp[i-1, jj])
        1. for jj in range of [0, j-1]
        2. 意思是dp[i, j]等于下列两项里的最大值
            1. dp[i, j-1]
            2. dp[i - 1, jj] + (price[j] - price[jj])
    3. 推导得到dp[i, j] = max(dp[i, j-1], prices[j] + max(dp[i-1, jj] - prices[jj]))
3. 第3题就是第4题变形，不需要思考

```java
public int maxProfit(int k, int[] prices) {
    int len = prices.length;
    if (k >= len / 2)
        return quickSolve(prices);
    int[][] dp = new int[k + 1][len];
    for (int i = 1; i <= k; i++) {
        int localMax =  -prices[0];
        for (int j = 1; j < len; j++) {
            dp[i][j] = Math.max(dp[i][j - 1], prices[j] + localMax);
            localMax =  Math.max(localMax, dp[i - 1][j - 1] - prices[j]);
        }
    }
    return dp[k][len - 1];
}

private int quickSolve(int[] prices) {
    int len = prices.length, profit = 0;
    for (int i = 1; i < len; i++)
        // as long as there is a price gap, we gain a profit.
        if (prices[i] > prices[i - 1])
            profit += prices[i] - prices[i - 1];
    return profit;
}
```

### 131 / 2. Palindrome Partitioning I / II

```md
Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

Example:

Input: "aab"
Output:
[
  ["aa","b"],
  ["a","a","b"]
]
```

简单DFS

```py
class Solution(object):
    def partition(self, s):
        res = []
        self.helper(s, 0, [], res)
        return res

    def helper(self, s, idx, path, res):
        if idx == len(s):
            res.append(path)
            return
        for i in range(idx + 1, len(s) + 1):
            temp = s[idx:i]
            if temp == temp[::-1]:
                self.helper(s, i, path + [temp], res)
```

```md
Given a string s, partition s such that every substring of the partition is a palindrome.

Return the minimum cuts needed for a palindrome partitioning of s.

Example:

Input: "aab"
Output: 1
Explanation: The palindrome partitioning ["aa","b"] could be produced using 1 cut.
```

1. 两个dp矩阵：isPal和dp
    1. `isPal[i][j]`表示`s[j:i]`是否是回文
    2. `dp[i]`表示在i位置处的最优切割
2. 递推：
    1. i从0到l，j从i到0
    2. 判断`s[j:i]`是回文的标准：
        1. `s[i] == s[j]`
        2. `i - j < 2` 或者 `isPal[i - 1][j + 1]`
    3. 既然`s[j:i]`是回文，那么`dp[i] = min(dp[i], dp[j - 1] + 1)`

```py
class Solution:
    # @param {string} s
    # @return {integer}
    def minCut(self, s):
        if s == s[::-1]: return 0
        lens = len(s)
        # edge case: only 1 cut
        for i in range(1, lens):
            if s[:i] == s[:i][::-1] and s[i:] == s[i:][::-1]:
                return 1
        #
        isPal = [[False] * (i + 1) for i in range(lens)]
        dp = range(lens) + [-1]
        for i in range(lens):
            for j in range(i, -1, -1):
                if s[i] == s[j] and (i - j < 2 or isPal[i - 1][j + 1]):
                    isPal[i][j] = True
                    dp[i] = min(dp[i], dp[j - 1] + 1)
        return dp[lens - 1]
```

## 3. 01背包问题

### 416. Partition Equal Subset Sum

01背包问题母题，请注意排序会造成`O(nlogn)`的复杂度，虽然直截了当但八成会TLE。

1. `dp[i]`表示使用`nums`里的数字能否组成`i`

```java
public boolean canPartition(int[] nums) {
    // edge case
    if (nums == null || nums.length == 0)
        return true;
    // find half
    int sum = 0;
    for (int n:nums)
        sum += n;
    if (sum % 2 != 0)
        return false;
    int target = sum / 2;
    // dp
    boolean[] dp = new boolean[target+1];
    dp[0] = true;
    for(int num: nums)
        for(int i = target; i >= num; i--)
            dp[i] = dp[i - num] || dp[i];
    return dp[target];
}
```

### 474. Ones and Zeroes

你有一串0和1组成的字符串，问用m个1和n个0能组成最多多少个字符串？

```md
Input: Array = {"10", "0001", "111001", "1", "0"}, m = 5, n = 3
Output: 4

Explanation: This are totally 4 strings can be formed by the using of 5 0s and 3 1s, which are “10,”0001”,”1”,”0”
```

典型的01背包问题

1. `dp[i][j]`表示有i个0和j个1时能组成的最多字符串的个数
2. 状态转移方程很简单，就是`dp[i][j] = Math.max(1 + dp[i - zeros][j - ones], dp[i][j])`
3. 注意矩阵是从右下往左上递推的

```java
public int findMaxForm(String[] strs, int m, int n) {
    int[][] dp = new int[m+1][n+1];
    for (String s : strs) {
        int[] count = count(s);
        for (int i = m; i >= count[0]; i--)
            for (int j = n; j >= count[1]; j--)
                dp[i][j] = Math.max(1 + dp[i - count[0]][j - count[1]], dp[i][j]);
    }
    return dp[m][n];
}

public int[] count(String str) {
    int[] res = new int[2];
    for (int i=0;i<str.length();i++)
        res[str.charAt(i) - '0']++;
    return res;
}
```
