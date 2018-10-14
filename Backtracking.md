# Backtracking & Permutation

## 1. Depth First Search

leetcode四大陈腔滥调：回溯搜索、动态规划、双指针，二分法之首的回溯搜索

### 51. N-Queens

这题太老套就不叙述题目了，本题是回溯搜索的母题，注意不要为了图省事每次调用递归函数都复制一遍棋盘，放在640k内存的时代这么玩妥妥爆栈。至于位操作之类属于奇技淫巧，实际上很影响代码可读性。

回溯搜索的实质在于，调用递归函数前更改的条件，要在调用完之后再改回来。

```java
public List<List<String>> solveNQueens(int n) {
    List<List<String>> ret = new ArrayList<>();
    ArrayList<String> board = new ArrayList<>();
    for (int i = 0; i<n; i++) {
        char[] input = new char[n];
        Arrays.fill(input, '.');
        board.add(String.copyValueOf(input));
    }
    dfs(n, 0, board, ret);
    return ret;
}

public void dfs(int n, int line, ArrayList<String> board, List<List<String>> ret){
    for (int i = 0; i<n; i++){
        char[] input = new char[n];
        Arrays.fill(input, '.');
        input[i] = 'Q';
        board.set(line, String.copyValueOf(input));
        if (validate(line, board)) {
            // got result
            if (line == n - 1)
                ret.add(new LinkedList<>(board));
            // con't search
            else if (line<n - 1)
                dfs(n, line+1, board, ret);
        }
        Arrays.fill(input, '.');
        board.set(line, String.copyValueOf(input));
    }
}

public boolean validate(int line, List<String> board){
    int n = board.get(line).indexOf('Q');
    for (int i = 0; i<line; i++) {
        int m = board.get(i).indexOf('Q');
        if (m == n || m == n + line - i || m == n - (line - i)) return false;
    }
    return true;
}
```

### 22. Generate Parentheses

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

把思考过程理解成一个完全二叉树，每向左走一格为加个左括号，向右走一格为加个右括号。深度优先回溯搜索即可（其实任何形式的搜索都可以）。

```java
public List<String> generateParenthesis(int n) {
    ArrayList<String> result = new ArrayList<String>();
    dfs(result, "", n, n);
    return result;
}

public void dfs(ArrayList<String> result, String s, int left, int right){
    if(left > right) return;
    if(left == 0 && right == 0){
        result.add(s);
        return;
    }
    if(left>0) dfs(result, s+"(", left - 1, right);
    if(right>0) dfs(result, s+")", left, right - 1);
}
```

### 47. Permutations II

这个题目的剪枝很有趣，为了恰当剪枝需要事先排序，然后比如说有三连出现的数字，它只能以1, 11, 111形式各出现一次。比如说[1,1,1,2]，当bfs完两个1之后，遇到第三个1需要跳过，为什么呢？因为递归[1,1]子树时已经搜索过[1,1,1]了。所以每一个子树——在这个例子中是[1]子树的第二位搜索的时候看到第三个1需要跳过，因为之前第二个1已经被跳过了，符合(nums[i - 1] == nums[i] and not used[i - 1])的条件——这一轮的i-1个值没用过，说明上一轮搜索的时候已经用过了。39/40、78/90两组题目和46/47两道题用的是完全一样的技巧，不再赘述了。

```py
def perm(self, nums, current, result, used):
    if len(current) == len(nums):
        result.append(current[:])
        return
    else:
        for i in range(0, len(nums)):
            if used[i]:
                continue
             Key: no repeat
            if i > 0 and nums[i - 1] == nums[i] and not used[i - 1]:
                continue
            used[i] = True
            current.append(nums[i])
            self.perm(nums, current, result, used)
            current.pop()
            used[i] = False

def permuteUnique(self, nums):
    ret, cur, used = [], [], []
    nums = sorted(nums)
    for i in nums:
        used.append(False)
    self.perm(nums, cur, ret, used)
    return ret
```

### 212. Word Search I

Word Search II真做不下去，但如果只是搜一个单词的话还是比较简单的，跟走迷宫完全一样的回溯搜索啦

