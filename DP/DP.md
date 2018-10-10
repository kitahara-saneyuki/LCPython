# Dynamic Programming

动态规划看书也看不懂，反正书上也是用例子来讲解，还不如实际做两道题就领悟的快。动态规划既可以理解成带记忆的递归，也可以理解成数学归纳法。

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

### 97. Interleaving String

Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

Solution: 二维DP，`dp[i][j]`意味着`s1[:i]`和`s2[:j]`可以构成`s3[i+j]`

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
    dp = [[0] * (len2 + 1) for _ in range(len1 + 1)]
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
        1. jj in range of [0, j-1]
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