# Two pointers

我已经不知道双指针跟回溯搜索相比哪个更陈腔滥调一点了，既然都这么陈腔滥调了，很显然这个思想是要透彻掌握的。

## 1. 双指针顺序操作

### 26. Remove Duplicates from Sorted Array

Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

很简单，维持两个指针，都在每次填数字时++，但后面那个指针在每次遇到重复数字时++。

```java
public int removeDuplicates(int[] nums) {
    int i = 1, j = 1;
    while (j<nums.length){
        if (nums[j‐1] == nums[j]) j++;
        else nums[i++] = nums[j++];
    }
    return i;
}
```

### 27. Remove Element

Given an array nums and a value val, remove all instances of that value in-place and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

双指针母题，每次遇到需要添加的字符就双指针都向前推进，否则就只推进前指针

```java
public int removeElement(int[] nums, int val) {
    int l = 0;
    for (int i = 0; i<nums.length; i++)
        if (nums[i] != val){
            nums[l] = nums[i];
            l++;
        }
    return l;
}
```

### 75. Sort Color

这个做法颇为鸡贼，\[0, i)部分是0，\[i, j)部分是1，\[j, n)部分是2

所以呢，2就一路向后推，遇到小于2的数字就增加j，等于0的时候就增加i

```py
def sortColors(self, nums):
    i = j = 0
    for k in range(0, len(nums)):
        v = nums[k]
        nums[k] = 2
        if v < 2:
            nums[j] = 1
            j += 1
        if v == 0:
            nums[i] = 0
            i += 1
```

### 41. First Missing Positive

难度2/5，时间复杂度O(n)，空间复杂度O(1)

这题目不算难，首先假定n个数字里第一个漏掉的正数不可能大于n，所以咱忽略掉所有大于n和小于0的数字，剩余数字就排列到原位就可以，然后再遍历一遍已经排布过的数组即可

```py
def swap(self, arr, a, b):
    c = arr[a]
    arr[a] = arr[b]
    arr[b] = c

def firstMissingPositive(self, nums):
    l = len(nums)
    for i in range(0, l):
        while 0 < nums[i] <= l and nums[nums[i] - 1] != nums[i]:
            self.swap(nums, i, nums[i] - 1)
    for i in range(0, l):
        if nums[i] != i+1:
            return i+1
    return l+1
```

## 2. 双指针窗口操作

双指针配合哈希表是字符串操作里极为陈腔滥调的题目，需要深入掌握

### 3. Longest Substring Without Repeating Characters

Given a string, find the length of the longest substring without repeating characters.

本题是双指针窗口操作的母题，双指针开头i结尾j指代当前字符串，如果哈希表里包含j则删除表中i项并i++，否则添加表中j项并j++

```java
public int lengthOfLongestSubstring(String s) {
    int left = 0, right = 0, max = 0;
    int[] hash = new int[26];
    char[] cs = s.toCharArray();
    while (right < cs.length){
        if (hash[cs[right] - 'a'] == 0) {
            hash[cs[right] - 'a']++;
            right++;
            max = Math.max(max, right - left);
        } else {
            hash[cs[left] - 'a']--;
            left++;
        }
    }
    return max;
}
```

### 5. Longest Palindromic Substring

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

从头到尾i遍历字符串s，如果(i - l - 1, i)处为回文，则回文长度l+2；否则如果(i - l, i)处为回文，则回文长度l+1。

```java
public String longestPalindrome(String s) {
    String res = "";
    int l = 0;
    for(int i=0;i<s.length();i++){
        if(isPalindrome(s, i - l - 1, i)){
            res = s.substring(i - l - 1, i + 1);
            l += 2;
        } else if(isPalindrome(s, i - l, i)){
            res = s.substring(i - l, i + 1);
            l += 1;
        }
    }
    return res;
}

public boolean isPalindrome(String s, int begin, int end){
    if(begin<0) return false;
    while(begin<end)
        if(s.charAt(begin++)!=s.charAt(end--)) return false;
    return true;
}
```

### 438. Find All Anagrams in a String

Given a string s and a non-empty string p, find all the start indices of p anagrams in s.

双指针+哈希表经典题目，我个人对leetcode上广泛流传的答案做了一个细节处的修改以更容易理解：既然哈希表里右指针所指代的字符大于等于1指代这个字符曾经在p中出现过，那么左指针指代的字符在哈希表里加回去之后大于等于1，也能代表这个字符曾经在p中出现过，否则的话左指针怎么加，右指针也都是减过的，最大不可能超过0。理解了这个机制就能破解掉大部分的双指针+哈希表题目。

```java
public List<Integer> findAnagrams(String s, String p) {
    List<Integer> ret = new ArrayList<>();
    char[] cs = s.toCharArray(), cp = p.toCharArray();
    int[] hash = new int[26];
    for (int i = 0; i<cp.length; i++)
        hash[cp[i] - 'a']++;
    int left = 0, right = 0, need = cp.length;
    while (right < cs.length){
        if (hash[cs[right++] - 'a']-- >= 1) need--;
        if (need == 0) ret.add(left);
        if (right - left == cp.length && ++hash[cs[left++] - 'a'] >= 1) need++;
    }
    return ret;
}
```

### 239. Sliding Window Maximum

当我们遇到新的数时，将新的数和双向队列的末尾比较，如果末尾比新数小，则把末尾扔掉，直到该队列的末尾比新数大或者队列为空的时候才住手。这样，我们可以保证队列里的元素是从头到尾降序的，由于队列里只有窗口内的数，所以他们其实就是窗口内第一大，第二大，第三大...的数。