```java
static boolean[][] visited;
public boolean exist(char[][] board, String word) {
    visited = new boolean[board.length][board[0].length];
    for(int i = 0; i < board.length; i++){
        for(int j = 0; j < board[i].length; j++){
            if((word.charAt(0) == board[i][j]) && search(board, word, i, j, 0)){
                return true;
            }
        }
    }
    return false;
}

private boolean search(char[][]board, String word, int i, int j, int index){
    if(index == word.length()){
        return true;
    }
    if(i >= board.length || i < 0 || j >= board[i].length || j < 0 || board[i][j] != word.charAt(index) || visited[i][j]){
        return false;
    }
    visited[i][j] = true;
    if(search(board, word, i-1, j, index+1) ||
       search(board, word, i+1, j, index+1) ||
       search(board, word, i, j-1, index+1) ||
       search(board, word, i, j+1, index+1)){
        return true;
    }
    visited[i][j] = false;
    return false;
}
```

### 864. Shortest Path to Get All Keys

```md
We are given a 2-dimensional grid. "." is an empty cell, "#" is a wall, "@" is the starting point, ("a", "b", ...) are keys, and ("A", "B", ...) are locks.

We start at the starting point, and one move consists of walking one space in one of the 4 cardinal directions.  We cannot walk outside the grid, or walk into a wall.  If we walk over a key, we pick it up.  We can't walk over a lock unless we have the corresponding key.

For some 1 <= K <= 6, there is exactly one lowercase and one uppercase letter of the first K letters of the English alphabet in the grid.  This means that there is exactly one key for each lock, and one lock for each key; and also that the letters used to represent the keys and locks were chosen in the same order as the English alphabet.

Return the lowest number of moves to acquire all keys.  If it's impossible, return -1.
```

本身走迷宫问题基本都是简单的回溯搜索，但这个题目他存在一个钥匙和大门，我们按照正常人的逻辑，列出来几个逻辑：

1. 没有开门之前就视同于墙
2. 而且在没有拿到钥匙之前，最好是不要走回头路，否则的话那完全可以在这个地方无限打转转
3. 拿到钥匙之后，允许走回头路，所以visited数组清零

不要被这个题目吓着，这题没有非常难，当然具体实现还是可以有很多奇技淫巧的

1. state用位数组来表示捡到了哪些钥匙
2. 用queue不是寻求最短路径的精神，heapq更适合搜索最短路径
3. 好马不吃回头草哦，所以用一个`memo(newState, x, y)`储存已经检索过的状态

```py
class Solution(object):
    def shortestPathAllKeys(self, grid):
        final, m, n, si, sj = 0, len(grid), len(grid[0]), 0, 0
        for i in range(m):
            for j in range(n):
                if grid[i][j] in "abcdef":
                    # 位数组
                    final |= 1 << ord(grid[i][j]) - ord("a")
                elif grid[i][j] == "@":
                    si, sj = i, j
        q, memo = [(0, si, sj, 0)], set()
        while q:
            moves, i, j, state = heapq.heappop(q)
            if state == final:
                return moves
            for x, y in ((i - 1, j), (i + 1, j), (i, j - 1), (i, j + 1)):
                if 0 <= x < m and 0 <= y < n and grid[x][y] != "#":
                    if grid[x][y].isupper() and not state & 1 << (ord(grid[x][y].lower()) - ord("a")):
                        # 撞到没开的门了，视同于墙
                        continue
                    # 捡到钥匙
                    newState = ord(grid[x][y]) >= ord("a") and state | 1 << (ord(grid[x][y]) - ord("a")) or state
                    if (newState, x, y) not in memo:
                        memo.add((newState, x, y))
                        heapq.heappush(q, (moves + 1, x, y, newState))
        return -1
```

## 2. Combinatorics

组合问题略微烧脑，高中学的排列组合在这里会派上用场

### 31. Next Permutation

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers. If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order). The replacement must be inplace, do not allocate extra memory.

这个题目需要理解排列的性质，找到一个最长的从头递增序列，把序列中倒数第二个数字替换成从右至左的第一个大于它的数字，然后把这个数字右侧的序列排序即可。

