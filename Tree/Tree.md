# Tree

## Inorder, Preorder & Postorder Traversal

### Inorder

> 思路 1：递归，瞬秒

```python
class Solution(object):
    def inorderTraversal(self, root):
        if root == None:
            return []
        res = []
        self.inorder(root,res)
        return res

    def inorder(self,root,res):
        if root == None:
            return
        self.inorder(root.left,res)
        res.append(root.val)
        self.inorder(root.right,res)
```

> 思路 2：迭代

先一股脑把左边一条线全部push到底（即走到最左边），然后node最终为None了就开始pop stack了，然后因为pop出来的每一个node都是自己这棵树的root，所以看看它有没有右孩子，没有那肯定继续pop，有的话自然而然右孩子是下一个要被访问的节点。

```python
class Solution(object):
    def inorderTraversal(self, root):
        res = []
        if not root:
            return res
        stack = []
        node = root
        while node or (len(stack) > 0):
            if node:
                stack.append(node)
                node = node.left
            else:
                node = stack.pop()
                res.append(node.val)
                node = node.right
        return res
```

### Preorder

> 思路 1：递归，瞬秒

```python
class Solution(object):
    def preorderTraversal(self, root):
        if root == None:
            return []
        res = []
        self.preorder(root,res)
        return res

    def preorder(self,root,res):
        if root == None:
            return
        res.append(root.val)
        self.preorder(root.left,res)
        self.preorder(root.right,res)
```

> 思路 2：迭代

这个没多难，注意弹入栈的顺序即可，先右后左

```python
class Solution(object):
    def preorderTraversal(self, root):
        res = []
        if not root:  
            return res  
        stack = []  
        stack.append(root)
        while(len(stack) > 0):  
            node = stack.pop()  
            res.append(node.val)  
            if node.right:  
                stack.append(node.right)  
            if node.left:  
                stack.append(node.left)  
        return res
```

### Postorder

> 思路 1：递归

```python
class Solution(object):
    def postorderTraversal(self, root):
        def postOrder(root):
            if not root : return
            postOrder(root.left)
            postOrder(root.right)
            res.append(root.val)
        res = []
        postOrder(root)
        return res
```

> 思路 2：迭代

