# 谷歌onsite面经

## 2018下半年

### [10/07/2018][1]

第一轮：给两个字母串 str1 = “ABABZ”, str2 = "ABZ", 判断str1能否用str2中的字符拼成，如果能，最少的步数是多少？例子，从str2中取“A”，“B”，“A”，“B”，“Z”一共五步，但如果取“AB”，“ABZ”只需要两步。follow up，如果str2中有duplicate，BFS shortest path问题

第一个题的解释，换一种说法，就是从str2里每次可以取出一个substring，需要取多少次才能拼成str1.在没有duplicate的情况下，直接比较下一个字符串是否相同。

先要判断能不能成。如果str1里有字符不在str2，就不能成。
能成的情况下最多len(strt1)肯定可以嘛，所以要求的是最少需要几次。

问了大神，第一题比较好的思路是 记录每个字符在str2里的位置，再把str1里的字符过一遍，如果在str2的位置不连续就要增加步数

第二轮：in-order traversal, 给N，能否print出in order顺序第N个数。follow up，若已知每个node下面有多少个descendent，如何更快print出第N个数，binary search。具体实现的时候和面试官讨论了比较多的细节，也要了提示。

第三轮：同义词，给出很多pair的同义词，判断两个词是否为同义词，dfs，union find

第四轮：这一轮就是LC新出的920，如果能提前看过思路会清晰很多。中间讨论的时间花了太多，code没能写完，只实现了random play（我一开始写了O（N）的，如果之前看过类似的题，可以轻松给出O（1）解决方案），follow up的问题也没问到（组合数）。中途发现面试官的脸色也不太好，最后催着把code补充完

第四轮的complexity，题目的要求是写一个class，比如说Player，实现playNextSong这个method的复杂度是O（1）。

### [10/04/2018][2]

第一轮是一个中国大哥，第一题是一个数组，在某个位置前元素单调递增，然后单调递减，就是那种元素大小像山一样形状的数组，然后求最大最小值，用binary search做，然后第二题是比较二叉树是否相同，问了一下时间复杂度啥的 LC 33 & 81
第二轮是考察dp的，类似与有多少条路径，从起点到终点，在一个二维grid上，leetcode有相似的题，然后如果遇到障碍或者必须经过某些位置的话咋办 LC 62 & 63
第三轮是考察二叉树，自己定义tree node，然后自己把二叉树各种遍历方法写一下，递归的和非递归的，这题没写完很慌 LC 94 & 144 & 145
第四题类似于number of islands，不过题目条件变复杂了在面试官指导下就挺快开始写代码了，然后follow up问了一下bfs相关问题啥的，不难
这几轮面试官都很友好，都是难度不大的题入手然后不断深入问下去

不知道结果怎样呢，毕竟一题没写完，碰到的tree的题目挺多可能因为sunnyvale做搜索的组挺多？然后题目可能会改变一些条件让题目变复杂增加点难度

### [10/07/2018][3]

第一轮.三姐, 给两个string, 一个比另一个多一个字母, 找出多出来的. follow up: 如果string是乱序怎么处理. 都写了白板. 第二题, 蠡口刘巴斯
第二轮. 国人大哥. 利口尓酒屋. 没做过, follow答得不好
吃饭. 食堂一般
第三轮. 不知道什么国家的大哥. 问了Java基础知识. 题目带时间戳的hashmap. 面经题. 讨论clean up的实现. 感觉答得不好. 希望比O(n)快
第四轮.国人. 感觉面得还可以. 给double Linkedlist然后给一个Input, input是一个array of nodes, 这些nodes都是之前double linkedlist里面的, 可能是乱序. 让你找出有多少个连续的段. 比如[n5, n1, n2, n3, n9] -> 3. n1,n2,n3是连续的, n5一段, n9一段
第五轮. 国人. 简单第一题一个grid找shortest path. BFS. 之后follow up比较难. 告诉你所有target坐标, 要找出一个从给定起点出发, 连接所有target的最短路线. 讨论了一下感觉是每个线段的permutation后的最短和. 他想讨论但是我把permutation代码写了...

### [10/08/2018][4]

第一个：. from: 1point3acres 
说有很多loud speaker，每个loud speaker在一些时间区间会发出声音。每个区间的声音响度可能不同。比如对于某一个loud speaker，发声音的间隔是[3, 5], [ 7, 10], [13, 15]，响度分别为50,30,40。.本文原创自1point3acres论坛
问这些loud speaker发声的总体效果。
其实就是区间的merge，如果两个speaker同时响了，响取较大的那个

第二个先问了给一个binary search tree，再给一个target value，如何找到树中和这个value的差最小的node。然后下一步问了说如果有全世界的机场，然后给定你现在的当前位置，如何找到方圆X公里内的所有机场。
大概和他讨论了一下kd tre

第三了我如何在string里inplace的删除一个char！！！
太简单了，不过要求是bug free。他提醒了几个corner case，基本上就bug free了。。

接着问了在一个2D 数组中如何找到从上到下的和是最小的路径

第四个人，问我现在假设google 要做一个project叫exact search，就是说query一个问题然后google返回exact的答案。假设现在google已经有了50B的问题和对应的答案，那么这个系统该如何设计。. from: 1point3acres 

我说应该用hash map，把每一个question都做hash。他说对的。然后感觉还比较轻松，因为这个人一步步的提问方式把问题渐渐深入：如果内存有限该怎么办，如果一台机器的硬盘也有限怎么办，基本思路就是分布式系统，在硬盘上对每一个问题再就行一遍hash。然后他继续问至多和至少需要多少台机器来实现这个系统，然后他给了每台机器的内存，硬盘空间。接着问如果给了ethernet的反应时间，同时有多少query这个系统就会崩

### [08/15/2018][5]

今天刚完成三轮onsite加面  附上面经面试时间2：15pm - 4：30 PM     8/14/2018  地点    MTV面试官按面试顺序 白人 ， 白人  ， 三哥+国人shadow

1. 高频题 给你一个String target 还有一个List<String> dictionary 要求你输出-----所有给target字符串 添加字符之后等于dictionary 的单词

比如 target ----> google    List<goooooogle, ddgoogle,  abcd, googles>   return List<goooooogle, ddgoogle, googles> 
2.开放性design题  要求你随机生成一个Maze(迷宫)
3.medium偏向easy题  给你一个String abcdefg  和一个int row = 2 要求你按顺序打印字符
a    c     e     g            打印结果 acegbdf                          
  b     d     f