```java
public void nextPermutation(int[] nums) {
    int l = nums.length;
    if (l<2) return;
    int i;
    boolean perm = false;
    // if it's on descending order, no permutation possible
    for (i = l - 2; i>=0; i--)
        if (nums[i]<nums[i+1]) {
            perm = true;
            break;
        }
    if (!perm) Arrays.sort(nums);
    else {
        int temp = nums[i], j;
        for (j = l - 1; j>=0; j--)
            if (nums[j]>temp)
                break;
        nums[i] = nums[j];
        nums[j] = temp;
        int[] ret2 = Arrays.copyOfRange(nums, i+1, l);
        Arrays.sort(ret2);
        for (j = i+1; j<l; j++)
            nums[j] = ret2[j - i - 1];
    }
}
```

### 60. Permutation Sequence

基本是直接按题意去思考

1. n个数字一共有`n!`种排列
2. 所以第一个数字就是`k/((n-1)!)`，然后把`k%((n-1)!)`赋值给新的k
3. 在待处理数字组中去掉已经用过的数字
4. 如此往复直到n=0

```py
import math
class Solution:
    def getPermutation(self, n, k):
        numbers = range(1, n+1)
        permutation = ''
        k -= 1
        while n > 0:
            n -= 1
            # get the index of current digit
            n_fac = math.factorial(n)
            index = k // n_fac
            k = k % n_fac
            permutation += str(numbers[index])
            # remove handled number
            numbers.remove(numbers[index])
        return permutation
```

### 89. Gray Code

The gray code is a binary numeral system where two successive values differ in only one bit. Given a nonnegative integer n representing the total number of bits in the code, print the sequence of gray code. A gray code sequence must begin with 0.

这题目简直是脑筋急转弯，可以分成两段理解，首位是0的如何变化，那么首位是1的数字要想每一位变动只相差1个数字，那就只能按照首位0的序列倒序过来。

```java
public List<Integer> grayCode(int n) {
    List<Integer> ret = new ArrayList<>();
    if (n == 0){
        ret.add(0);
        return ret;
    } else {
        // Recursion
        List<Integer> last = grayCode(n - 1);
        // On reverse order
        for (int i = last.size() - 1; i>=0; i--)
            last.add(last.get(i) + (1<<(n-1)));
        return last;
    }
}
```

## 3. Breadth-First Search

BFS思考起来比DFS要简单很多，而且对于很多问题是秒杀……尤其走迷宫BFS一般比较好写

### 207 \& 210. Course Schedule I \& II

这题目虽然是拓扑排序，BFS秒杀，然而仍然要注意，正向BFS是不如逆向BFS的，因为这题目的实质是寻找图里的环，含环图可以有个开端，但一定没有结尾

```py
def canFinish(self, numCourses, prerequisites):
    que, hashmap, deg, tot = [], {}, [0] * numCourses, 0
    # Prepare a list pre-req edges
    for i in prerequisites:
        if i[0] not in hashmap:
            hashmap[i[0]] = [i[1]]
        else:
            hashmap[i[0]].append(i[1])
        deg[i[1]] += 1
     Topo-sort from the ends -- ends have deg of 0
    for i in range(0, numCourses):
        if deg[i] == 0:
            que.append(i)
            tot += 1
    ret = []
    # BFS to Topo-sort
    while len(que) > 0:
        cur, que = que[0], que[1:]
        ret.append(cur)
        if cur in hashmap:
            for i in hashmap[cur]:
                # only classes w/o following classes can be traversed
                deg[i] -= 1
                if deg[i] == 0:
                    que.append(i)
                    tot += 1
    ret.reverse()
    if tot == numCourses:
        return ret
    else:
        return []
```

### 269. alien dictionary

There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of words from the dictionary, where words are sorted lexicographically by the rules of this new language. Derive the order of letters in this language.

For example, Given the following words in dictionary,

```py
[
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]
```

The correct order is: "wertf".

Note: You may assume all letters are in lowercase. If the order is invalid, return an empty string. There may be multiple valid order of letters, return any one of them is fine.

主要难点在读题，他这个是和以前做过的题目略有不同的，题目的意思是外星人的字母顺序与人类不同，但外星人提供了他们的字母排序算法，你要根据这个算法来求外星人语言的字母顺序

