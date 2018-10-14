# Uber

## 电面

### 系统设计

1. Brief system design: given a coordinate, find top K nearest bus stations (geohash + NlogK)

### Coding

1. LC 49
2. Find minimal `m * N` that only have 1 or 0 in `m * N`

```java
    private int getNumber(int n){
        int res=-1;
        for (int i=7;;i+=7){
            String s=String.valueOf(i);-google 1point3acres
            int idx=0;
            while (idx<s.length()){
                if(s.charAt(idx)=='0' || s.charAt(idx)=='1'){
                    idx++;
                }else{
                    break;
                }
                if(idx==s.length()){
                    //System.out.println("String :"+i);
                    res=i;
                    return res;
                }
            }
        }
    }
```

1. LRU cache
2. Rate limiter -- LC 359

就是用queue去存当前时间，每次call这个function就去比较queue.top，用一个while循环，直到queue的top和当前时间差值小于1秒，然后把当前时间塞进queue，我记得利口有一道类似的

```java
class Logger {
    Queue<Node> q = new ArrayDeque<>();
    HashMap<String,Integer> dict = new HashMap<>(); // ip, called Times.
    public Logger() {}
    public boolean ipLimiter(double timestamp, String ip, int callTimes){
        while ( !q.isEmpty() && timestamp - q.peek().time >= 1){
            Node t = q.poll();
            dict.remove(t.ip);
        }
        if(!dict.contains(ip)){  
            if(callTimes > 100){
                return false;
            }
            q.offer(new Node(timestamp, ip));
            dict.add(ip,callTimes);
            return true;
        }else{
            if(dict.get(ip) + callTimes <= 100){
                dict.put(ip, dict.get(ip) + callTimes);
                return true;
            }
        }
        return false;
    }
    private static class Node{
        double time;
        String ip;
        public Node(double t, String ip){
            this.time = t;
            this.ip = ip;
        }
    }
}
```

就是一个函数在给定时间不能调用太多次，拿个queue记下来时间戳就好了。并不知道C++获得Unix timestamp是啥函数。给他说我查下，是time(0）. 一亩-三分-地，独家发布

然后被要求编译测试。写了个for 循环一直call

接下来要控制时间call，但是C++并没有sleep。编译器报错他就放弃了

要求加synchronized和加static, private protected这些access modifier. 

1) massive requests. 怎么改进？我说可以让queue存timestamp和count，这样存储省下许多并且估计处理器cache可以放下

2) each request takes processing time. Offload processing to other machine

3) different task takes different time, limit based on start time and current running. 最近提交的个数+虽然提交很久还没跑完的。把queue改成list就是了，让写了代码

http://blog.gssxgss.me/not-a-simple-problem-rate-limiting/

3. K closest elements with x in an unsorted array
4. LC 229 Boyer-Moore Majority Vote
5. LC 629
6. LC 36
7. Trie
8. LC 53
9. Two Sum
10. Word Break II 变种，不需要返回所有的可以组成的string，而是给一个isSentence(String input) API，判断这个input是否可以被分解，但是做法是差不多的
11. 从database A migrate data到database B. A里有n个primary keys，到B后希望只有1个key，怎么来生成一个unique key?
12. 两个interval list 并集

a = [[0, 2], [5, 10], [13, 23], [24, 25]]
b = [[1, 5], [8, 12], [15, 18], [20, 24]]
Expected output: [[1, 2], [5, 5], [8, 10], [15, 18], [20, 24]]

13. LC 658
14. Travel Buddy (Buddy List) （出自于airbnb） 就是找几个user 想去的相同城市 超过 half 的就是buddy list 基本上一样，写完就把pad 关了。topo sort 解决，其实也不用 就是数数有几个相同就好了，毫无算法可言。
15. 印度大姐，黑白格迷宫 四个方向 有起点有重点，找有没有路径，因为扯简历扯了半个小时，题写了20分钟，不过 bfs 解决 10分钟吧。问了复杂度，我说不是 2^n 大姐问N 是啥，我说N 是迷宫各自数 m\*n 大姐说不对，后来想想难道只是 m\*n 因为我用Hashset 去掉已经访问过的？
16. Calculator I
17. LC 437 binary tree 找所以路径和等于target，打印出来那些paths
18. LC 20
19. LC 199
20. LC 33
21. 给一个数组要求返回所有可能的和, allow duplicate