如果row = 3
a           e                打印结果  aebdfcg
  b     d      f
     c               g

// 今天刚完成面试，还不确定结果，如果只看面经的话可以止步了，之后写的都是我个人的经验总结，只给大家作为借鉴，实力不够不敢误人子弟。
. visit 1point3acres for more.
首先我要详细的阐述一下我个人的答题流程（目前只针对google）. 1point3acres
1.repeat question 
2.clear question. From 1point 3acres bbs
3.confirm input data / output result. Waral 博客有更多文章,
4.abstract question 
5.ALGO+DataStructure
6.time/space
7.write code
7.1 keep communcation
7.2 summary code
8 explain 
9 run test case. Waral 博客有更多文章,
10 think about unit test case
. From 1point 3acres bbs
解释一下我的答题流程希望对大家有帮助， 首先我们一定要知道google不是只要你写好看的代码，同时考察你思考的方式和过程，这需要靠交流来展现，所以交流很重要（我的两个google recruiter都跟我说要注重交流 交流 交流)
之前面试的人说面试第一步是要跟面试官针对问题深入探讨，讨论各种情然后再写代码，我不是非常同意，我个人认为，第一步不是讨论这个问题，而是你去重复这个问题！他说的问题你用自己的话简单的总结 然后告诉他我们现在面对一个什么问题，之后我们再跟面试官对细节进行讨论 这就是第二步讨论问题。 
第三步是确定输入输出的参数，这个很重要，相同的问题不同的入参导致的结果就是解题算法可能不一样，如果他没有确定要求那我会按照我喜欢的来，如果面试官说输入的参数只可以是什么 . 1point3acres
第四步 抽象化这个问题，题刷多了你就会发现 什么最少的钱招聘工人，连接岛屿，最短路径，乱七八糟的描述 都是图 树 数组的问题，包装的很炫酷而已， 快速的删除那些没用的形容词 不要受到打扰（每个人思维逻辑不一样，你跟我说我们有几个飞机场 有飞机航班 几点起飞，求最快的到某个机场的时间，当我听见飞机 我快速的联想到各种飞机 空姐什么的，跳跃性思维，给我一个跳板我能飞出这个宇宙） 
第五步 当我们抽象化问题之后，基本上就锁定了一部分算法，然后试想这个算法是否可行，（比如一个图 dfs  bfs unionfind  哪个可以需要什么数据结构 这要靠多刷题自我积累）
第六步 如果可以的话，写代码之前 简单的说一下时间 空间复杂度
前六步 每一步都不是自己站在那里想，每一步你都要跟面试官交流，对话内容     以我面经第一题为例子 展示我打流程. more info on 1point3acres
1.我：“我想简单的重复一下我们的问题， 我们有一个blabla 还有一个blabla 想要输出一个blabla 对么？”                   面试官“对的宝贝/不对亲爱的 我们有..... 没有....” “ok 那我们有.....”
2.我：“那如果输入的参数是这个样 我们怎么办，会不会有空字符串啊 亲爱的， 会不会字典里有一样的单词呢？ 宝宝”   面试官“可能有哦，你说的都有可能/ 放心不存在的”
3.我：“honey 输入参数我可以自己定么？ list可以不，还是一定要什么。。。。”   面试官“你长得帅听你的/ 不行我说是什么就是什么”
456.我： 好的，我们现在的有这个和那个，我们要找subsequence 我们问题的重点是找.... 我决定用hashmap<Integer List<String>> 删选我们的字典 然后将长度大于target的单词作为我们的候选单词 然后每个单词compare
因为我们可能存在相同的单词 我们可能需要一个hashset 时间大约是O(xxx) 空间大约是O(xxx)  你觉得可以么 宝贝？“   面试官 ”你真帅·完美答案/可以不错 但是有没有更好的 或者其他的解法么？“ . 一亩-三分-地，独家发布
我： ”当然有，亲爱的 我们可以用Trie数据结构 blabla 但是代码多时间复杂度差不多，我们可以在第一种解法上优化代码  你想要什么姿势？啊不对，是你想要什么算法 我都会哦“     面试官”我要。。。。。“.本文原创自1point3acres论坛
7. 写代码，完成大部分代码才解释 或者完成一部分代码才解释， 最好的方法是你写某些功能之前就提前说了 我现在要干嘛******** 我创建这个HashMap是为了什么  这个变量名是代表什么. 围观我们@1point 3 acres
面试官点头 或者微笑 或者么么哒你 你就可以写了，他要是不理你，你不要生气（他可能在想晚上要吃什么，不是每个面试官都很专业的，不要因为他的行为 影响你的思路和节奏）.1point3acres网
8.完成每一步之后，黑板上就有你的完整代码了，按照顺序 简单的描述一下你的算法流程，这里是什么 那里是什么
9.跑例子
10 提出多种不同的例子 其实就那么几种，字符串很长，字符串很多，字符串空，重复的单词，单词里有特殊字符*&……%￥  

以上是我个人的答题流程，如果对大家有用是我的荣幸，如果有问题可以提出，我会改进，另外我是刚面试完，不知道结果，在这里发表个人经验其实是很有压力的，坑自己没事，坑了别人我会内疚的
现在是我个人的基础总结 如何对面试有帮助
我在地里关于google的面经有一些讨论记忆犹新，一道题是用minHeap 还是maxHeap，当时面经的楼主说错了用什么Heap（我记得清是因为我也不太会）后来关于PriorityQueue的题做了几道 瞬间就发现自己的知识漏洞真是可怕，甚至是后怕。一直以为会了很多算法（貌似会了，其实很多时候是假会 自己骗自己 真的来个变种题 不去仔细思考 结果就是挂 毫无疑问的）
我今天面试中遇到的基础问题
今天面试中 第一个题，当我说用hashmap存的时候 面试官问我一下，hashmap里的key是什么顺序（这题我一直思路很清晰，所以写code时间快 给他很多时间问问题）我说hashmap的key是无序的，面试官点头然后  他问什么Map有序，我说如果你想要 可以用LinkedHashMap 或者 TreeMap 面试官继续点头，然后他问如果用TreeMap 怎么找上一个值 我说可以用ceilingKey 时间复杂度？ TreeMap 基于红黑树 查找删除是logn（三问三答 无缝衔接 ）
因为HashMap<Integer, ArrayList<String>> 用的是Array 面试官继续问 可不可以不用Array 我说可以 ，他说你能用什么来提高性能呢？ 内心冷笑 LinkedList  掐头去尾O（1）时间  面试官Ok