其实就是个简单的拓扑排序去BFS，烦人的地方在于这个图你要自己画，他这个答案为了速度是选用的邻接矩阵，我个人是不太赞赏的，空间复杂度忒不和谐

```java
private final int N = 26;
public String alienOrder(String[] words) {
    boolean[][] adj = new boolean[N][N];
    int[] visited = new int[N];
    buildGraph(words, adj, visited);

    StringBuilder sb = new StringBuilder();
    for(int i = 0; i < N; i++) {
        if(visited[i] == 0) {                 // unvisited
            if(!dfs(adj, visited, sb, i)) return "";
        }
    }
    return sb.reverse().toString();
}

public boolean dfs(boolean[][] adj, int[] visited, StringBuilder sb, int i) {
    visited[i] = 1;                            // 1 = visiting
    for(int j = 0; j < N; j++) {
        if(adj[i][j]) {                        // connected
            if(visited[j] == 1) return false;  // 1 => 1, cycle
            if(visited[j] == 0) {              // 0 = unvisited
                if(!dfs(adj, visited, sb, j)) return false;
            }
        }
    }
    visited[i] = 2;                           // 2 = visited
    sb.append((char) (i + 'a'));
    return true;
}

public void buildGraph(String[] words, boolean[][] adj, int[] visited) {
    Arrays.fill(visited, -1);                 // -1 = not even existed
    for(int i = 0; i < words.length; i++) {
        for(char c : words[i].toCharArray()) visited[c - 'a'] = 0;
        if(i > 0) {
            String w1 = words[i - 1], w2 = words[i];
            int len = Math.min(w1.length(), w2.length());
            for(int j = 0; j < len; j++) {
                char c1 = w1.charAt(j), c2 = w2.charAt(j);
                if(c1 != c2) {
                    adj[c1 - 'a'][c2 - 'a'] = true;
                    break;
                }
            }
        }
    }
}
```

### 310. Minimum Height Trees

这题的题眼是把原题变形成拓扑排序，确切说就是从1度的叶子开始往下剥，一直剥到“芯”

1. 初始化：对每个节点赋值度数
2. 从度数为1的叶子往里剥
3. 每剥一层把内层度数-1，然后这一层的所有叶子成为新的queue
4. 最内层即为所求

```py
class Solution(object):
    def findMinHeightTrees(self, n, edges):
        if n <= 1:
            return [0]
        degrees = [0] * n
        graph = {x:[] for x in xrange(n)}
        for p in edges:
            degrees[p[1]] += 1
            degrees[p[0]] += 1
            graph[p[1]].append(p[0])
            graph[p[0]].append(p[1])
        queue = [x for x in xrange(0, n) if degrees[x] == 1]
        ret = []
        while queue:
            temp = []
            ret = queue[:]
            for x in queue:
                for n in graph[x]:
                    degrees[n] -= 1
                    if degrees[n] == 1:
                        temp.append(n)
            queue = temp
        return ret
```

### 126 & 127. Word Ladder I / II

Given two words (beginWord and endWord), and a dictionary's word list, find all shortest transformation sequence(s) from beginWord to endWord, such that:

1. Only one letter can be changed at a time
2. Each transformed word must exist in the word list. Note that beginWord is not a transformed word.

Note:

- Return an empty list if there is no such transformation sequence.
- All words have the same length.
- All words contain only lowercase alphabetic characters.
- You may assume no duplicates in the word list.
- You may assume beginWord and endWord are non-empty and are not the same.

```py
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]
```

Output:

```py
[
  ["hit","hot","dot","dog","cog"],
  ["hit","hot","lot","log","cog"]
]
```

这题的思路是很无聊的，无非是BFS和DFS而已，难点：

1. 两个字符串有一个char不同：这题大家用的都是笨方法，n^26
2. 用一个parents<son, parent>储存从前向后的BFS所见到的顺序
    1. key是变化后的单词，value是它的来源
3. 曾经在parents里出现过一次的单词是不允许出现循环的
4. 用update函数更新parents
5. 用一轮反向DFS整理最后的结果：
    1. r in res：r是从前向后的，但搜索的顺序是从后向前的

