# Misc

## 1. 正则表达式和各种String

### 8. String to Integer (atoi)

1. 用trim()函数删除左右的空格，如果剩余字符串为空则返回0；
2. 处理首位的正负号；
3. 处理数字，一旦遇到非数字字符则退出循环，处理溢出。

### 65. Valid Number

这题目纠结各种情况就是自讨苦吃，本质仅仅是一道正则表达式练习题。还有人用自动机做，我只想说真的是吃饱了撑的……

```py
"[‐+]?(([0‐9]+(.[0‐9]*)?)|.[0‐9]+)(e[‐+]?[0‐9]+)?"
```

### 179. Largest Number

这题的逻辑很浅显，然而限于我python力太弱，python3取消cmp之后的语法我也不会写……

这题的逻辑就是按照两个字串连接之后的数字大小来排序，不难

```py
def largestNumber(self, num):
    num = [str(x) for x in num]
    num.sort(cmp=lambda x, y: cmp(y+x, x+y))
    return ''.join(num).lstrip('0') or '0'
```

## 2. 取余操作

### Fast power

```py
(a * b) % p = ((a % p) * (b % p)) % p
```

## 3. Boyer-Moore 投票算法

### 169 & 229. Majority Element I & II

这题目里Majority元素必然出现超过半数次数，那么我们可以用一个逆向逻辑去考虑：

1. 一个非majority元素的话，必然有多于他出现次数的其他元素
2. 那么如果所有其他元素的出现次数都少于他，那么他就是majority元素
3. 要点是，数组中从candidate被赋值到count减到0的那一段可以被去除，余下部分的多数元素依然是原数组的多数元素。

229的逻辑和169类似，就不赘述了

```java
public int majorityElement(int[] num) {
    int major=num[0], count = 1;
    for(int i=1; i<num.length;i++) {
        if (count==0) {
            count++;
            major=num[i];
        } else if(major==num[i]) {
            count++;
        } else count--;
    }
    return major;
}
```

```py
def majorityElement(self, nums):
    if not nums:
        return []
    count1, count2, candidate1, candidate2 = 0, 0, 0, 1
    for n in nums:
        if n == candidate1:
            count1 += 1
        elif n == candidate2:
            count2 += 1
        elif count1 == 0:
            candidate1, count1 = n, 1
        elif count2 == 0:
            candidate2, count2 = n, 1
        else:
            count1, count2 = count1 - 1, count2 - 1
    return [n for n in (candidate1, candidate2)
                    if nums.count(n) > len(nums) // 3]
```

## 4. 无法归类的各种怪题

### 189. Rotate Array

这个题不难，ABCD要旋转成CDAB的话，可以先翻转ABCD到DCBA，然后分别翻转两半为CDAB即可

```java
public void rotate(int[] nums, int k) {
    k %= nums.length;
    reverse(nums, 0, nums.length - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, nums.length - 1);
}

public void reverse(int[] nums, int start, int end) {
    while (start < end) {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
}
```

### 172. Factorial Trailing Zeroes

这个题不难，首先要构成一个0的尾数就必须包含5，其次呢如果这个n的系数里包含不止一个5，需要处理完现在这个再去除以5，处理下一个

```py
def trailingZeroes(self, n):
    if n == 0:
        return 0
    else:
        a = self.trailingZeroes(n // 5)
        return n // 5 + a
```

### 204. Count Primes

埃拉托斯特尼筛法，不难，但这个例程可以学到不少python奇形怪状的语法

```py
def countPrimes(self, n):
    if n < 3: return 0
    primes = [True] * n
    primes[0] = primes[1] = False
    for i in range(2, int(n ** 0.5) + 1):
        if primes[i]:
            primes[i*i:n:i] = [False] * len(primes[i*i:n:i])
    return sum(primes)
```

### 233. Number of Digit One

这题目超级蠢，主要考点在思考每一位上1出现次数的逻辑

```java
int countDigitOne(int n) {
    int countr = 0;
    for (long long i = 1; i <= n; i *= 10) {
        long long divider = i * 10;
        countr += (n / divider) * i + min(max(n % divider - i + 1, 0LL), i);
    }
    return countr;
}
```

### 621. Task Scheduler

There is a non-negative cooling interval n that means between two same tasks, there must be at least n intervals that CPU are doing different tasks or just be idle.

这题的逻辑是这样的

1. 模块的次数为任务最大次数减1，模块的长度为n+1，
2. 最后加上的字母个数为出现次数最多的任务，可能有多个并列

```py
def leastInterval(self, tasks, N):
    task_counts = collections.Counter(tasks).values()
    M = max(task_counts)
    Mct = task_counts.count(M)
    return max(len(tasks), (M - 1) * (N + 1) + Mct)
```

### PocketGem. All paths from node to node