-google 1point3acres
星巴克开始赶人了 话没说完 先发这些
肯定有人问第二题  不知道是不是面经题（我个人没见过）一个很开放性的问题， 我的思路
首先我自己定义 起始点 终止点 然后还有地图的长款（交通后 面试官同意） 然后我用dfs build 一个path 连接start 和 end 
重点是 随机生成方向 而不是按照dfs 四个顺序生成方向 ，除了这个path 其他所有点我把它想成 障碍物 用1表示

之后我可以生成分支（从这个正确的路上）或者 别的地方生成一个路，什么样的无所谓，重点是每次生成的迷宫不同 而且我可以自己定义参数 想生成几个有效的路 或者定义这个迷宫的难度
难度越高 死路越多，想成一个树 从root 到end 只有一个或者几个path  但是 却有很多叶节点
感觉面试官说我的想法很新颖（我画了一个树来解释dfs 和 有效 无效的路 他说喜欢我的树）. 一亩-三分-地，独家发布

### [10/04/2018][6]

第一轮：. more info on 1point3acres
给一个无环图，以及player1的起始点，输出player2的起始点使得player2的得分最高。
得分的定义是最后属于你的点的个数。
规则是每个人走一步，这一步是上一步的所有归你的点的距离为1的邻居。只要某个点没被占领，这个点就归你了。两个人同时可以占领某一个点的话，谁都不得分。所以其实是两个人同时走一步。
一个非常easy的bfs。

第一题是无向无环图。其实只用从player1的邻居为起点分别做bfs就行了，不用从每一个点分别都做bfs，因为没有环。然后BFS时不需要管player1，因为player1无法占领player2这边的点。

第二轮：
处理log，输出top k talkative的用户。talkative的定义是说的词的个数，重复的也算。 来源一亩.三分地论坛. 
稍微处理一下string，然后一个topk的easy题。

第三轮：
merge interval的简单版本。
两个输入，A是一堆没有overlap的interval list，B也是一堆没有overlap的interval list。
返回一个合并了A和B的interval list。

第四轮：. Waral 博客有更多文章,
word search的变种。给一个二维的grid，一个target word。问grid中最多能找到多少个target word。
就是dfs，然后加memo改dp。

感想是面试官很喜欢问你怎么test这个code，所以要想好怎么设计test cases。. 留学申请论坛-一亩三分地
交流很关键，题都不难，面试官想让你写什么你就写什么，我唯一的目的就是为了让面试官开心。

### [10/05/2018][7]

a2[b3[a]] -> abbaaabbaaa
missing range
3sum less than K.1point3acres网
自行车和人的题目

### [10/02/2018][8]

第一轮：

1. 猜字游戏，leetcode原题375, 分析complexity一开始分析错了，但写完代码又重新分析对了。
2. 有点像LC835， 不过是让你找两个图片对应的transform,而且第二个图的1可能比第一个图的1要少，因为移出去了。
3. LC candy变形。

第二轮：

1. 给你一个Node 找tree中这个Node最近的右节点
2. 优化第一问，我说加个next指向他的right, 有点想LC117，然后问题是给你一个Node 插入到这个TREE,不过每个node 都有个next指向， update这个tree。、

第三轮：
1.有点像LC790, 一开始没推出来递推，在面试官指导下推出来，然后follow up是再加一个tile, 递推式怎么变。

四轮：

1. easy找array最小的值 然后找array中比它大的个数。
2. 有点像LC676, 一开始说了按length存，然后他说他复杂了就用了LC最优解。
3. 父母生了很多孩子，找两个人的lowest common ancestor, 虽然看到过面经，但是不太会，而且那时候时间也不多了，就讲了讲思路，感觉用Bi-BFS? 就大概写了pesudo code

### [10/07/2018][9]

倒序层级遍历树 要从最下层开始 按层级输出 面试官想要的答案是改变数据结构 把树变成几个circle的链表 感觉没提前看过很难现场想出来. visit 1point3acres for more.


number of island变体 但是是输出这些所有island里最大的size 这是第一问 第二问是自己选择改变一个0->1 使能输出新的最大的island size 也就是也许可以把两个island连起来之类的
          这个题还是很有意思的 因为要存island的大小和island编号（因为要知道是两个不同的island） 跟面试官讨论了怎么存 我开始想的是建一个coordinate类存到一个新的matrix里 后来讨论了发现不用 只存编号 然后再存一个编号和size的对应关系在一个新的一维数组里即可 anyway这轮还是很有意思感觉面的最好的一轮吧= =



题目挺简单的 给一个area code和area name的对应关系列表 根据这个列表输出给的一组area code的area name 这个题的关键是 area code可能是前面重复的 比如123 -> AZ   1234 - > CA 那么如果有一个input是123456 要输出CA不是AZ 她想要的最优方案也是改变数据结构 把这个变成一个树的结构 当时紧张的脑子一片空白 现在想想是不是trie啊= = 然后第二题是interval overlaps 输出最多数量的overlaps和它对应的数量

面经题 给两个字符串 其中都包含一些/b 代表删除前一个有效字符 输出这两个字符串是否相等 要求复杂度低

### [10/07/2018][10]

第一轮，某白人女：dfs题，秒之，有一些如何优化空间的follow up问题，大概就是把visited数组改成hashset之类的，都不是很难。
. 1point3acres
第二轮，某白人大叔：感觉最差的一轮，上来就觉得不对劲，根本就不好好面我，题目没有写下来，没有clear的input output。大意就是编译器会报很多错误，希望你设计一个算法返回最后5min被某一种错误影响的user的个数。我听完之后一脸黑人问号？？？然后就进入了尬聊10min，不断的在我问“您的意思是不是这样”和他的“不是”之下进行着面试。最后我终于大概明白了他大概是想我design一个什么东西，并且终于明白了输入输出是什么，于是赶紧开始写，卡点写完，讲了一遍，应该起码是正确解，但因为这题太非主流，我也不知道是否是最优的解法（我很怀疑这个人自己是否认真想过这题，可能随手出的，毕竟输入输出都没定义好）

第三轮，某白人大叔：人特别nice，先出了一道巨简单无比的hashmap题，10min写完加跑完test case，然后开始follow up large scale下如何优化，先是怎么样把hashmap搞到disk上存储，然后是假设有100台机器如何搞。总之这轮不是单纯的coding，我觉得我答的还行，他的反应也很积极。