e.g. [1,2,3] => [0,1,2,3,3,4,5,6]

22. Skyline problem
23. LC 3
24. LC 10
25. 判断一个input数组是不是valid preorder BST

```py
INT_MIN = -2**32
def canRepresentBST(pre):
    # Create an empty stack
    s = []
    # Initialize current root as minimum possible value
    root = INT_MIN
    # Traverse given array
    for value in pre:  
        #NOTE:value is equal to pre[i] according to the  
        #given algo
        # If we find a node who is on the right side
        # and smaller than root, return False
        if value < root :
            return False
        # If value(pre[i]) is in right subtree of stack top,  
        # Keep removing items smaller than value
        # and make the last removed items as new root
        while(len(s) > 0 and s[-1] < value) :
            root = s.pop()
        # At this point either stack is empty or value
        # is smaller than root, push value
        s.append(value)
    return True
  
# Driver Program
pre1 = [40 , 30 , 35 , 80 , 100]
print "true" if canRepresentBST(pre1) == True else "false"
pre2 = [40 , 30 , 35 , 20 ,  80 , 100]
print "true" if canRepresentBST(pre2) == True else "false"
```

26. LC 51
27. 生成一个n+1*n+1的图，value是1-n*n,连线是按照slash的方向，每条外边也要连上
123
456
789
对应slash的内联：2-4 3-5 5-7 6-8 
28. 实现给两点输出所有路径的方法
29. LC 200
30. 
// - - - - - - -
//| | |x| | | | |
// - - - - - - -
//| | |x|x|x|x| |
// - - - - - - -
//| | | | | | | |
// - - - - - - -
//|x|x| | | | |D|
// - - - - - - -
//| |x| | | | | |
// - - - - - - -
// Given: 1. board 2. coordinate of the destination
// Output: API
// api_input: coordinate of the start position
// api_output: #steps of shortest path from start to destiation
31. LC 44
32. LC 91
33. 用string 建数
"+12"                  +
             变成      1  2

“++123"          变成             +
                             +      3
                          1   2

34. breaking bad

Given an array of strings `words` and a string `name`, find one substring of `name` that matches any word in `words`.
Put brackets around the matching substring in `name` and capitalize the first letter.

Sample input:
    words = ['B', 'Ar', 'O']
    name = 'aaron'

Output:
    a[Ar]on

Followup. Find all possible ways of breaking bad.

Sample input:
    words = ['B', 'Ar', 'O']
    name = 'aaron'

Output:
    ['a[Ar][O]n', 'aaron', 'a[Ar]on', 'aar[O]n']

35. breaking bad

输入: 长度限制 = 20,"Hey Alice, your Uber is arriving now!" 
输出: ["Hey Alice, (1/3)", "your Uber is (2/3)", "arriving now! (3/3)"]

36. LC 706

之后是followup这个就比较坑了，要求实现一个功能updateall，可以把所有的key都update成这个新的值，我确实不知道hashtable有这样的功能，需要常数时间。正确的做法是设置一个global value，每个value，包括global value都要有last updated timestamp。这样每次update都update timestamp，get的时候就比较一下global的和真正value的timestamp就可以了。楼主一开始确实是这么想的，但是因为刚写完处理conflict的代码，所以觉得这并不是O(1)。就没说，后来说了global value和timestamp。面试官说这就是正确的思路，但是我觉得这样不是O(1)啊，面试官说不用考虑哪些细节，hash function够好就可以，好吧。。。可能这里是挂点吧

37. LC 34
38. LC 75
39. LC 102/103
40. LC 79
41. find a element in a sorted array that index == value, average O less than O(n). follow-up: array has duplicates.

https://www.geeksforgeeks.org/find-fixed-point-value-equal-index-given-array-duplicates-allowed/

42. 题目是假如对于Uber eat，有一大堆记录，每条记录有id，订了什么食物，是几点订的。其中几点定的只有0-23这24个可能。
比如：
(0, apple, 0)
(1, apple, 0)
(2, orange, 1). Waral 博客有更多文章,
(3, orange, 0)

让找出每个小时的top K selling food。

难度不大，我是对0-23点每个小时建一个hash map，里面key是food，value是被订的次数，然后遍历这些记录更新这些map，最后对从每个小时的map中找出top k的food。