其实思路就一句话，后序遍历是左右中，因为我们第一个放进去的肯定是中（即root），所以我们逆向思维考虑一下，我们按照中右左的顺序放进去，然后返回res[::-1]就行了。这其实跟[leetcode第144题](https://github.com/apachecn/LeetCode/blob/master/docs/Leetcode_Solutions/144._binary_tree_preorder_traversal.md)是一样的思路

```python
class Solution(object):
    def postorderTraversal(self, root):
        res = []
        if not root:
            return res
        stack1 = []
        stack1.append(root)
        while len(stack1) > 0:
            node = stack1.pop()
            res.append(node.val)
            if node.left:
                stack1.append(node.left)
            if node.right:
                stack1.append(node.right)
        return res[::-1]
```

### 105 & 106 & 889. Construct Binary Tree from Preorder and Inorder Traversal (Inorder and Postorder Traversal) (Preorder and Postorder Traversal)

这题目实际是在考察对前序和中序遍历的理解，前序遍历的话最左侧的项是root，以此去寻找中序遍历数组中的root，中序遍历数组里root的左边是左子树，右边是右子树，注意python里`pop(0)`是弹出最左侧，`pop()`是弹出最右侧

```py
def buildTree(self, preorder, inorder):
    if inorder:
        ind = inorder.index(preorder.pop(0))
        root = TreeNode(inorder[ind])
        root.left = self.buildTree(preorder, inorder[:ind])
        root.right = self.buildTree(preorder, inorder[ind+1:])
        return root
```

106的话和105类似，只不过改成了pop掉postorder的最后一项，而且需要注意，因为是从右向左pop，需要先构造右子树，再构造左子树，这个顺序不能搞错

```py
def buildTree(self, inorder, postorder):
    if not inorder or not postorder:
        return None
    root = TreeNode(postorder.pop())
    inorderIndex = inorder.index(root.val)
    root.right = self.buildTree(inorder[inorderIndex+1:], postorder)
    root.left = self.buildTree(inorder[:inorderIndex], postorder)
    return root
```

后序遍历的最后一项是根节点，而倒数第二项明显就是右儿子

```py
def constructFromPrePost(self, pre, post):
    if not pre or not post: return None
    root = TreeNode(pre[0])
    if len(post) == 1: return root
    idx = pre.index(post[-2])
    root.left = self.constructFromPrePost(pre[1: idx], post[:(idx - 1)])
    root.right = self.constructFromPrePost(pre[idx: ], post[(idx - 1):-1])
    return root
```

### 173. Binary Search Tree Iterator

这题目实际是用stack模拟中序遍历……

1. 先把所有把左孩子压入stack，直到左边为空
2. 然后开始取node
3. 如果node有右孩子，则同样要把node的右孩子的所有左孩子全部append入stack

```py
class BSTIterator(object):
    def __init__(self, root):
        self.stack = []
        while root:
            self.stack.append(root)
            root = root.left

    # @return a boolean, whether we have a next smallest number
    def hasNext(self):
        return len(self.stack) > 0

    # @return an integer, the next smallest number
    def next(self):
        node = self.stack.pop()
        x = node.right
        while x:
            self.stack.append(x)
            x = x.left
        return node.val
```

### 230. Kth Smallest Element in a BST

继续用stack模拟中序遍历……

1. 先把所有把左孩子压入stack，直到左边为空
2. 然后开始取node
3. 如果node有右孩子，则同样要把node的右孩子的所有左孩子全部append入stack

```py
class Solution:
    # @param {TreeNode} root
    # @param {integer} k
    # @return {integer}
    def kthSmallest(self, root, k):
        stack = []
        while root or stack:
            while root:
                stack.append(root)
                root = root.left
            root = stack.pop()
            k -= 1
            if k == 0:
                return root.val
            root = root.right
```

## 各种递归基础题

树是最简单的数据结构，主要是因为一般不会用迭代来处理树的内容，只有递归的话比较好想

### 98. Validate Binary Search Tree

实际上就是每次往下看，node都确保被夹在一个范围。

```python
class Solution:
    def isValidBST(self, root):
        return self.validity(root, -2**32, 2**32)

    def validity(self, root, left, right):
        if not root:
            return True
        if root.val >= right or root.val <= left:
            return False
        return self.validity(root.left, left, root.val) \
                and self.validity(root.right, root.val, right)
```

### 100. Same Tree

```python
class Solution:
    def isSameTree(self, p, q):
        if not p and not q: return True
        if not p or not q: return False
        if p.val == q.val:
            return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
        return False
```

### 101. Symmetric Tree

两棵树symmetric， 有几种可能：

- 均为none，symmetric
- 左孩子，右孩子都不存在，并且值相等，symmetric
- 右子树和另一棵树的左子树相等，左子树和另一颗树的右子树相等

```python
class Solution(object):
    def isSymmetric(self, root):
        if not root:
            return True
        return self.symmetric(root.left, root.right)

    def symmetric(self, l1, l2):
        if not l1 and not l2:
            return True
        if not l1 or not l2:
            return False
        if l1.val == l2.val:
            return self.symmetric(l1.left, l2.right) and self.symmetric(l1.right, l2.left)
        else:
            return False
```

### 104. Maximum Depth of Binary Tree

```python
class Solution(object):
    def maxDepth(self, root):
        if not root:
            return 0
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
```

### 108 & 109. Convert Sorted Array / List to Binary Search Tree

递归

- nums为空，return None
- nums非空，nums[n/2]为中间元素，根结点，nums[:mid]为左子树， nums[mid+1:]为右子树

```python
class Solution(object):
    def sortedArrayToBST(self, nums):
        if not nums:
            return None
        if nums:
            mid = len(nums) / 2
            root = TreeNode(nums[mid])
            root.left = self.sortedArrayToBST(nums[:mid])
            root.right = self.sortedArrayToBST(nums[mid+1:])
            return root
```

链表版本没区别，无非是用个快慢指针

```python
class Solution(object):
    def sortedListToBST(self, head):
        return self.listToBST(head, None)

    def listToBST(self, head, tail):
        if head == tail:
            return None
        else:
            slow = head
            fast = head
            while fast != tail and fast.next != tail:
                slow = slow.next
                fast = fast.next.next
            root = TreeNode(slow.val)
            root.left = self.listToBST(head, slow)
            root.right = self.listToBST(slow.next, tail)
            return root
```

### 110. Balanced Binary Tree

递归，判断左右子树最大高度差不超过1且左右子树均为平衡树

```python
class Solution(object):
    def isBalanced(self, root):
        def height(node):
            if not node:
                return 0
            return 1 + max(height(node.left), height(node.right))
        if not root:
            return True
        return abs(height(root.left) - height(root.right)) <= 1 \
                and self.isBalanced(root.left) \
                and self.isBalanced(root.right)
```

### 111. Minimum Depth of Binary Tree

这个题目的陷阱在于如果一个节点只有一侧有儿子，你是不能返回min(left, right)的，因为此时有一侧返回值是0

```python
class Solution(object):
    def minDepth(self, root):
        if not root:
            return 0
        left = self.minDepth(root.left)
        right = self.minDepth(root.right)
        if left == 0 or right == 0:
            return 1 + left + right
        else:
            return 1 + min(left, right)
```

### 124. Binary Tree Maximum Path Sum

这题名为难题实际上没多难……重点是体会递归关系

```py
class Solution:
    def maxPathSum(self, root):
        res = [-2**32]
        self.helper(root, res)
        return res[0]

    def helper(self, root, res):
        if not root:
            return 0
        left = max(0, self.helper(root.left, res))
        right = max(0, self.helper(root.right, res))
        res[0] = max(left + right + root.val, res[0])
        return max(left, right) + root.val
```

### 129. Sum Root to Leaf Numbers

```py
class Solution:
    def sumNumbers(self, root):
        return self.calSum(root, 0)

    def calSum(self, root, curSum):
        if root == None:
            return 0
        else:
            curSum = curSum * 10 + root.val
            if root.left == None and root.right == None:
                return curSum
            else:
                return self.calSum(root.left, curSum) + self.calSum(root.right, curSum)
```

### 226. Invert Binary Tree

基础题，要注意速度

```py
class Solution:
    def invertTree(self, root):
        if not root: return None
        root.left, root.right = self.invertTree(root.right), self.invertTree(root.left)
        return root
```

### 285. Inorder Successor in BST

货真价实的简单题，BST中序遍历是单调递增的，所以实际就是在BST里寻找比p大的最小值咯

```py
def inorderSuccessor(self, root, p):
    ret = None
    while root:
        if p.val < root.val:
            ret = root
            root = root.left
        else:
            root = root.right
    return ret
```

### 297 / 449. Serialize and Deserialize Binary Tree / BST

这题其实没说要你把二叉树弄成啥样……这个解法就是复杂版前序遍历而已

```py
class Codec:
    def serialize(self, root):
        def preOrder(node):
            if node:
                vals.append(node.val)
                preOrder(node.left)
                preOrder(node.right)
            else:
                vals.append('#')
        vals = []
        preOrder(root)
        return vals

    def deserialize(self, data):
        def build():
            val = next(vals)
            if val == '#':
                return None
            else:
                node = TreeNode(val)
                node.left = build()
                node.right = build()
                return node
        vals = iter(data)
        return build()
```

```py
class Codec:
    def serialize(self, root):
        vals = []
        def preOrder(node):
            if node:
                vals.append(node.val)
                preOrder(node.left)
                preOrder(node.right)
        preOrder(root)
        return ' '.join(map(str, vals))

    # O(N) since each val run build once
    def deserialize(self, data):
        vals = collections.deque(int(val) for val in data.split())
        def build(minVal, maxVal):
            if vals and minVal < vals[0] < maxVal:
                val = vals.popleft()
                node = TreeNode(val)
                node.left = build(minVal, val)
                node.right = build(val, maxVal)
                return node
        return build(float('-infinity'), float('infinity'))
```

### Ternary Expression to Binary Tree

这题目leetcode里没有，可能因为太简单？两个解法，一个是栈解法：

1. 一开始推进去一个树节点
2. 每次向右推两格
    1. 遇到问号呢，就把当前栈顶节点的左子树加上这个节点
    2. 遇到冒号的话，先往外弹一个，然后如果遇到右子树满着的节点，一路从栈往外弹，直到遇到右子树为空的节点
    3. 每次循环的最后把节点推进去

另一个是递归，问号后面的【整个字符串】是左子树，冒号后面的【整个字符串】是右子树呗

```java
public TreeNode convert(String expr) {
    char[] exp = expr.toCharArray();
    if (exp.length == 0)
        return null;
    TreeNode root = new TreeNode(exp[0]);
    Stack<TreeNode> stack = new Stack<>();
    stack.push(root);
    for (int i = 1; i < exp.length; i += 2) {
        TreeNode node = new TreeNode(exp[i + 1]);
        if (exp[i] == '?')
            stack.peek().left = node;
        if (exp[i] == ':') {
            stack.pop();
            while (stack.peek().right != null)
                stack.pop();
            stack.peek().right = node;
        }
        stack.push(node);
    }
    return root;
}

Node convertExpression(char[] expression, int i) {
    if (i >= expression.length)
        return null;
    Node root = new Node(expression[i]);
    ++i;
    if (i < expression.length && expression[i]=='?')
        root.left = convertExpression(expression, i+1);
    else if (i < expression.length)
        root.right = convertExpression(expression, i+1);
    return root;
}
```

### 543. Diameter of Binary Tree

这个做法似乎是唯一解？但反正在二叉树问题里时间复杂度是很不漂亮的一种了

```py
def diameterOfBinaryTree(self, root):
    self.best = 1
    def depth(root):
        if not root: return 0
        depL = depth(root.left)
        depR = depth(root.right)
        self.best = max(self.best, depL + depR + 1)
        return max(depL, depR) + 1
    depth(root)
    return self.best - 1
```

### 572. Subtree of Another Tree

```py
def isSubtree(self, s, t):
    def helper(s, t, root):
        if not s and not t:
            return True
        if not s or not t:
            return False
        if s.val == t.val:
            return (helper(s.left, t.left, False) and helper(s.right, t.right, False)) or (helper(s.left, t, True) or helper(s.right, t, True))
        else:
            if root:
                return helper(s.left, t, True) or helper(s.right, t, True)
            else:
                return False
    return helper(s, t, True)
```

## DFS

### 112 / 3. Path Sum I/II

```python
class Solution(object):
    def hasPathSum(self, root, sum):
        if not root:
            return False
        if root.left or root.right:
            return self.hasPathSum(root.left, sum-root.val) or self.hasPathSum(root.right, sum-root.val)
        else:
            return root.val == sum
```

```python
class Solution(object):
    def pathSum(self, root, sum):
        res = []
        self.auxPathSum(root, sum, [], res)
        return res

    def auxPathSum(self, root, sum, cur_list, cur_lists):
        if not root:
            return
        if sum == root.val and not root.left and not root.right:
            cur_lists.append(cur_list + [root.val])
            return
        if root.left:
            self.auxPathSum(root.left, sum - root.val, cur_list + [root.val], cur_lists)
        if root.right:
            self.auxPathSum(root.right, sum - root.val, cur_list + [root.val], cur_lists)
```

## 各种LCA

### 235 / 6. Lowest Common Ancestor of BST / Binary Tree

BST的话要注意方向，如果不是BST的话要注意他是如何变换状态的

```py
def lowestCommonAncestor(self, root, p, q):
    if root.val < p.val and root.val < q.val:
        return self.lowestCommonAncestor(root.right, p, q)
    elif root.val > p.val and root.val > q.val:
        return self.lowestCommonAncestor(root.left, p, q)
    else:
        return root

def lowestCommonAncestor(self, root, p, q):
    if root is None or root is p or root is q:
        return root
    else:
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        if left and right:
            return root
        elif left:
            return left
        elif right:
            return right
```

## Trie

### 208. Implement Trie (Prefix Tree)

Trie最好是不要用递归写法，太长，容易错，迭代其实不难解决

```py
class TrieNode:
    def __init__(self):
        self.word=False
        self.children={}

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node=self.root
        for i in word:
            if i not in node.children:
                node.children[i]=TrieNode()
            node=node.children[i]
        node.word=True

    def search(self, word):
        node=self.root
        for i in word:
            if i not in node.children:
                return False
            node=node.children[i]
        return node.word

    def startsWith(self, prefix):
        node=self.root
        for i in prefix:
            if i not in node.children:
                return False
            node=node.children[i]
        return True
```

## Binary Search Tree

### 700 & 701 & 450. BST 增删查

```py
class Solution:
    def searchBST(self, root, val):
        if root and val < root.val:
            return self.searchBST(root.left, val)
        elif root and val > root.val:
            return self.searchBST(root.right, val)
        return root

    def insertIntoBST(self, root, val):
        if not root:
            return TreeNode(val)
        if val < root.val:
            root.left = self.insertIntoBST(root.left, val)
        else:
            root.right = self.insertIntoBST(root.right, val)
        return root

    def deleteNode(self, root, key):
        if root is None: return
        if root.val == key:
            if root.right and root.left:
                right = root.right
                while right is not None and right.left is not None:
                    right = right.left
                right.left = root.left
                return root.right
            else:
                if root.left:
                    return root.left
                elif root.right:
                    return root.right
                else:
                    return None
        elif key > root.val:
            root.right = self.deleteNode(root.right, key)
        else:
            root.left = self.deleteNode(root.left, key)
        return root
```

### 95 & 96. Unique Binary Search Trees

Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1 ... n.

```md
Input: 3
Output:
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
Explanation:
The above output corresponds to the 5 unique BST's shown below:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

这题目的题眼就是BST的性质：每个节点的左子树都比他小，右子树都比他大

```py
def generateTrees(self, n):
    if n == 0:
        return []
    def generate(first, last):
        trees = []
        for root in range(first, last+1):
            # B/c this is BST, left sub-tree < root < right sub-tree
            for left in generate(first, root-1):
                for right in generate(root+1, last):
                    node = TreeNode(root)
                    node.left = left
                    node.right = right
                    trees.append(node)
        return trees or [None]
    return generate(1, n)
```

注意96题因为有时间限制，单纯递归是不管用的，95因为要逐个生成每个树，所以不用递归也不可能

我们首先定义`G(n)`是长度n的序列能生成的独特BST树数量，`F(i,n)`是以i为root，从1到n的序列能生成的独特BST树数量，所以`G(n)=sum(F(i,n))`，而我们观察95题，得到`F(i,n) = G(i-1) * G(n-i)`

```java
public int numTrees(int n) {
    int [] G = new int[n+1];
    G[0] = G[1] = 1;
    for(int i=2; i<=n; ++i) {
        for(int j=1; j<=i; ++j) {
            G[i] += G[j-1] * G[i-j];
        }
    }
    return G[n];
}
```

### 99. Recover Binary Search Tree

Two elements of a binary search tree (BST) are swapped by mistake. Recover the tree without changing its structure.

```md
Input: [1,3,null,null,2]

   1
  /
 3
  \
   2

Output: [3,1,null,null,2]

   3
  /
 1
  \
   2
```

这题看着有点难，但实际上是利用的中序遍历的性质

1. BST的中序遍遍历必为顺序，那么每次遍历的时候记录prev跟cur
2. 第一次遇到`prev > cur`的话记录下来需要交换的`first = prev`
3. 第二次记录下来`second = cur`
4. 结尾处交换一下`first`和`second`即可

```java
TreeNode firstElement = null;
TreeNode secondElement = null;
TreeNode prevElement = new TreeNode(Integer.MIN_VALUE);
public void recoverTree(TreeNode root) {
    // In order traversal to find the two elements
    traverse(root);
    // Swap the values of the two nodes
    int temp = firstElement.val;
    firstElement.val = secondElement.val;
    secondElement.val = temp;
}
private void traverse(TreeNode root) {
    if (root == null)
        return;
    traverse(root.left);
    if (firstElement == null && prevElement.val >= root.val)
        firstElement = prevElement;
    if (firstElement != null && prevElement.val >= root.val)
        secondElement = root;
    prevElement = root;
    traverse(root.right);
}
```