第四轮，某印度小哥：人看起来很nice，出了一道top k，我用heapify+pop k做的，然后他就问heapify为什么O(N),于是我就现场给他讲sift down，然后推导公式，这里要吐个槽，我把公式写出来，按照正常的推导过程都在黑板上写的明明白白了，也讲了半天，他硬是看了好几min才说，那我就当你这个是对的了，我当时就内心吐血（最后得知这小哥原来是DE shaw的我更是不能理解，从hedge fund出来的人数学不至于这个水平吧。。），然后我又给了他一种nlogk的size K heap做法。然后写完结束。主要时间花在推导heapify的时间复杂度上了。

### [09/28/2018][11]

第一轮 和蔼可亲的印度大叔
以下内容需要积分高于 150 才可浏览
.留学论坛-一亩-三分地
给一个字典，typing suggestion的问题， 我说可以建个trie tree顺着找，他问那不是要找很久，能不能instant返回recommendation，我说那就把所有以这个prefix开头的词都存在node里，但是需要很多空间。继续问，需要都存下来吗？每次屏幕上只能显示4个词，我说那就只存最frequent的四个。开始写码，写完了说给5分钟，想出尽可能多的test case，然后边写边讨论了一些edge case。
. 留学申请论坛-一亩三分地


第二轮 白人小哥
以下内容需要积分高于 150 才可浏览

Currency conversion，一个Union Find题。一开始我说建graph然后找，这样是O(N)的lookup，问能不能做到O(1)，我说那可以建一个2D表格，又问能不能把memory降到N，但是保持O(1) lookup，我就讲了建bucket然后merge的思路，小哥直接问有没有听过union find。然后开始写，我说有点复杂估计写不完，小哥说没事你尽量写。然后果然没写完，不过我把大概框架搭好了，小哥说没关系我相信给你多点时间你是可以写出来的…
.本文原创自1point3acres论坛


中午有点乌龙，之前跟我说的是面完两轮就吃饭下午再接着面，结果当天面完第二轮小哥说中午安排了一轮面试面完再吃饭，但是等了十几分钟也没找到下一个interviewer于是第二轮小哥就直接带我去吃饭了… 午饭聊了一些real world工作的东西，整体感觉也挺愉快，吃完小哥还把我送去了另一栋楼面下一轮（因为临时安排找不到同一栋楼里的会议室了）。

第三轮 白人小姐姐
. 留学申请论坛-一亩三分地
以下内容需要积分高于 150 才可浏览

. more info on 1point3acres
不是很好描述的一个题…大意就是给你一些画，每个画都有一个min price和一个quality point，问需要多少钱才能把所有画买下来，条件是1）每幅画的成交价不能低于min price，2）所有画的成交价必须和他们的quality point成正比。e.g. {20, 3}, {10, 1}, {15, 2}，成交价就是30, 10, 20, 总价60。这一问比较简单，可以O(N) time O(1) space完成。接下来follow up问最少需要多少钱才能买下n幅画。当时只有20分钟左右了我就说简单一点可以brute force，把所有画里取n个的组合找出来，然后call第一问的函数算价格，最后取global min。小姐姐说不错，你就写brute force吧，我就写了。面完以后走回原来楼的路上我就问这题是不是有更简单的解法，感觉有点像DP，小姐姐说是的可以DP解。


后来回家想了想可以用背包问题解

. from: 1point3acres 



第四轮 俄罗斯？小哥
以下内容需要积分高于 150 才可浏览


Reverse linked list by group of K. 给一个链表，每K个一组reverse，e.g. 1->2->3->4->5->6->7->8变成3->2->1->6->5->4->7->6。弄了几个pointer，需要记录一下每个组的开头结尾什么的，写起来感觉挺乱的不过我在白板上画了一下解法以及一丢丢pseudo code，写完又去白板上完整了test了一遍。小哥全程感觉有一丢丢脱节，不过我每次check时候他都说嗯，可以，没问题……


第五轮 俄罗斯？小哥
. visit 1point3acres for more.
以下内容需要积分高于 150 才可浏览


shortest distance between words，也是提了几种解法，最后推导到O(N)/O(1)，用2 pointer，然后很快写出来了，还有15分钟，我问还有follow up吗小哥说没有了，说你面一天估计也累了，然后随便聊了一下就放我走了。

### [10/03/2018][12]

十月一号狗家Onsite面经，希望可以造福地里的其他国人面试者。也求一些大米哈哈。. from: 1point3acres 
整体感觉谷歌是唯一一家公平对待所有求职者的的一线公司了。我问了几个面试官，他们说HC review的时候不会知道你的gender, race, university等等，会凭借面试官给你的feedback打分。感觉还是很专业的。. 一亩-三分-地，独家发布
Ok, 话不多说直接上题。. 牛人云集,一亩三分地
. visit 1point3acres for more.

以下内容需要积分高于 130 才可浏览

你想要隐藏的内容比如面经1.第一轮面试，印度小哥。题目是candy的那道面经题。input: int[] scores, 代表着每个学生的考试分数，现在老师要根据每个学生的分数发糖果，规则是，如果一个学生的分数高于左右临近学生的分数，那么该学生的到的糖果数量也要比左右学生多。输出就是int,代表着老师所需要最少糖果的总数。 follow up：如何不使用extra space解决这道题。全程面试小哥都会要你根据你的算法，跑他的case。感觉他也不确定你写的算法对不对，你一边写，他会根据他的case来分析你写的对错与否。


2.第二轮面试， 中国小哥， 字符串转换那道面经题，输入是String src, String target, 问你是否可以从src转换到target, 返回boolean. 比如abc -> def，转换方法就是建立映射map， a->d, b->e,  c ->f转换具体过程就是abc -> dbc -> dec -> def.这是最简单的情况。如果字符串map是有环的，例如, ab -> ba, 其中的环就是a->b->a,这会造成转换失败。ab -> bb ->aa ->bb .......， 但是呢你可以借助第三个变量来完成转换，还是ab -> ba, 你可以建立map a->c b->a, c->b, 转换过程就是， ab ->cb -> ca ->ba。所以其实ab -> ba是可以成功转换的，返回true。 所以失败的case就是，如果你没有这样额外的变量c可以借用来解决换的问题了。假设字符集只有a-z， 你abcdef....z -> bcdef...za就不能转换，因为在26个字母中没有额外字母可以用来解环。

我觉得没那么简单，我觉得这个题要根据两个string 建图， 然后找环。 具体思路我想是这样，欢迎大家来讨论：