在每个小时的map里找top K的food的时候是用min heap的方法做的

43. 面试官问了一个graph的问题，一个存各种状态的数组，每一个状态都有自己的各种property以及nextState。需要自己画一个graph给出所有可能的path。dfs bfs都可以，但后面的题目还要累计计算某些property，所以用dfs比较合适。
44. LC 39
45. word break 那道题
46. Number of Connected Components in an Undirected Graph
47. 判断一个tree是不是bst. 1point 3acres 论坛
48. 求bst中第n大的数
49. 基本的BFS找最短距离题目。给一个2D matrix，里面有一些位置是障碍物，不能pass。然后给一个destination的坐标，求所有其他点到destination的最短距离。
50. system design: autocomplete/typeahead
51. LC 239
52. LC 56
53. LC 591
54. LC 252/253
55. 然后题目我是用preorder traversal生成一个String来代表这个树(or 子树)，空子节点用特殊符号表示，Node之间用“|”隔开，然后放到一个Set里，然后递归检查用“|”的数量来判断tree的size，再看set是否已有相同的String，以此确定是否有duplicate。
后来walk through the solution时发现，preorder会导致额外的递归调用，时间复杂度O(N^2)，然后我就加了个Map<TreeNode, String>来减少对同一节点重复计算String，这样在traversal过程中，如果map里已经有答案了就直接返回String。这样时间、空间复杂度分别是O(N), O(N)。

面完之后，回忆起来想到其实用postOrder做可以省掉那个Map的空间，但是总体时间空间复杂度不变，觉得这一轮应该稳了。 
56. 第一题，给一个整型数组，把0元素移到前面，其他元素移到后面。算是原题吧。楼主脑子进水卡了一下，之前做的都是移到后面，所以有点不习惯。先写了一个开辟新空间的，后来才写in space的. 1point3acres
第二题，货币转换，这题楼主没见过，不知道是不是原题，求地里人给个链接或者思路让我学习下。
要求有两个函数，update 是输入两个货币的进制转换，例如 "USD", "CNY", 6.8 这个代表1USD = 6.8 CNY。 还可以有"CNY", "KRW", 20 代表1人民币=20韩元。. from: 1point3acres 
convert函数输入"USD", "KRW", 2， 表示问你2美元可以得到多少韩元
    public static void update(String cur1, String cur2, double rate) {

    }
    public static double convert(String cur1, String cur2, double amt) {

    }


楼主说用一个map把所有可能性存起来。例如<USD, [[CNY, 6.8], [KRW, 6.8 * 20]]>, 小哥说这样太耗空间，问我有什么好方法，我想不出让他提示，他说了一通····我没听懂····让他给个例子，他写了个USD --111.27-> JPY -->10.10-> KRW， 我还是没懂···他又说那你可以反过来想看行不行，我想了下还是不懂怎么样，感觉小哥有点不耐烦加上时间不多了，就让我问他问题了
现在还没结果不过应该是挂了···怪楼主自己刷题不精，第一题都卡了一下把自己彻底搞慌了。
地里大神教下第二题怎么写。

1. 不用编程语言自带的 dict 设计一个键值存储类，要求添加、查找都是常数时间复杂度，注意处理 hash 值冲突的情况
2. LC 287
3. LC 359
4. LC 767
5. LC 380
6. LC 528
7. 两个链表形式数字的加法
8. Count Island
9. LC 290/291
10. LC 418
11. LC 17
12. LC 636
13. LC 542
14. LC 317
15. LC 286
16. Tree
17. LC 74
18. LC 270
19. LC 97
20. LC 36
21. x^y
22. 第一道题：给定“UBERCAB"这个string，然后给另外一个string， 求需要多少个”UBERCAB"这样的单词，才能组成输出的单词，比如”bear car“，那么久输出2，如果是“Amazon”，那么就输出-1，应该“UBERCAB"里面没有”Z"
23. LC 267
24. 
一副无限多的牌（A, 1, ...., K），一直摸（相当于无限的stream输入），手里有顺子（5张）就打出去（print同时remove）。例子：
6
4
7
9
6
10
8       --->    6, 7, 8, 9, 10
2
5
3      --->    2, 3, 4, 5, 6