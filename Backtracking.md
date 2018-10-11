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

### 扯淡迷宫问题

Suppose you have a 2-D grid. Each point is either land or water. There is also a start point and a goal. There are now keys that open up doors. Each key corresponds to one door. Implement a function that returns the shortest path from the start to the goal using land tiles, keys and open doors. Implement a function that returns the shortest path from the start to the goal using land tiles, keys and open doors.

本身走迷宫问题基本都是简单的回溯搜索，但这个题目他存在一个钥匙和大门，我们按照正常人的逻辑，列出来几个逻辑：

1. 没有开门之前就视同于墙
2. 而且在没有拿到钥匙之前，最好是不要走回头路，否则的话那完全可以在这个地方无限打转转
3. 拿到钥匙之后，允许走回头路，所以visited数组清零

不要被这个题目吓着，这题没有非常难

```py
def solve(self, maze):
    ret, path, keyring, visited = [], [], {}, self.initVisited(maze)
    for i in range(0, len(maze)):
        for j in range(0, len(maze[i])):
            if maze[i][j] == '2':
                self.walk(maze, i, j, keyring, path, ret, visited)
    return ret

def initVisited(self, maze):
    ret = []
    for i in maze:
        temp = []
        for j in i:
            temp.append(False)
        ret.append(temp)
    return ret

def walk(self, maze, y, x, keyring, path, ret, visited):
    if y < 0 or y >= len(maze) or x < 0 or x >= len(maze[0]):
        return                       out of board
    pt = maze[y][x]
    if visited[y][x] or pt == '0':
        return                       visited
    if pt == '3':
        path.append([y, x])
        ret = list(path)
        print(ret)
        return                       found dest
    if len(path) > len(ret) > 0:
        return                       longer path than old

    if pt.isalpha():
        if pt.isupper() and pt.lower() not in keyring:
            return                   key missing
        elif pt.islower():
            if pt not in keyring:
                keyring[pt] = 1      add key to keyring
                visited = self.initVisited(maze)

    visited[y][x] = True
    path.append([y, x])
    self.walk(maze, y, x + 1, keyring, path, ret, visited)
    self.walk(maze, y + 1, x, keyring, path, ret, visited)
    self.walk(maze, y, x - 1, keyring, path, ret, visited)
    self.walk(maze, y - 1, x, keyring, path, ret, visited)
    visited[y][x] = False
    path.pop()
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
     Prepare a list pre-req edges
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
     BFS to Topo-sort
    while len(que) > 0:
        cur, que = que[0], que[1:]
        ret.append(cur)
        if cur in hashmap:
            for i in hashmap[cur]:
                 only classes w/o following classes can be traversed
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