1. 根据两个string的关系建图，然后通过26 - # of char， 确定 num of char left（就是算出来没有被用过的char）
2. 对于图里的每一个char，进行图遍历搜索， 并且标记vivisited，如果有环退出，并记录环的个数 . from: 1point3acres 
3. 要想让环能够自解, 必须跟每一个环匹配额外一个没有用过的char. 比如题目说的a->b b->a的例子，必须另外加一个字符并且这个字符没有在字典里 
4. 最后我们只要保证环的数量 <= num of char left  就可以说明这个一定有解了。

3.第三轮面试， 印度大姐， 给你一个BST, 但是这个BST是有duplicate的，问你在这棵BST中出现频率最高的那个数字是什么，以及频率是多少。 follow up是， 不用extra space

利用BST中序遍历是单调递增的性质。维护一个curVal，在中序遍历的时候，如果root.val == curVal，更新curFreq。因为BST保证了你只会在连续几个node的时候碰到相同的val.不可能你刚开始遍历了几个4，然后遍历了几个5，然后又遍历到4.

4.第四轮面试，国人大哥, maze generation. 输入是int[][] board, int[] start, int[] dest,返回一个int[][] maze. 这题题意比较复杂。简单来说就是让你随机生成一个迷宫，-google 1point3acres
条件是：
    （1）你肯定要生成一些墙，这些墙宽度为1，意思就是board[0][0] - board[0][3]可以是墙，s宽度为1， 长度为4。 但是不能生成board[0][0] - board[1][3]这样的厚墙（2*4)
      (2)  要求这个迷宫有且仅有一条路可以从start到达destination， 另外对于那些不是墙的blank cell，也要有可以从start到达它的路径。 也就是说不能有一些孤岛是不能到达的
      (3)  后来大哥给我简化了一点，如果输入board里面已经有一些墙， 用1表示，但是这个迷宫并不是具有通路的，然后让你根据以上条件，生成迷宫。






总之面试体验是很友好的，你提出一个brute force解，然后你讲给他们，讲的过程中你可以提出优化的点，一般就是他们想要的了，然后你可以和他们讨论你的优化方案。这样不断.留学论坛-一亩-三分地
交流下去你就会想到答案了。

### [09/19/2018][13]

