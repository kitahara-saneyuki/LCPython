# Linked List

## 1. 各种反转链表

### 206. Reverse Linked List

反转链表母题，需要熟练掌握各种变量的变化顺序，追踪两个变量法

```java
public ListNode reverseList(ListNode head) {
    ListNode newHead = null;
    while (head != null){
        ListNode headNext = head.next;
        head.next = newHead;
        newHead = head;
        head = headNext;
    }
    return newHead;
}
```

### 92. Reverse Linked List II

反转链表有很多种方式，上一题只是其中一种，这次我们来试试第二种，实际只追踪一个变量

```java
public ListNode reverseBetween(ListNode head, int m, int n) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode startL = dummy;
    for (int i = 0; i<m-1; i++)
        startL = startL.next;
    ListNode cur = startL.next;
    for (int i = m; i<n; i++){
        ListNode curNext = cur.next;
        cur.next = curNext.next;
        curNext.next = startL.next;
        startL.next = curNext;
    }
    return dummy.next;
}
```

### 25. Reverse Nodes in k-Group

1. 假设起点为i，每次前推k个node
2. 然后翻转[i, i+k]

```py
def reverseKGroup(self, head, k):
    dummy = jump = ListNode(0)
    dummy.next = l = r = head

    while True:
        count = 0
        # use r to locate the range
        while r and count < k:
            r = r.next
            count += 1
        # if size k satisfied, reverse the inner linked list
        if count == k:
            pre, cur = r, l
            for _ in range(k):
                # standard reversing
                cur.next, cur, pre = pre, cur.next, cur
            # connect two k-groups
            jump.next, jump, l = pre, l, r
        else:
            return dummy.next
```

### 24. Swap Nodes in Pairs

简单题，注意顺序即可

```java
public ListNode swapPairs(ListNode head) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode prev = dummy;
    ListNode cur;
    ListNode move;
    while (prev.next != null && prev.next.next != null){
        cur = prev.next;
        move = cur.next;
        prev.next = move;
        cur.next = move.next;
        move.next = cur;
        prev = cur;
    }
    return dummy.next;
}
```

### 61. Rotate List

```md
Input: 1->2->3->4->5->NULL, k = 2
Output: 4->5->1->2->3->NULL
Explanation:
rotate 1 steps to the right: 5->1->2->3->4->NULL
rotate 2 steps to the right: 4->5->1->2->3->NULL
```

这题的题眼在于k有可能会大于list长度……所以需要先遍历一轮list求长度，然后取余，然后rotate

```java
public ListNode rotateRight(ListNode head, int n) {
    if (head == null || head.next == null)
        return head;
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode fast = dummy,slow = dummy;

    int i;
    // Get the total length
    for (i = 0; fast.next != null; i++)
        fast = fast.next;
    // Get the i - n % i th node
    for (int j = i - n % i; j > 0; j--)
        slow = slow.next;
    // Do the rotation
    fast.next = dummy.next;
    dummy.next = slow.next;
    slow.next = null;

    return dummy.next;
}
```

## 2. 快慢指针

### 141 & 142. Linked List Cycle I & II

这俩题快慢指针典型题，1的话就是快慢指针会在环路中相撞

```java
public boolean hasCycle(ListNode head) {
    if(head == null)
        return false;
    ListNode slow = head, fast = head.next;
    while(fast != slow){
        if(fast==null || fast.next==null)
            return false;
        slow = slow.next;
        fast = fast.next.next;
    }
    return true;
}
```

找端点这题需要一点思量

1. 假定环路长度是N，环路起点是A
2. 那么快慢指针相遇时候，慢指针走了A+B，快指针走了2A+2B
3. 所以推论出来A+B+N=2A+2B，所以N=A+B，那么A+N=A+A+B
4. 所以再找个第三根指针跟慢指针同步向前走，两者相遇的时候就找到了A

```java
public ListNode detectCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while(fast != null && fast.next != null) {
        fast = fast.next.next;
        slow = slow.next;
        if (slow == fast) {
            while (head != slow) {
                head = head.next;
                slow = slow.next;
            }
            return slow;
        }
    }
    return null;
}
```

### 143. Reorder List

Given 1->2->3->4->5, reorder it to 1->5->2->4->3.

这题见过就不难：

1. 用快慢指针找到中点，从中点将链表截成两段
2. 把后半段链表反转
3. 把两个链表merge

```py
# @return A tuple containing the heads of the two halves
def _splitList(head):
    fast = head
    slow = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next
        fast = fast.next
    middle = slow.next
    slow.next = None
    return head, middle

# Reverses in place a list.
# @return Returns the head of the new reversed list
def _reverseList(head):
    last = None
    currentNode = head
    while currentNode:
        nextNode = currentNode.next
        currentNode.next = last
        last = currentNode
        currentNode = nextNode
    return last

# Merges in place two lists
# @return The newly merged list.
def _mergeLists(a, b):
    tail = a
    head = a
    a = a.next
    while b:
        tail.next = b
        tail = tail.next
        b = b.next
        if a:
            a, b = b, a
    return head

class Solution:
    # @param head, a ListNode
    # @return nothing
    def reorderList(self, head):
        if not head or not head.next:
            return
        a, b = _splitList(head)
        b = _reverseList(b)
        head = _mergeLists(a, b)
```

### 234. Palindrome Linked List

快慢指针求中点，然后用慢指针作为中点往后遍历，前半部分是本题的难点，如果希望不改动链表的话，需要从头到尾再从尾到头翻转两次