```py
def findLadders(self, beginWord, endWord, wordList):
    dic = set(wordList)
    level = {beginWord}
    parents = collections.defaultdict(set)
    while level and endWord not in parents:
        next_level = collections.defaultdict(set)
        for node in level:
            for char in string.ascii_lowercase:
                for i in range(len(beginWord)):
                    n = node[:i] + char + node[i+1:]
                    # 1. new word in wordList
                    # 2. no cycle in ladder
                    if n in dic and n not in parents:
                        next_level[n].add(node)
        level = next_level
        parents.update(next_level)
    res = [[endWord]]
    while res and res[0][0] != beginWord:
        res = [r.append(p) for r in res for p in parents[r[0]]]
    return res
```

### 785. Is Graph Bipartite

传统拓扑排序题，思考BFS并不难，但要注意边界条件：

1. 用+-1标色，不需要01标色
2. 上一轮已经标色过的点不需要再理会
3. 每一轮遍历遇到两个相邻点颜色一样就return False

```py
class Solution(object):
    def isBipartite(self, graph):
        n, colored = len(graph), {}
        for i in range(n):
            if i not in colored and graph[i]:
                colored[i] = 1
                q = collections.deque([i])
                while q:
                    cur = q.popleft()
                    for nb in graph[cur]:
                        if nb not in colored:
                            colored[nb] = -colored[cur]
                            q.append(nb)
                        elif colored[nb] == colored[cur]:
                            return False
        return True
```

### 787. Cheapest Flights Within K Stops

实际是实现一个Dijkstra算法

1. Python奇技淫巧：defaultdict实现dict[dict[]]
2. 用优先队列实现，优先级为迄今为止的travel cost

```py
class Solution(object):
    def findCheapestPrice(self, n, flights, src, dst, k):
        f = collections.defaultdict(dict)
        for a, b, cost in flights:
            f[a][b] = cost
        heap = [(0, src, k + 1)]
        while heap:
            cost, cur, k = heapq.heappop(heap)
            if cur == dst:
                return cost
            if k > 0:
                for dest in f[cur]:
                    heapq.heappush(heap, (cost + f[cur][dest], dest, k - 1))
        return -1
```

### 417. Pacific Atlantic Water Flow

```md
Given an m x n matrix of non-negative integers representing the height of each unit cell in a continent, the "Pacific ocean" touches the left and top edges of the matrix and the "Atlantic ocean" touches the right and bottom edges.

Water can only flow in four directions (up, down, left, or right) from a cell to another one with height equal or lower.

Find the list of grid coordinates where water can flow to both the Pacific and Atlantic ocean.

Note:
The order of returned grid coordinates does not matter.
Both m and n are less than 150.
Example:

Given the following 5x5 matrix:

  Pacific ~   ~   ~   ~   ~ 
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * Atlantic
```

这题目的题眼是太平洋和大西洋不是两个角，而是分别指代两条边，由每个节点BFS必然超时，所以从“每个节点向外递减”逆向思考为“从大洋向内递增”

1. 从太平洋和大西洋分别向里BFS找到（太平洋是向右向下，大西洋是向左向上）不可再增加的边
2. 对两个集合求交集即可

```py
class Solution(object):
    def pacificAtlantic(self, matrix):
        if not matrix: return []
        m, n = len(matrix), len(matrix[0])
        def bfs(reachable_ocean):
            q = collections.deque(reachable_ocean)
            while q:
                (i, j) = q.popleft()
                for (di, dj) in [(0,1), (0, -1), (1, 0), (-1, 0)]:
                    if 0 <= di+i < m and 0 <= dj+j < n and (di+i, dj+j) not in reachable_ocean \
                            and matrix[di+i][dj+j] >= matrix[i][j]:
                        q.append( (di+i,dj+j) )
                        reachable_ocean.add( (di+i, dj+j) )
            return reachable_ocean
        pacific  = set ( [ (i, 0) for i in range(m)]   + [(0, j) for j  in range(1, n)]) 
        atlantic = set ( [ (i, n-1) for i in range(m)] + [(m-1, j) for j in range(n-1)]) 
        return list( bfs(pacific) & bfs(atlantic) )
```
