# Binary Tree

#  94. Binary Tree Inorder Traversal
**<font color=red>难度: 中等</font>**

## 刷题内容

> 原题连接

* https://leetcode.com/problems/binary-tree-inorder-traversal/description/

> 内容描述

```

Given a binary tree, return the inorder traversal of its nodes' values.

Example:

Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
Follow up: Recursive solution is trivial, could you do it iteratively?
```

## 解题方案

> 思路 1


递归，瞬秒


```python
class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        res = []
        if not root:
            return res
        if root.left: 
            res.extend(self.inorderTraversal(root.left))
        res.append(root.val)
        if root.right:
            res.extend(self.inorderTraversal(root.right))
        return res
```
> 思路 2

或者我们可以先写一下中序遍历的函数，然后一个一个贴上去

```python
class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
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
> 思路 3

迭代

先一股脑把左边一条线全部push到底（即走到最左边），然后node最终为None了就开始pop stack了，然后因为pop出来的每一个node都是自己这棵树的root，所以看看它有没有右孩子，没有那肯定继续pop，有的话自然而然右孩子是下一个要被访问的节点。


```python
class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
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

#  96. Unique Binary Search Trees
**<font color=red>难度: 中等</font>**

## 刷题内容

> 原题连接

* https://leetcode.com/problems/unique-binary-search-trees/description/

> 内容描述

```
Given n, how many structurally unique BST's (binary search trees) that store values 1 ... n?

Example:

Input: 3
Output: 5
Explanation:
Given n = 3, there are a total of 5 unique BST's:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

## 解题方案

> 思路 1


参照此处hint:

https://shenjie1993.gitbooks.io/leetcode-python/096%20Unique%20Binary%20Search%20Trees.html


首先明确n个不等的数它们能构成的二叉搜索树的种类都是相等的。而且1到n都可以作为二叉搜索树的根节点，当k是根节点时，它的左边有k-1个不等的数，它的右边有n-k个不等的数。以k为根节点的二叉搜索树的种类就是左右可能的种类的乘积。用递推式表示就是 h(n) = h(0)*h(n-1) + h(1)*h(n-2) + ... + h(n-1)h(0) (其中n>=2) ，其中h(0)=h(1)=1，因为0个或者1个数能组成的形状都只有一个。从1到n依次算出h(x)的值即可。此外这其实就是一个卡特兰数，可以直接用数学公式计算，不过上面的方法更加直观一些。


```python
class Solution(object):
    def numTrees(self, n):
        """
        :type n: int
        :rtype: int
        """
        dp = [1 for i in range(n+1)]
        for i in range(2, n+1):
            s = 0
            for k in range(i):
                s += dp[k]*dp[i-k-1]
            dp[i] = s
        return dp[-1]
```
