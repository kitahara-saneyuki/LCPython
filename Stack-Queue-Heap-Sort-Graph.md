# Stack-Queue-Heap-Sort-Graph

## 1. Heap

### 347. Top K Frequent Elements

这个题不难，hash map+heap queue，需要注意的就是heapq默认是最小堆，改成最大堆只需要把key变成负的就可以呀

```py
def topKFrequent(self, nums, k):
    freq, h, ret = {}, [], []
    for i in nums:
        if i in freq:
            freq[i] += 1
        else:
            freq[i] = 1
    for i in freq:
        heapq.heappush(h, (-freq[i], i))
    for i in range(0, k):
        temp = heapq.heappop(h)
        ret.append(temp[1])
    return ret
```

### Given unsorted array of int, each element is the length of a rod, return the minimum total cost of combining all rods

难度2/5，这题目最简单的办法很显然是最小堆，不证明了，每次从最小堆里提出来两根棍子接一起，然后把接起来的新棍子丢最小堆里，每次操作的复杂度是O(logn)，所以总时间复杂度就是O(nlogn)，空间复杂度很显然是O(n)

```java
int minCost(int len[], int n) {
    int cost = 0;
    struct MinHeap* minHeap = createAndBuildMinHeap(len, n);
    while (!isSizeOne(minHeap)) {
        int min     = extractMin(minHeap);
        int sec_min = extractMin(minHeap);
        cost += (min + sec_min);
        insertMinHeap(minHeap, min+sec_min);
    }
    return cost;
}
```

## 2. Interval问题

### 56 & 57. Merge / Insert Intervals

这俩题目大同小异，无非是先排序，再判断边界条件而已

```py
def merge(self, intervals):
    out = []
    for i in sorted(intervals, key=lambda i: i.start):
        if out and i.start <= out[-1].end:
            out[-1].end = max(out[-1].end, i.end)
        else:
            out += i,
    return out
```

```py
def insert(self, intervals, newInterval):
    out = []
    intervals.append(newInterval)
    for i in sorted(intervals, key=lambda i: i.start):
        if out and i.start <= out[-1].end:
            out[-1].end = max(out[-1].end, i.end)
        else:
            out += i,
    return out
```

## 3. Stack & Queue

### 155. min stack

这个东西的难点就是如何记录【某一时刻的最小值】，那很简单，每次最小值变得更小，就往栈里连推两次，第一次推最小值，第二次推x；每次最小值变得更大的时候呢，从栈里连弹两次，第一次弹出来的是x，第二次弹出来的是最小值

```java
class MinStack {
    int min = Integer.MAX_VALUE;
    Stack<Integer> stack = new Stack<Integer>();
    public void push(int x) {
        if(x <= min){
            stack.push(min);
            min=x;
        }
        stack.push(x);
    }
    public void pop() {
        if(stack.pop() == min)
            min=stack.pop();
    }
    public int top() { return stack.peek();}
    public int getMin() { return min;}
}
```

## 4. 奇怪的排序

### 220. Contains Duplicate III

坐标差不能大于k，值差不能大于t

如果t=0的话其实和LC219是同一个题目，加入t的话就是利用桶排序，每个桶大小为t+1，每经历过一轮k，就删除bucket里i-k所对应的值，这样就可以避免坐标差超过k的情况出现，而值差则是利用桶排序的性质，每一轮中在m桶里的数字很显然值差小于t，两侧桶里的数字经过恰当的测试值差也会小于t

```py
def containsNearbyAlmostDuplicate(self, nums, k, t):
    bucket = {}
    if t < 0: return False
    w, n = t + 1, len(nums)
    for i in range(0, n):
        m = nums[i] // w
        if m in bucket:
            return True
        if m - 1 in bucket and abs(nums[i] - bucket[m - 1]) < w:
            return True
        if m + 1 in bucket and abs(nums[i] - bucket[m + 1]) < w:
            return True
        bucket[m] = nums[i]
        if i >= k:
            del bucket[nums[i-k] // w]
    return False
```

## 5. Graph

### 133. Clone graph

这个问题的题眼是，复制一个图，其中每个节点都只能创造一次，第二次调用它的时候你就得重复调用以前使用过的节点

其他的其实就是简单的BFS而已

```py
def cloneGraph(self, node):
    if not node:
        return
    nodeCopy = UndirectedGraphNode(node.label)
    dic = {node: nodeCopy}
    queue = collections.deque([node])
    while queue:
        node = queue.popleft()
        for neighbor in node.neighbors:
            if neighbor not in dic:
                # store copy
                neighborCopy = UndirectedGraphNode(neighbor.label)
                dic[neighbor] = neighborCopy
                dic[node].neighbors.append(neighborCopy)
                queue.append(neighbor)
            else:
                # we met this node before, no need to insert it to queue
                # but necessary to add that edge
                dic[node].neighbors.append(dic[neighbor])
    return nodeCopy
```