```java
def isPalindrome(self, head):
    slow, fast = head, head
    rev = None
    while fast and fast.next:
        fast = fast.next.next
        rev, rev.next, slow = slow, rev, slow.next
    if fast: tail = slow.next
    else: tail = slow
    while rev:
        if rev.val != tail.val: return False
        slow, slow.next, rev = rev, slow, rev.next
        tail = tail.next
    return True
```

### 160. Intersection of Two Linked Lists

1. 双指针按同一速度推进两截链表A-C和B-C
2. 当他们都走到尽头时交换位置，让他们走一个A-C-B和B-C-A
3. 如此他们的长度差就被抹掉，交汇处就是两链表交点

```python
# @param two ListNodes
# @return the intersected ListNode
def getIntersectionNode(self, headA, headB):
    if headA is None or headB is None:
        return None

    pa = headA # 2 pointers
    pb = headB

    while pa is not pb:
        # if either pointer hits the end, switch head and continue the second traversal,
        # if not hit the end, just move on to next
        pa = headB if pa is None else pa.next
        pb = headA if pb is None else pb.next

    return pa # only 2 ways to get out of the loop, they meet or the both hit the end=None

# the idea is if you switch head, the possible difference between length would be countered.
# On the second traversal, they either hit or miss.
# if they meet, pa or pb would be the node we are looking for,
# if they didn't meet, they will hit the end at the same iteration, pa == pb == None, return either one of them is the same, None
```

## 3. 其他杂题

### 2. Add Two Numbers

Input: (2 > 4 > 3) + (5 > 6 > 4)

Output: 7 > 0 > 8

这个题目的难点在于corner case多而且庞杂，但实际上不需要转换成十进制数字，因为他本身提供的链表就是从小到大的，符合加法的计算习惯，生加即可

```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode cur = dummy;
    int c = 0;
    while (l1 != null || l2 != null){
        int a = 0, b = 0, d = 0;
        // a, b
        if (l1 != null) {
            a = l1.val;
            l1 = l1.next;
        }
        if (l2 != null) {
            b = l2.val;
            l2 = l2.next;
        }
        // c is carrier
        if (a + b + c >= 10) {
            d = (a + b + c) % 10;
            c = 1;
        } else {
            d = a + b + c;
            c = 0;
        }
        cur.next = new ListNode(d);
        cur = cur.next;
    }
    if (c != 0) {
        cur.next = new ListNode(c);
        cur = cur.next;
    }
    cur.next = null;
    return dummy.next;
}
```

### 23. Merge k Sorted Lists

题目很直接就不再重复叙述了，这题最直截了当的想法是分治调用merge 2 sorted lists的函数，而后者是个人就会写

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    if (l1 == null && l2 == null) return null;
    else if (l1 == null) return l2;
    else if (l2 == null) return l1;
    else {
        ListNode dummy = new ListNode(0), cur = dummy;
        ListNode cur1 = l1, cur2 = l2;
        while (cur1 != null && cur2 != null){
            if (cur1.val <= cur2.val){
                cur.next = cur1;
                cur1 = cur1.next;
            } else {
                cur.next = cur2;
                cur2 = cur2.next;
            }
            cur = cur.next;
        }
        if (cur1 == null)
            cur.next = cur2;
        else if (cur2 == null)
            cur.next = cur1;
        return dummy.next;
    }
}

public ListNode mergeKLists(ListNode[] lists) {
    if (lists.length == 0)
        return null;
    else if (lists.length == 1)
        return lists[0];
    else if (lists.length == 2)
        return mergeTwoLists(lists[0], lists[1]);
    else {
        ListNode[] l1 = Arrays.copyOfRange(lists, 0, lists.length/2);
        ListNode[] l2 = Arrays.copyOfRange(lists, lists.length/2, lists.length);
        return mergeTwoLists(mergeKLists(l1), mergeKLists(l2));
    }
}
```

### 138. Copy List with Random Pointer

这题目的题眼就是用一个map把链表的每个node存好……

```java
public RandomListNode copyRandomList(RandomListNode head) {
    if (head == null) return null;
    Map<RandomListNode, RandomListNode> map = new HashMap<RandomListNode, RandomListNode>();
    // loop 1. copy all the nodes
    RandomListNode node = head;
    while (node != null) {
        map.put(node, new RandomListNode(node.label));
        node = node.next;
    }
    // loop 2. assign next and random pointers
    node = head;
    while (node != null) {
        map.get(node).next = map.get(node.next);
        map.get(node).random = map.get(node.random);
        node = node.next;
    }
    return map.get(head);
}
```

### 147. Insertion Sort List

这题还真不是一个简单题，需要注意的就是如果插入位置后面的最小值就是插入位置本身的话，就不需要再移动

```py
def insertionSortList(self, head):
    dummy = ListNode(0)
    dummy.next = head
    inscur = dummy;
    while inscur.next != None:
        min = 2**32
        cur = inscur
        tempNode = None
        while cur.next != None:
            if cur.next.val < min:
                min = cur.next.val
                tempNode = cur
            cur = cur.next
        if tempNode != inscur:
            temp = tempNode.next.next
            tempNode.next.next = inscur.next
            inscur.next = tempNode.next
            tempNode.next = temp
        inscur = inscur.next
    return dummy.next
```

### 148. Sort List

这题反而不难。。。注意细节

```py
def sortList(self, head):
    """
    :type head: ListNode
    :rtype: ListNode
    """
     Corner case
    if head == None or head.next == None:
        return head
     find middle node using fast & slow pointer
    slow = head
    fast = head
    while fast.next != None and fast.next.next != None:
        slow = slow.next
        fast = fast.next.next
    a = head
    b = slow.next
     truncate list by middle node
    slow.next = None
     recursion
    a = self.sortList(a)
    b = self.sortList(b)
     use merge sort
    return self.mergeTwoLists(a, b)
```