1. 问简历上的项目+带时间戳的map
2. 貌似是个高频题，之前地理看到过。 给了2d grid的宽度和高度， 找从左下到右下有几种方法，规定只能往右，右上，右下三个方向走。 follow up能不能优化空间。
3. 挂的是这轮，要找长度为50的bar code, bar code是由黑白两色构成，第一个和最后一个只能是白色，且最多连续三白和连续三黑，问有多少种符合条件的 bar code. 
    LZ刚开始的思路是dp[j] 代表 长度为i， 以j 为 结尾 有多少个bar code (j == 0代表白，j == 1代表黑） 然后去掉不满足条件的，被面试官指出会剪掉很多解，LZ后来说想用三维试试，
    也没时间了，feedback给的说有些题用的方法太复杂可能就是指这轮吧。

第三题我的思路：
建立两个int[] white 和 black 长度都为50-google 1point3acres
white[i] 和 black[i] 分别表示 第 i 位 涂成 white or black 的方法有多少种
white[0] = 1;black[0] = 0;
white[1] = 1;black[1] = 1;. visit 1point3acres for more.
white[2] = 2;black[2] = 2;.1point3acres网

white[i] = black[i-1]+black[i-2]+black[i-3];
black[i] = white[i-1]+white[i-2]+white[i-3];
最后返回white[49];
因为一个块（i）如果涂成白色的话， 从左向右数， 
它要么是第一个白色，(i-1)是黑色 
要么是第二个白色，（i-2）是黑色， （i-1）是白色. Waral 博客有更多文章,
要么是第三个白色，（i-3）是黑色，（i-2）(i-1)都是是白色

dp[j] 长度为j且两侧颜色相同。= dp[j - 2] + 2 * dp[j - 3] + dp[j - 4] + 2 * dp[j - 5] + dp[j - 6], dp[1] = dp[2] = 1, dp[3] = 2

i表示当前位置，j表示颜色，0是白色，1是黑色 
初始化dp[0][0] = 0，dp[1][0] = 1, dp[2][0] = 1, dp[0][1] = 0, dp[1][1] = 0, dp[2][1] = 1
dp[i][0] = dp[i - 1][1] + dp[i - 2][1] + dp[i - 3][1]
dp[i][1] = dp[i - 1][0] + dp[i - 2][0] + dp[i - 3][0]
最后返回dp[n][0]

关于第三题，维护一个50×6的dp。50是barcode的长度，6只一共只有六种结尾的状态，即：1白， 2连白， 3连白， 1黑， 2连黑， 3连黑。. 1point 3acres 论坛
.本文原创自1point3acres论坛
int Solution::google(void) {
    vector<vector<int>> dp (6, vector<int> (50, 0));
    dp[0][0] = 1;

    int mod = 1e9 + 7;

    for (size_t i = 1; i < dp[0].size(); ++i) {
        // end with 1 while.1point3acres网
        dp[0][i] = (dp[3][i - 1] + dp[4][i - 1] + dp[5][i - 1]) % mod;. 1point 3acres 论坛
        // end with 2 while
        dp[1][i] = (dp[0][i - 1]) % mod;. more info on 1point3acres
        // end with 3 while
        dp[2][i] = (dp[1][i - 1]) % mod;

        // end with 1 black
        dp[3][i] = (dp[0][i - 1] + dp[1][i - 1] + dp[2][i - 1]) % mod;
        // end with 2 black
        dp[4][i] = (dp[3][i - 1]) % mod;
        // end with 3 black
        dp[5][i] = (dp[4][i - 1]) % mod;
    }
.1point3acres网
    return dp[0].back() + dp[1].back() + dp[2].back();. 1point3acres
}
. 一亩-三分-地，独家发布
手动test了下。一下1代表黑，0代表白。
长度为1
所有可能：0
满足条件：0， 共计1种
长度为2
所有可能：00， 01
满足条件：00， 共计1种. Waral 博客有更多文章,
长度为3
所有可能：000，001，010，011
满足条件：000，010，共计2种.本文原创自1point3acres论坛
长度为4. 留学申请论坛-一亩三分地
所有可能：0000，0001，0010，0011，0100，0101，0110，0111 来源一亩.三分地论坛. 
满足条件：0010，0100，0110，共计3种

请大家看看思路是否正确。谢谢。

第三题我觉得是DP没问题， DP[n] = DP[N - 2] + 2DP[N - 3] + 3DP[N-4] + 2DP[N - 5] + DP[N - 6]. 然后把1-6的情况都求出来就好了。。我也不知道求得对不对 1->1, 2->1,3->2,4->3,5->7,6->12然后开始往后面DP就好了 应该是个O[N]. 大体逻辑是你两边必须是两个白的开始，如果你两边只有两个白的，就是两边两个黑的的48个格子，如果两边有三个白的，就有两种情况每种都是两边都是黑的的47个格子依次类推。两边都是白的和两边都是黑的其实是一样的，所以每次直接递归就可以了。

4. 力抠坝巳舅 two pass -> one pass o(1) space
5. 自我介绍+简历项目+算法：说几个人赛跑，{A, B} 代表 A跑赢了B，{C, D} 代表C跑赢了D, 然后{A, C}表示A跑赢了C，输出“ACD”或"ADC", 就是胜者在前，平的话顺序无所谓。拓扑排序。

### [06/28/2018][14]

刚刚在LA面完的google onsite，和大家分享一下。

第一题：有一个logger，然后两个函数，startRequest(string requestId, long startTime), endRequest(string requestId, long endTime)。 然后打印的时候要按照startTime的顺序来打印出来，打印出requestId，startTime和endTime。输入的时候startTime是从小到大的输入的，endTime的大小不一定。. Waral 博客有更多文章,
以下内容需要积分高于 120 才可浏览

follow up是只有前面一个requestId的endTime到了才能print出后面的。

比如输入startRequest("bar", 200), startRequest("foo", 300), endRequest("foo", 500), endRequest("bar', 400)
当输入endRequest("foo", 500)的时候是没东西打印出来的，因为在foo之前的bar还不知道结没结束，直到输入了 endRequest("bar', 400)，这个时候输出“bar“和”foo“。


第二题：是一张图，比如三层，第一层3个点，第二层4个点，第三层3个点，每一层的点都和下一层的点连接在一起，每个点都有值，每个连接都有值，然后求第一层到最后一层最小的值，-google 1point3acres
以下内容需要积分高于 120 才可浏览

follow up是求值最小的路径。面试官说是DP题，用两个vector记录状态。

第二题我也一开始说是BFS，然后他说是DP问题，他说时间复杂度低一点。就是从有1，2，3这三个点的这一层到有8，9，10这三个点的这一层，其中每相邻两层之间所有的点都有连接，比如1->4, 1->5, 1->6, 1->7, 2->4, 2->5, 2->6, 2->7这样，每个点有自己的值，每条连接也有值。求第一层到最后一层哪条路径值最小。
1  4  8
2  5  9
3  6  10
    7

第三题： 8 Puzzle问题

李扣琪琪三

第四题：就是一个2维数组里的有人和自行车，要每个人匹配到一辆自行车，人和自行车的距离越短越好，没有距离相同的情况。就是算出所有的距离然后放到heap里慢慢pop出来，记录下人和车的状态就可以了。. From 1point 3acres bbs

### [10/04/2018][15]

1.设计一个in memory cache 这轮有点紧张，本来以为要设计个distributed <k,v> store什么的（像redis）那样的，好久才搞清楚面试官只是想要一个generic的cache。列了很多需要考虑的，但是写代码的时候有些没考虑到，而且写写删删，最后代码没写完，只说了下思想（可能是跪在了这一轮，让HC觉得我不是L4的料？）。
2.hashmap with expiration 这轮是一步一步从只有put, get函数，到加上cleanup函数，到多线程。感觉面试官引导的不错。
3.(1) 输出所有叶子数为n的FBT（full binary tree:每个节点要么两个孩子，要么没有孩子）(2) 字符串数组编码成字符串，再解码成字符串数组（好似在leetcode见过，没记过题号）。面试官只让楼主只写了解码的方法，开始有几个小bug（下标少加了1这种）。面试官指正后迅速改正了（感谢面试官），拍照结束。
4.给matrix，只可以向右边（正右边，右上，右下）走，问走到(0, H)的走法。follow up: 要经过给定的一系列点的走法。
之后面试官说时间有点早，再出一道吧。给一个table，intersection的地方有些点。可以将在同一行和同一列的点删掉，问最多要删多少个点。楼主感觉这像是个connected component的题，同一行同一列的可以作为一个connected component，每个CC里面最后只能剩一个点，就说出了想法，面试官认可后开始写代码，然而最后没写完。。面试官安慰说可以了。。。
5. 给a list of list, 其中的格式是{{parent, child}, {parent, child}...}，parent和child分别是树中的节点的index，要求恢复出来这棵树。楼主写完这道题还剩十分钟，面试官问要不要下一个challenge。然后出了cross word puzzle的题目，楼主看了半天只知道要用search，然而不知道怎样减少search space。最后面试官说要借助历史数据，先填容易更容易填成功的词（如world, finance等）。。。(我自己真想不到。。) 后来想想第一道题不是难题，不应该用那么久来解。不知道这轮面试官评价咋样。

### [10/01/2018][16]

round1：这个面试官就是我上面说的不走寻常路的。一上来就说，我不经常第一轮面试的。然后又说，我今天不问你算法题。lz听了心里一惊，因为邮件里说都是算法题啊。然后他说是个api设计题，说是一个坐标系里面有很多点，你设计一个类来把这些点分成cluster。我就说 加点 分成k组 这两个方法。他说好那你怎么检验分的cluster质量好坏呢？我说我们可以求一个cluster 里面所有点的重心，看距离远近。他说不太好。lz实在是烦这种题，就那种比较直观的思维，感觉谁面试都会这么说，也没法让我outstanding 啊，我就说点难的吧。我就说找出每个cluster的外边界，看是否相交。https://www.geeksforgeeks.org/convex-hull-set-2-graham-scan/
他说这个太复杂了，你也写不出来啊，咱么想点简单的吧。我说我能写出来。他说 then that would be interesting。 他又说假设我给你了个库，能实现关于判断图相关的所有方法，比如比较器，你不用自己实现细节，用这个来实现检验classify的质量好坏。我这里理解偏了，还以为终于回到算法层面了，就开始写Graham Scan的code。不过写一半，他说看不懂我写的什么。然后我就给我讲我的算法的思路。他就开始喊，I told you, no algorithm, no math. 我低头无语了，不知道他让我写什么。我就问他你是说你给我的类里面已经能实现 graham scan了吗？他说是。我勒个去，好吧，那我就又写了两个函数，一个是找出graham scan的边界的所有点，第二个是判断两个边界时候相交，他说哦，看起来还行。最后时间也到了。写了半天其实只有四个(unimplemented的)函数名字是他想要的，我那些实现的细节他都不不看。我就很纳闷他这api design到底是考什么……简直是坑了我一轮。事后证明了这轮是nagetive。遇到这种面试官我觉得95％的人都会是nagetive吧。

round2: 白人小哥，身高185+。利口起灵，比那个稍微难点，一次不是跳两级，是跳k级，给一个k，一个n，n是总台阶数，k是每次最多跳的个数，可以比它少。我一上来说dp，给了个时间复杂度 O(kn)，空间O(n)的。他说能不能简化一下空间。我说那我给了个时间kn, 空间k的。最后讨论了一阵子我简化成了时间n，空间min(n,k)的。就是不用每次都把那k个加一遍，保持一个sum就好了，每次删除一个旧的再加一个新的。

round3: 巴西人肤色的姐姐，白小哥shadow。问我个高频题，扫地机器人，利口死罢就。一开始是长方形地图，秒了之后改成不规则地图，又秒了。还剩下15分钟，尬聊，问了好多组里的事。
. 1point 3acres 论坛
午饭，不敢吃太多，白人小哥带我逛了逛纽约office，没啥意思，大公司都这样。不过lz说了一路 waoo, so cool!

round4: 白人阿姨，abc小哥shadow 。高频题，一个dictionary里面有很多词 比如 ["abc","def"]，有一个stream一个一个单词进来，e,d,c,a,b,c,s,d,e,f.... 如果出现了dict里面的单词就输出这个单词，刚才那个栗子里就在 读第二个c时输出abc，最后那个f那里输出def。lz用的地理的方法，把所有的单词倒序存到trie里面，然后找出所有单词的最长的长度，用一个linkedlist 存读过的字母，超过这个长度就在前面删掉旧的。然后每读一个新字母就到trie里面比较一下。有的话就输出。写完还剩下25分钟，阿姨说，你这个代码有什么限制吗？我说输入必须是小写字母，不过你之前不是说都是小写字母了吗，她说那万一不是怎么办，我说读完字母之后检测一下是不是，不是的话throw个exception。她说好，不过我告诉你不只是letter怎么办，我说trie里面array改成hashmap，好，又花了7分钟改代码。写完差不多还剩下15分钟，她说如果要交codereview了，你有什么要改的吗。我觉得她实在是不知道问啥了，没话找话。我装模作样看了一会说就这样吧不改了。然后尬聊15分钟。

round5: 白人小哥，身高187+，高频题饮料贩卖机。三个button，第一个 [30,40]第二个[20,40] 第三个[60,70] （具体的数字我忘了，瞎编的）。有一个杯子装[130,160]，能不能有一种方法能够确保倒的饮料正好在这个杯子的范围里。lz正好面试前一天晚上睡觉前做了这道题，所以记忆犹新。不过还是装作没听过一样问了一些自己都觉得蠢的问题。然后花了十分钟写完了。方法就是递归+（二维）memery. 还剩下半个小时吧。小哥跟我讨论复杂度，带不带memery的都讨论了一下，我貌似这里出错了，其实带不带mem都应该是3^n，唉，backtracking的复杂度我面试就没答对过。不过小哥没看出来，我画了个说明图给他唬过去了。然后时间还很多很多，他说你是要尬聊还是做题，我说做题。他就口述了几道题，我也就随便说说思路，没写。后来小哥送我下楼还问我是不是有什么参加竞赛的经历，做那么快。我说是的(参加leetcode每周的那个竞赛)。
请问大概是这个意思吗:.本文原创自1point3acres论坛

Map<int[], boolean> map = new HashMap<>();

public void backtrack(int[] range) {. Waral 博客有更多文章,
    if(map.containsKey(range)) return map.get(range);
    for (int i = 0; i < buttons.length; i++) {
        int[] buton = buttons;
        int[] newRange = new int[] {range[0] - button[0], range[1] - button[1]};
        if (backtrack(newRange)) {
            map.put(range, true);
            return true;
        }
    }
    map.put(range, false);
    return false;
}

面完试隔了一天recruiter 说有个nagetive 和a bunch of positive，所以能送hc，不过要先team match。花了一周team match，今天交了hc之后过了一个小时recruiter发邮件告诉我过了。希望后面不要有变故吧。

第四轮为啥要倒序存trie，第五轮可乐题的二维memory是干哈用的？

1因为单词是正序从stream 里输出的，从后往前找方便些，后前往后也行，稍微麻烦点。
2比如你获取到了一个 [60,80]这样的范围，backtracking之后知道这个数再怎么组合别的按钮也没法到最后的范围，下次再遇到[60,80]直接就剪枝了。就不用在backtracking一遍了。

补充内容 (2018-10-3 13:47):
从前往后的话你不知道从list的哪里开始比较，所以要比很多次。可以写写看，就明白了。

### [10/01/2018][17]

skip了电面，因为背景比较match cloud，但还是吐槽下，5轮面试4轮印度人，1轮白人，连吃饭都是印度人作陪！！！

1. 让你写一个函数check两个string是不是同一个类型的，比如 banana和xxxxxx就不是同一个类型的，因为不是one to one mapping，这个用一个map就可以做了. 留学申请论坛-一亩三分地
follow up是说，如果给你一堆string，作为模板，现在输入一个string，只要这个string跟模板里的任何一个string pattern match就行了，这里要求优化的是compare的time是o(1)，记得当时解法是.本文原创自1point3acres论坛
把给的这堆string按数字分隔的方式作为模板存到set里，中间用符号间隔数字，面试官表示认同。follow up的中途那个面试官突然冒一句，我好像把题给你出错了，我心里一万只草泥马飘过，
算法都讨论清楚了开始要写代码了，你跟我说你题出错了……最后他说没事，还是按我们现在讨论的办法写吧。后来我看了看其他的面经，好像是这个面试官自己把面经题搞错了，
这个题follow up应该是问的类似一个有向图的概念，不过年代久远我也忘了， 大家往前翻翻面经吧。. 1point 3acres 论坛

2. 分钱，一堆人一起出去玩，每个人都付了一些钱，然后让你实现一个算法，optimize所有的给钱方式，最后使得人与人之前的transaction次数总和最少，要求输出这些所有的transaction，不允许用dfs这种brute force，leetcode原题，最后给的解法是按个人整合之后排序，首尾双指针往中间处理，queue也提了，说时间复杂度差不多，面试官认可，就让我写了，其实个人觉得这个算法不太对，至少我不能证明是对的，这一轮写之前跟面试官确认了函数的定义，写的中途面试官不断让我改变函数的定义，还跟我说没事，你的code大部分都可以保留，也不能说他黑我吧，态度还是挺nice的，但我估计我那个不太好的feedback是这个人给的。LC465

3. design elevator in sunnyvale google cample，那个电梯很奇怪，里面没有按键说你要去几楼，你要去几楼是在外面输入的，然后让你写相关的class，然后讨论monitor的分配电梯算法，优化之类的

4. 给你一个m*n的矩阵，然后现在让你实现两个函数，一个是update()，能去update这个矩阵任意一个位置的数字，另一个是sum()，给一个sub矩阵的坐标，要你求出这个sub矩阵的和，要求优化sum(),时间复杂度是0(1)，follow up是要log(n)的解法，不用写说就行了，leetcode原题

5. 处理log，现在给你一个log，你可以当成input是一个string, 然后这个log里的formate都是
[timestamp]<jobn>"hello, my day!"
timestamp<jim>"greate"....
这种format的，就是一个人名后面会跟一段message，像聊天软件一样，现在让你统计top k的user，统计顺序按照他们敲的单词数总和来定
. 围观我们@1point 3 acres
跟面试官讨论了min heap，max heap和sort三种办法，外加常规的字符串处理。

总体来说题中规中矩吧，后来等了三周有个人还没交feedback，实在没办法，就只好4个feedback交HC了，然后挂了，所以建议大家稍微提前点申G家，他们家是最慢的。
另外就是我个人的一点体会，不要一开始就答应HR switch到一个固定的role，我就是被HR忽悠着换到一个cloud相关的role下面，虽然也是general hiring，但team match的时候HR死活不给我match其他组，找各种借口拖延match其他组，连internal 的 referral发信催都没用。最后送HC的时候match的那个老板还休假一周，support letter也没有，真是欲哭无泪啊。

HC还是看运气，同样一个分数等级，feedback具体怎么写，可能最后在HC的结果会完全不一样。所以原则上还是祈祷多遇到中国面试官和白人面试官吧。

### [04/03/2018][18]

1. next permutation 2. dp高频 3. LC气流就 4.inorder morris traversal?

1. LC原题，给一个数2134，用这个数的这些字符，排出最小的比它大的数；.1point3acres网
-follow up：如何不用Arrays.sort; 如果这个数是负数怎么办 来源一亩.三分地论坛. 
2。 DP。给定一个矩形的长宽，用多少种方法可以从左上角走到右上角 （每一步，只能向正右、右上 或 右下走）：整个矩形遍历做DP即可，不需要想复杂
-follow up：如果给矩形里的三个点，要求解决上述问题的同时，遍历这三个点 （切割矩形，一个一个地做DP，然后相加）
-follow up：如何判断这三个点一个是合理的，即存在遍历这三个点的路经. 留学申请论坛-一亩三分地
第二题的第二问是不是分别四次DP过程DP第一次起点为左上角，终点为第一个点，第二次是起点为第一个点，终点为第二个点，第三次是起点为第二个点，终点为第三个点，然后最后就是第三个点到右上角。同样的状态转移方程？
-follow up：如果给你一个H，要求你的路径必须向下越过H这个界，怎么做 （别问我，我不会）
楼主这题试一试用镜像做，也就是说终点不在(W, 0), 而在(W, 2H)， W是矩阵的宽度。

第二题follow up3用两个dp矩阵，一个存到过H以下的路径数量，一个存从来没有到过H的路径数量，然后正常dp，最后输出第一个矩阵的右上值就好了吧。
第三问很好回答啊，三个点的纵坐标必须是不等的，按照列排序后（Point2.col - Point1.col）>= abs(Point2.row - Point1.row)。点二点三满足同样的关系？第四问我有个思路不知道对不对，就是假设把矩阵在row H砍一刀，下边的不要，求这个新矩阵的第一问，然后老矩阵的第一问减去新矩阵的第一问，就是答案了？
第四问我有个思路不知道对不对，就是假设把矩阵在row H砍一刀，下边的不要，求这个新矩阵的第一问，然后老矩阵的第一问减去新矩阵的第一问，就是答案了？

3. 给一个数组，要求你尽可能多的切割这个数组，使得每一个小段分别sort之后，整个数组就sort了 （眼熟，应该是原题，我不记得解法了，当时用stack做的）LC 769

第三题是说区间之间需要按照大小排序，每个区间的最小值大于等于上一个区间的最大值。

定义f（k),  0 <= k <= matrix.cols-1, 为当第一次越过H时经过的节点 node A （H，k）时的总方法数，包含起点到（H-1， k-1）然后右下方向到A 和 A到终点两段，均可DP做。. 牛人云集,一亩三分地
对f（k）做循环累加即可

从后向前扫一遍，找出每个位置之后的最小值，时空O(n)。
再从前往后扫一边，如果某一个区间的最大值小于之后的所有值，那就切一刀。
这样可行吗？（居然面完三个才吃饭，饿死妈妈了）
4. BST 的in-order遍历，嗯没错，就是这样，我也不知道为啥 （然后问我不用stack怎么做？我怎么知道。他一边提示我一边写，就是每个node又加了一个指针，反正到最后我也没完全搞懂）。morris traversal
stack作用是找到它之前的node 也就是它的parent
所以每个node加一个parnt pointer（可以trace back） 就可以起到stack作用了

### [10/07/2018][2]



### [10/07/2018][2]



### [10/07/2018][2]



### [10/07/2018][2]




[1]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=448051
[2]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=447378
[3]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=447987
[4]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=448149
[5]: http://www.1point3acres.com/bbs/thread-438216-2-1.html
[6]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=447339
[7]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=447724
[8]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=446650
[9]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=446993
[10]: http://www.1point3acres.com/bbs/thread-447993-2-1.html
[11]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=445865
[12]: http://www.1point3acres.com/bbs/thread-447125-2-1.html
[13]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=443906
[14]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=432049
[15]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=447644
[16]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=446929
[17]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=446909
[18]: www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=380867
[19]: 
[20]: 
[21]: 
[22]: 
[23]: 
[24]: 
[25]: 
[26]: 
[27]: 
[28]: 
[29]: 