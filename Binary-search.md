# Binary Search

## 2. Binary Search

二分搜索的思想是很简单的，但一次性写对也不容易：

```py
def binarysearch(self, arr, k):
    m = len(arr) // 2
    if k == arr[m]:
        return arr[m]
    elif k > arr[m]:
        return self.binarysearch(arr[m:], k)
    else:
        return self.binarysearch(arr[0:m], k)
```

另外不要拘泥于python提供的简单写法：

```py
def binarysearch(self, arr, k, lo, hi):
    m = (lo + hi) // 2
    if k == arr[m]:
        return arr[m]
    elif k < arr[m]:
        return self.binarysearch(arr, k, lo, m)
    else:
        return self.binarysearch(arr, k, m + 1, hi)
```

### 33 \& 81 \& 153 \& 154. Find Minimum in Rotated Sorted Array II

这个题和153基本一样，简单的二分搜索，唯一的问题是如果两侧一样的话怎么办呢？153题不含重复值，含重复值的154题，去掉重复值不就跟153一样了吗

```py
def findMin(self, nums):
    """
    :type nums: List[int]
    :rtype: int
    """
    l = len(nums)
    if l < 1:                   # corner cases
        return 0
    elif l == 1:
        return nums[0]
    elif nums[0] < nums[l-1]:   # local minimum
        return nums[0]
    elif nums[0] > nums[l-1]:   # global minimum
        return min(self.findMin(nums[0:l//2]), self.findMin(nums[l//2:]))
    elif nums[0] == nums[l-1]:  # remove the repeat value
        return self.findMin(nums[1:])
```

### 162. Find Peak Element

这个题目就是分情况讨论的二分搜索，如果找到了peak那当然好，找不到的话，增长趋势就向右找，下跌趋势就向左找，如果搜索范围只有一个那只能返回他，如果有两个就返回那个较大值，一共这是五种情况

```py
def findPeakElement(self, nums):
    """
    :type nums: List[int]
    :rtype: int
    """
    left, right = 0, len(nums) - 1
    while True:
        if left == right: return left  # edge case
        elif left + 1 == right:
            if nums[left] > nums[right]: return left
            else: return right
        m = (left + right) // 2
        if nums[m-1] < nums[m] and nums[m+1] < nums[m]:
            return m
        elif nums[m-1] > nums[m] > nums[m+1]:
            right = m - 1
        else:
            left = m + 1
```

#### 34. First/Last Occurrence of Binary Search

这个题目也是简单的二分搜索，唯一需要讨论的就是边界条件

```java
// low and high are ids, n is array length
int first(int arr[], int low, int high, int x, int n) {
    if(high >= low) {
        int mid = low + (high - low)/2;
        if (( mid == 0 || x > arr[mid - 1]) && arr[mid] == x)
            return mid;
        else if(x > arr[mid])
            return first(arr, (mid + 1), high, x, n);
        else
            return first(arr, low, (mid - 1), x, n);
    }
    return -1;
}

int last(int arr[], int low, int high, int x, int n) {
    if (high >= low) {
        int mid = low + (high - low)/2;
        if (( mid == n-1 || x < arr[mid + 1]) && arr[mid] == x)
            return mid;
        else if (x < arr[mid])
            return last(arr, low, (mid - 1), x, n);
        else
            return last(arr, (mid + 1), high, x, n);
    }
    return -1;
}
```