保持队列里只有窗口内数的方法是每来一个新的把窗口最左边的扔掉，然后把新的加进去。然而由于我们在加新数的时候，已经把很多没用的数给扔了，这样队列头部的数并不一定是窗口最左边的数。这里的技巧是，我们队列中存的是那个数在原数组中的下标，这样我们既可以直到这个数的值，也可以知道该数是不是窗口最左边的数。

为什么时间复杂度是O(N)呢？因为每个数只可能被操作最多两次，一次是加入队列的时候，一次是因为有别的更大数在后面，所以被扔掉，或者因为出了窗口而被扔掉。

```java
public int[] maxSlidingWindow(int[] nums, int k) {
    if(nums == null || nums.length == 0) return new int[0];
    LinkedList<Integer> deque = new LinkedList<Integer>();
    int[] res = new int[nums.length + 1 - k];
    for(int i = 0; i < nums.length; i++){
        // 每当新数进来时，如果发现队列头部的数的下标，是窗口最左边数的下标，则扔掉`
        if(!deque.isEmpty() && deque.peekFirst() == i - k) deque.poll();
        // 把队列尾部所有比新数小的都扔掉，保证队列是降序的
        while(!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) deque.removeLast();
        // 加入新数
        deque.offerLast(i);
        // 队列头部就是该窗口内第一大的
        if((i + 1) >= k) res[i + 1 - k] = nums[deque.peek()];
    }
    return res;
}
```

## 3. 双指针夹逼操作

### 11. Container With Most Water

Given n nonnegative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x=axis forms a container,
such that the container contains the most water.

维持一个max函数，一开始从两端测量面积“夹逼”，每次迭代都删除两端中的短边，然后继续测量面积，直到两端相遇

```java
public static int maxArea(int[] height) {
    int len = height.length, low = 0, high = len - 1 ;
    int maxArea = 0;
    while (low < high) {
        maxArea = Math.max(maxArea, (high - low) * Math.min(height[low], height[high]));
        if (height[low] < height[high]) low++;
        else high--;
    }
    return maxArea;
}
```

### 42. Trapping Rain Water

Given n nonnegative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

双指针从左右向中间“夹逼”：

1. 以一个变量记录当前蓄水池的高度（初值为0）
2. 夹逼时每遇到一个小于此高度的边，则移动指针并加入水量
3. 否则在本轮迭代结束时改变当前蓄水池的高度，保证水池的高度在程序运行时是从小到大的

```java
public static int trap(int[] height) {
    int l = 0, r = height.length - 1, water = 0, curH = 0;
    while (l<r){
        while (l<r && height[l]<=curH)
            water += (curH - height[l++]);
        while (l<r && height[r]<=curH)
            water += (curH - height[r--]);
        curH = Math.min(height[l], height[r]);
    }
    return water;
}
```

### 15. 3Sum

3-sum并不是用的hashmap，还是排个序比较快

```py
def threeSum(self, nums):
    res = []
    nums.sort()
    for i in range(len(nums) - 2):
        if i > 0 and nums[i] == nums[i - 1]:
            continue
        l, r = i + 1, len(nums) - 1
        while l < r:
            s = nums[i] + nums[l] + nums[r]
            if s < 0:
                l += 1
            elif s > 0:
                r -= 1
            else:
                res.append((nums[i], nums[l], nums[r]))
                while l < r and nums[l] == nums[l + 1]:
                    l += 1
                while l < r and nums[r] == nums[r - 1]:
                    r -= 1
                l += 1
                r -= 1
    return res
```

### 16. 3Sum closest

3-sum closest单纯就是3-sum的简单改造

```py
def threeSumClosest(self, num, target):
    num.sort()
    result = num[0] + num[1] + num[2]
    for i in range(len(num) - 2):
        j, k = i+1, len(num) - 1
        while j < k:
            sum = num[i] + num[j] + num[k]
            if sum == target:
                return sum
            if abs(sum - target) < abs(result - target):
                result = sum
            if sum < target:
                j += 1
            elif sum > target:
                k -= 1
    return result
```

### 18. 4Sum

4-sum，这个算法的核心在于利用递归把n-sum问题化简为2-sum问题，然后用双指针解决2-sum问题

```py
def fourSum(self, nums, target):
    def findNsum(nums, target, N, result, results):
        # early termination
        if len(nums) < N or N < 2 or target < nums[0]*N or target > nums[-1]*N:
            return
        # two pointers solve sorted 2-sum problem
        if N == 2:
            l,r = 0,len(nums)-1
            while l < r:
                s = nums[l] + nums[r]
                if s == target:
                    results.append(result + [nums[l], nums[r]])
                    l += 1
                    while l < r and nums[l] == nums[l-1]:
                        l += 1
                elif s < target:
                    l += 1
                else:
                    r -= 1
        # recursively reduce N
        else:
            for i in range(len(nums)-N+1):
                if i == 0 or (i > 0 and nums[i-1] != nums[i]):
                    findNsum(nums[i+1:], target-nums[i], N-1, result+[nums[i]], results)
    results = []
    findNsum(sorted(nums), target, 4, [], results)
    return results
```

## 4. Misc

### 238. Product of Array Except Self

这题目题意不需要解释，实际操作就是从左向右累乘一轮，在累乘之前让输出数组B[i]等于累乘结果，这样他就等于他左侧所有数累乘，然后从右向左再来一轮，他就等于自己左右侧所有数累乘了

```py
def productExceptSelf(nums):
    p = 1
    n = len(nums)
    output = []
    for i in range(0,n):
        output.append(p)
        p = p * nums[i]
    p = 1
    print(output)
    for i in range(n-1,-1,-1):
        output[i] = output[i] * p
        p = p * nums[i]
    return output
```
