1. 不幸碰到阿三，从一上来就板着个脸，问了一道LC上一道题的变体，说把一个array分成两个subsequence（不是subarray），让这两个subsequence的和最接近，返回这两个subsequence。
2. 美白，LC原题，给一个matrix，全是0和1，要数数相连的1的“岛”的数量，轻松解决后又追问如果是要输出最大的岛的大小怎么办，稍微修改一下recursive的method，让它返回当前岛的大小就行。又追问如果要统计所有岛的形状，返回岛的形状的数量怎么办，我的解法是定义一个Shape类，让recursive method返回，再implement一个比较Shape的method，统计返回的形状数量就行。
3. 老黑，先比较一下array和linked list的特点，再implement一个两头开的deque，要求get(int index), addToFirst(int num), addToLast(int num)都要平均O(1), 两个arraylist解决
4. 国人，LC原题，能返回min的stack。又追问给两个array A和B，两个array的元素都一样，只是顺序不一样，要求用stack处理A，允许的操作有push和pop，让stack pop出来的数字正好可以组成B，如果不能实现返回空。

1. permutatio II 考虑重复情况
2. combination
3. Find Median from Data Stream

1. BQ + 蠡口仪器
2. BQ + 设计国际象棋
3. BQ + 蠡口刘思
3. BQ + 设计产品推荐系统

很简单，实现Math.power(int a, int b)这个function。 然后问了下复杂度和一个BQ就完了。

1. BQ+ system design(mini_Url)
2. BQ+ coding(忘了）
3. BQ
4. BQ+里口以留吴（verComp)
5. BST kth element( leftSubtreeCount provided ) + system design( in-memory cache cloudfront service)

印度大姐：
问了30分钟behavior，然后开始出题。
花了10分钟她终于说明白了自己出的是算法题，不是OO design
然后说9：50结束，给我10分钟code

中国大哥：
问了30分钟behavior，然后开始出题。
出了tree serialize, deserialize. 我说是bst还是binary。他自己想了一下，说你写bst吧。. From 1point 3acres bbs
写了，他说嗯，你这个有点不对。
我说哪里不对了，他看了30秒，没说出来。
我又跟他讲了一遍。
最后5分钟他说，你写个binary的吧。
没写完。. from: 1point3acres 

白人manager:
问了30分钟behavior，然后开始出题。. more info on 1point3acres
问了怎么设计photosharing website
设计完了还跟他扯了一点怎么做highly available， partition-tolerant的系统

白人大哥：
问了30分钟behavior，然后开始出题。. 1point 3acres 论坛
问了一个word maze。 就是DFS，写完了。他说你优化一下。.留学论坛-一亩-三分地
我就优化了。-google 1point3acres

第一轮
第一题给了个大背景巴拉巴拉但是本质是里口 四十.本文原创自1point3acres论坛
第二题是 two sum，然后是有相同的数，要输出所有的组
第二轮 OODesgn an elevator
第三轮 BTS to a doublelinklist 
第四轮 LFU cache，但是结合了一些system design 的概念

第一轮：code 轮， 印度小姐姐，SDE I，看着很年轻， 负责面的principle好像是 High standard,  口齿不是很清楚，题目是给一堆log, 有customer id, 有pageId，有timestamp， 要求找出一定时间内访问频率最高的 TOP 3 Page sequence.
不知道大家和我想的一不一样，反正我第一反应就是 leetcode的TOP K frequent word那道题，心里窃喜，也没细想，哗哗就开始在白板上写，用PrioirtyQueue, 写个比较器什么的，写的非常熟练，这个时候印度小姐姐满脸困惑的问我为啥要用PriorityQueue, 我以为印度小姐姐没懂我的思路，又跟她巴巴地说了半天我为啥用PrioityQueue，然后她说不是这个意思，不是问的最高频的3个page，问的是点击次数最多的3个pageId sequence，比如A->C->D, 比如B->C->E， 所以求的其实是频率最高的那个sequence, 思路挺直接的，就是用个map先存customerId和pageSequence, 然后再遍历一遍所有的pageSequence来统计其中任意3个连续的子序列出现的次数，最后得出次数最多的那个序列。 等我理清题意的时候，我已经写了大半个白班，TOP K 都快写完了，印度小姐姐才问，于是我一着急，就把写过的全擦了，想要重新写，印度小姐姐估计也知道我时间不够写完全部代码了，让我先别擦，先拍一个我已经写好的代码，最后时间不大够了，就让我把其中主要的两个过程，就是如何从log中得到pageSequence以及如何统计次数的过程写出来。虽然理解错了题意，但是理解完题意我很快的给出了思路，然后把她要求的部分代码写出来，时间刚好用完，慌得一批。.本文原创自1point3acres论坛
. From 1point 3acres bbs
第二轮： OOD， 一个美国白人小哥，人挺nice的，先自我介绍一分钟，完了就开始面OODesign.问我玩不玩棋牌，我说玩，就丢给了我一道Black Jack. 因为之前有准备过棋牌类设计，所以不怎么慌，在白板上边交流边画类图，在他要求的地方写一些代码无非是继承之类的，45分钟很快就过去了，基本上类图也画完了，聊得挺好，感觉还可以。

第三轮： Code 轮，本来给的list里应该是一个印度姐姐来面的，结果推门进来是个国人小哥。上来问了自我介绍，随便聊了一会项目，然后，就直接给了一道String palindrome permulation, 应该就是LeetCode 原题，很久以前刷过，思路还是挺直接的，我就说了思路，用回溯法，递归，然后小哥说可以，sounds good，可以写了。于是就哗哗开始写了，写了一半发现不对，应该是substring, 我一不留神写成了subsequence，有点慌当时，然后国人小哥说没事，时间还有，你慢慢想，我又停下来想了想，最后终于想明白了，把代码差不多写完的时候，小哥说时间到了，然后要拍一下code，回头写评价用。当时我想思路是对的，虽然开始写歪了，但最后还是自己写出来了，国人小哥应该不会挂我吧？

第四轮： system design和behaviour， bar raiser轮，美国白人大哥，director， 穿的花花绿绿，但是人特别smart，年轻有为，感觉也就三十出头。先是问了一堆behavior questions，项目相关的，很多"tell me about a time" 之类的问题，就是亚麻的十四军规，之前准备了些例子，都是工作中的一些真实case，所以聊得挺顺畅，核心就是以客户为中心。然后就是system design，设计一个订阅系统。数据库设计，如何拓展，诸如此类，感觉聊得还不错。


第五轮：纯Behaviour, hiring manager轮。 也是个烙印大哥，是个Director, 迟到了大概十分钟，好像是从别的楼赶过来的，来了电脑又刚好更新自动重启，就对着大眼瞪小眼坐了几分钟，跟我说不好意思，然后说不用紧张，都是behaviour question，没有technical question，还是十四军规，因为之前有提前准备，所以感觉基本都还聊得挺好。.本文原创自1point3acres论坛

第五轮之后，进来了个HR，详细聊了下他们家的benefit和perk， 还有relocation之类的，然后问了给offer会不会接，对薪资有什么要求，多久能开始之类的，我当时一度错觉，以为这是定了怎么的？然后他告诉我现在是周五下午，大家都过周末去了，下周一下午会Debrief, 完了很快就出结果，就会通知我的。带我参观了下他们的办公室和食堂用餐区，还有活动区，确实很fancy，然后就把我送出来了。

然后就是煎熬的一个周末的等待，心里一直在打鼓，觉得第一轮题意没搞清，印度小姐姐不会挂我吧？然后想想另外四轮感觉都面的还行，即便第一轮印度小姐姐挂我，应该还有戏吧？ 就这么纠结了两天，到周一下午快下班了还没消息，我心里一沉，就觉得不大妙了。
.留学论坛-一亩-三分地
周二早上沉不住气，发了个邮件去问了recruiter，猎头立马就把电话打过来了，当时在公司开会，没接到，看到以后我直接翘了会出去给猎头打过去，果然不出所料，“Unfortunately”一开头就知道悲剧了，但是猎头人蛮好的，给了非常详细的feedback，以及五个面试官每个人的投票情况及优缺点分析，说Debrief 的时候意见非常分散，但总体还是不出我所料的，印度小姐姐投的Not inclined, 说我对data structure掌握的挺好，但是没办法把code写完， bar raiser 轮那个Director 投的Yes, 说大概在SDE I 和SDE II之间， OOD 美国白人小哥给的也是YES, 也是说在SDE I和II 之间，说缺点可能就是想象力还不够，有时候还需要启发。最后的Hiring manager也投的YES， 说能够以客户为重，很符合公司文化诸如此类的，唯一令我深感意外的就是国人小哥，居然投了No,具体原因我当时也没听清，可能是震精了， 但是就是说国人小哥坚持No，最后bar raiser也没有坚持YES，所以结果就是悲剧了。。。recruiters说feedback是mixed，说我这种情况已经非常close了，可能就是经验差了点，因为只有四年多一点的经验，要是再有多几个月的经验可能就是不同的决定了，说希望我六个月后再投。当然也不知道是不是他故意安慰我。. 1point3acres


Work simulation(原则有先后顺序)
目前两大做题中最重要原则：
1.requirement排在第一，deadline第二。
2.有manager出现的选项无脑选manager，manager就是一个组的地头蛇。
.本文原创自1point3acres论坛
Amazon9条主要原则
原则1：客户是上帝，requirement优先，任何影响上帝的事情都不能干，. Waral 博客有更多文章,
        如某个requirement影响了上帝的体验， 
        你就是死键盘上也不能砍了，宁愿miss deadline
原则2：为长远考虑，即客户几年之后可能会出现的需求也要考虑到，
        不会为了交付短期的deadline，
        而牺牲长期的价值。（比如 global api  和 local api）
原则3：最高标准，“最高”对应上面的“长远”。
原则4：一般情况，能请示manager就请示manager，manager一般不会出错
原则5：速度很重要，决策和行动都可以改变，因此不需要进行过于广泛的推敲
        ，但提倡在深思熟虑下进行冒险。
原则6：不需要一定要坚持“非我发明”，需求帮助也是可以的，四处寻找创意 来源一亩.三分地论坛. 
        ，并且接受长期被误导的可能
原则7：敢于承担责任，任劳任怨，比如领导说谁会java，你会你就跳出来说我会
原则8：对问题刨根问底，探究细节
原则9：服从大局（团队比个人重要）

打分不是关键，排序才是关键。
大部分情况下其实并没有deadline 和 requirement谁更好，更多还是在
这个组合中你对ddl 和 requirement整体的权衡。

每个选项可以评1~5分，most effective 是5，然后1是least effective
刚开始让你看一些介绍amazon工作环境的视频
1.上来给一段video，场景是项目的晨会，就是把team正在推进的项目描述一下，
期间会有多个项目和你有关系，后面会遇到.1point3acres网
2.进入工作界面，可以看到接受到邮件，接收到的instant message
3.进入工作状态。会有同事给你发邮件，发信息。需要你对他们提出的问题做一些判断，也就是给解决问题的选项评分
4.一个21题，有log分析bug，有给报告出问题结论，有判断项目 走向的

情境1：给图书馆写图书推荐系统，关于book api
两个人，在表达不同的观点
选择：tell me more.1point3acres网
一开始其实每个人都在强调自己是对的，即使有一个人更对一些，. 一亩-三分-地，独家发布
也应该选tell me more（原则8），选了之后会得到更多信息

情境2：选图书馆的服务器有没有开放关于实体书的api
两个小哥讨论图书推荐的api应该是自己做还是用现成的。
自己做api覆盖面广，但是due赶不上，别人做的能赶上due。 
requirement优先（原则2），tell me more层层递进

情境3：经理说咱们最近服务器老挂，什么情况？
先选看internal bug的记录
选 I think service 3 is the problem, 
but I would like to see another report to confirm
烙印，义正言辞说自己做了20年服务器，不可能有错误，.1point3acres网
刚刚调试过服务器，不可能是内部错误。
选自己去查，问题的关键在于不要麻烦别人
增加开发过程中测试的时间/测试覆盖更多case，放5
写Manuel test，放3
还有个是unit test，也放3. visit 1point3acres for more.
增加QA的人手，放1
让客户来当小白鼠发现问题，放1


情境4：Amazon recommendation system item，
给你推荐一些你感兴趣的item，第一个issue总是失败，
第二个issue总是显示germany
第一个问题是因为username 太长所以一直报错。. 牛人云集,一亩三分地
第二个问题是因为他用proxy的name来决定是不是语言了。

情境5：德国amazon除了什么问题，让你看log回答问题。问你大概哪里除了问题.留学论坛-一亩-三分地
亚马逊推荐广告，给英国人推了德文广告，给你log文件，
问你可能在哪，找bug in error log
来源一亩.三分地论坛. 
情境6：员工们讨论case media network服务器最近好多compliants
有德国的，有invalid recommendation，有返回404，. 一亩-三分-地，独家发布
找出错原因的相同点
德语因为服务器， 一个因为用户名太长，一个是有些用户的语言变成德语

情境7：具体客户ddl 只有两周，两个方案，延到四周，做完整。
另一个说先实现一部分功能做个demo，再慢慢做。.1point3acres网
先做demo放5，按部就班四周放3， 通知其他组说两走做不完接着做美国放1

情境8：估计项目开发时间.1point3acres网
Manager放5，找有经验的人请教4，上网查资料或是先做一段时间再估计都放3，
还有其他裸上的就1。. 1point3acres
. more info on 1point3acres
情境9：一个项目时间表设计
说你是这里最会用什么语言的，比如java
. from: 1point3acres 
情境10：安排会议
视频会议 5   三个老二开会和老二去找老大开会 3   推迟会议和邮件开会 1
. 一亩-三分-地，独家发布
情境11：搞个数据库. 围观我们@1point 3 acres
两周时间可以搞个数据，**ben可以帮忙，大腿priya可以帮，但是要等一周半
报告manager放5，和**合作等大腿放4，合作/等大腿是3. visit 1point3acres for more.
自己单干，cut feaure都是1

情境12：系统是否升级
做两个feature，一个让100%用户爽，一个让20%用户爽，
但要升级系统，升级系统自己组会爽，但是升级会推迟做的feature，.1point3acres网
不升级吧，升级之后还得做一遍. 牛人云集,一亩三分地
这题的中心是不升级，先做feature，先让用户爽。
先做100的feature再升级，再做20的feature，放5
不升级，因为我们承诺要做feature，放4。. more info on 1point3acres
不升级，要搞定feature，可以以后推了其他ddl再升级，放3-google 1point3acres
不升级，因为对其他组没影响，我们应该focus在request上面，放2
升级，推迟这两个feature的ddl，因为升级造福子孙后代，放2
升级，不然要做两次，放1
这题的关键在于升不升级，要坚定的站在一边

情境13：新产品设计
给8周时间，选择题，让你pick up 一个features的组合要求利益最大化，-google 1point3acres
每个feature都有相应的价值，H >> M >> L 都代表远大于. 1point 3acres 论坛
首先ddl是前提，中位数不能超过8太多，那样的话就算feature再多也没意义，
同价值，按照ddl排序，同ddl按照价值排序。
. 牛人云集,一亩三分地
情境17：代码分析
三段一长选最长 


一个BQ: 工作上曾遇到什麽困难，然后怎麽解决。
一题coding:
每个session(类似user) 有一个播放歌曲顺序的历史纪录
session1: A -> B -> C -> A
session2: C -> A -> B -> C -> E -> A -> B -> C
session3: A -> B -> C -> B -> D

找长度为n最热门的播放顺序
ex1
input: n=3
output: A -> B -> C. From 1point 3acres bbs

ex2
input: n=2
output: A -> B

ps1:它们存session是用List of List
ps2:同一个顺序在同个session裡面只会算一次, 像是session2 A -> B -> C发生两次,只会算一次

第一题：给几个地点以及这几个地点之间的路线，如A可以到达B，A可以到达C, B可以到达C等等，打印出X到Y的所有路线. 围观我们@1point 3 acres
第二题：给一个二叉树，求二叉树最长的数值连续path的长度，比如：
         1
   2        3
3   5    4   9

那么有两个path是连续的：1-2-3， 3-4,最长的长度为3。path只能从父到子。

过resume 自我介绍
BQ 问customer focus的經驗
string reverse
判断 BST - 我用recursion做, 要求case带入 (recursive code 带入case还真麻煩)
判断 BST - 要求用iterative做

LeetCode题
LC1TwoSumHashMap
LC2AddTwoNumbers
LC2AddTwoNumbersII 来源一亩.三分地论坛. 
LC12IntegerToRoman-google 1point3acres
LC13RomanToInteger
LC15ThreeSum
LC20ValidParentheses
LC21MergeTwoSortedLists
LC23MergeKSortedList
LC28ImplementstrStr
LC33SearchRotatedSortedArray
LC38CountAndSay
LC40LRUCache
LC41FirstMissingPositive
LC46Permutations
LC47PermutationsII
LC49Anagram
LC50Powerxn
LC53MaximumSubarray
LC56MergeIntervals. from: 1point3acres 
LC64MinimumPathSum
LC78Subset
LC81SearchRotatedSortedArrayII
LC90SubsetsII
LC94BinaryTreeInorderTraversal
LC98ValidateBinarySearchTree
LC101SymmetricTree
LC102BinaryTreeLevelOrderTraversal. From 1point 3acres bbs
LC103BinaryTreeZigzagLevelOrderTraversal
LC107BinaryTreeLevelOrderTraversalII
LC120Triangle
LC125ValidPalindrome
LC131PalindromePartitioning
LC136FindSingleNumber
LC153FindMinRotatedSortedArray
LC165CompareVersionNumbers
LC173BSTIterator
LC200NumberIslands. 围观我们@1point 3 acres
LC206ReverseLinkedList. 1point3acres
LC215KthLargestArray
LC217ContainsDuplicate
LC219ContainsDuplicateII
LC220ContainsDuplicateIII
LC230KthSmallestElementBST
LC232ImplementQueueStacks.本文原创自1point3acres论坛
LC234PalindromeLinkedList
LC236LowestCommonAncestor. from: 1point3acres 
LC268MissingNumber
LC280WiggleSort. 围观我们@1point 3 acres
LC297SerializeDeserializeBinaryTree
LC322CoinChange
LC324WiggleSortII
LC338CountingBits

非LeetCode题
ConvertBSTBinaryTree. 围观我们@1point 3 acres
Count1
CountAndSayII. From 1point 3acres bbs
CountAndSayIII
CountingSort
Evaluation
HotelRating. 牛人云集,一亩三分地
IdentifyString
IncreaseAlphabet
InPlaceSort
InterString. more info on 1point3acres
KWayMerge
MaximumConsecutiveNumbers. 1point 3acres 论坛
NameGenerator. Waral 博客有更多文章,
OccurancesSortedArray. Waral 博客有更多文章,
RemoveNodes. more info on 1point3acres
SearchASubStringInword
SingleNumberII
SiteMap. Waral 博客有更多文章,
StackImplUsingQueues
SumNumberString
SwapKthElements

第一轮, 系统设计+ 15mins bq, 设计Twitter的timeline, [请大神帮忙看看]
上来先bq, disagree问题, I: project is using hibernate, I suggest to use spring data instead of old design, the benefit is convenient and efficient (templates ), the result is group disagree my idea, 
I disagree but commit to it (amz principle), and in the future, and we have extra time we do the refactoring.
the interviewer is confusing about it, I cannot clarify very well, shadow helps me to explain, spring data just add another layer.
这块 解释的不好, 自己需要仔细搜搜如何解释 spring data 和 hibernate (其实都是orm)
系统设计 twitter
我照本宣科地说了 qps等计算, 算出了 40M/s 感觉这块完全是多余自己提, 面试官不感兴趣好像 [留个疑问在这里, 系统设计这种estimate 需要做么??]
之后, 讲了最简单的 timeline 设计, 所有followers 获取tweet, 之后排序 aggregate, 返回. 面试官: make sense high level : API server => DB 
followup, case 如果 川普发了句, 我明天9点发tweet, 1m 用户准时不断刷, 怎么处理.
sharding 方面, 如果川普的tweet都在一个db里, 我分析的是, 所有request 会 hit 某一个 db, heavy load, 所以 db要 shard by tweetID to make sure data is shared evenly.
面试官: how can the user get the tweetIds, 
我: user 会首先 拿到所有 follower的userid (包含Trump), 然后查询 所有db, 返回对应的 tweets, (我当时脑子短路, 以为设计的是 userid : [tweets] 的结构, 其实应该是 tweetID, Uid tweetId 做主键和shard id, ) 这样就不会heavy load 某一个db, 所以当时答的含糊其辞)
我: 当时shadow 问的是 shard by uid or tid, 我就说了 tid, 
之后我补充了 要加 cache, 
之后也没下文了, 不知道最后结果是什么
之后 问我 工作经验相关, 如何test 自己设计的系统 可用, 我说了 spring eureka 里可以提供dashboard 检测 内存占用, cpu占用, 之后 可以做集成测试, 压力测试.
面试官 做了笔记, 问还有什么, 
我: 想不出还有什么, 其实还可以说 to make available, we can provide replica instances, to avoid single point failure. 但我觉得他更考察你的经验, 相关的tool
如果让我再回答一遍 我可能这么说:
first, make every service functionally work, pass the unit test. 
second, make integration work, RPC call, (microservices集成测试, 大神给点意见, 什么工具之类的)
third, high available (pressure test, single point failure)
其实最重点不知道他考哪里, 感觉就tm想问 unit test? 其实有时候不知道对面问题的level是什么

lunch 
跟中国妹子聊天, 说组里没oncall
第二轮 
hm 
bq狂聊, challenging project, 讲了自己搞sub domain cookie的事情, 感觉不在他的兴趣点上, 感觉bq其实&#8482;的是看你工作经验.
第三轮
印度小哥, back traverd 算法题, 
第四轮
猜测bar raiser, principal engineer, 
tree node 里包含 left node 的数目, 查找inorder(忘了是preorder 还是什么order) 第x个node, dfs举例, 几行秒掉
设计 CloudFront, 对你没听错
我: 
www.google.com/aa.jpg 作为key, 内容作为 value, in-memory cache, 可以考虑用db作为数据backup
之后问了我 lru , 我给出了算法设计 (最佳解)
问高频查询情况, 给了lfu
面试官total agree, 很开心
这轮感觉不会有问题, 不过传说中的 bar raiser 过了就没事, 应该是童话故事.
第四轮
ood , 主要考继承 抽象类
bq 问我性能和可读性 怎么考虑
我脑抽的说了 先尽量搞定性能, 我其实是英语没听太懂, bq最难的其实就是英语!

希望给大家点帮助, 个人建议, 面试官良莠不齐, 一定要跟住对方的思路和方向, 已经查考点, 你即使知道各种fansy, 他可能只考你 class level的基础.

赞一下lz，我查了最近大半年所有的onsite，linux find， tinyURL 还有停车场是高频中的高频
linux find的核心我感觉就是recursion search 每一个子文件，遇到是文件的就加到返回list，如果是directory 就dfs
我就找到一个用java写的
https://www.mkyong.com/java/search-directories-recursively-for-file-in-java/
希望大家一起分享一下，感觉这道题可以出的很复杂很难

我觉得这道题本身是所谓的面向函数编程的体现

做法是在外部构建一个函数，这个函数返回boolean，然后input是文件，函数的具体实现是find命令所带的各种参数，然后将这个函数放入一个recursive的find方法，这个方法会得出当前目录下的所有文件，并遍历所有当前的文件，如果是文件则使用这个函数来判断一下是否返回true，返回true，则加入到返回文件列表中，如果文件是个目录，则recursive的调用find方法来查询目录下的所有文件。

比较麻烦的是如果文件是个soft link，这个处理有点烦人。

Java下面实现这个主要应该是靠1.8的lambda来做，最java的方法是基于find定义成一个interface，然后基于这个interface继承各种具体的查询类，比如查询名字，查询大小，然后将这些查询类实例化以后发给这个recursive的find，再复杂一点就是得考虑多个查询条件并用的情况，这个是可以通过将实例化的各个类放到一个list里面一起传给find来搞定。

个人感觉这个是能充分说明函数式编程的优势的，应该有些语言用起来会更顺畅一些，个人不熟悉

leetcode里有这题啊，就是设计文件系统 lc588

回报地里的同志们。今天刚面完了亚麻的昂赛特，之前的OA也附在这里。OA是近期一直在用的合并log（前面alphanumerical，后面要不是string要不是numerical），和一串string去掉exclusive list里的词。
第一轮，hiring manager面，全都是bq。还想起来的一些问题比如，你怎么handle这些scenario：例如你跟别人的opinion都不一样的时候，你怎么最后最出决定follow众人的决定，或者别人都错只有你对的时候。。等等吧。我感觉我也就一个地方扯到了14条，别人基本就是陈述事实。

第二轮，友善印度小哥技术面。小哥以前貌似是搞物理的。问了一个比较简单的，given一列进来的数字，返回前K大frequent的数。题目的原意是假设这列数是dynamically进来的，我开始直接假设成静态的了（size已知，内容已知），写到一半发现好像跟他的初中有些不一样。但是他说没关系先把我写到一半的code写完，于是就用了个prority queue的方法，然后写一个自定义的comparator。大概就好了。最后他还主动帮我算了一下complexity，说是nlogk。感觉最好的话应该是自己主动来分析，大家可以注意这一点。. 1point 3acres 论坛

第三轮，白人小哥技术面。问了一个given一个电话号码的grid，可以给你去掉*和#（因为后面的内容imply这两个键也不会被hit），以及数字5（可能会问先你除了*和#还有什么可以去掉），规则是按马的日字型走，可以从任意一个键出发。目标是记录下来所有可以走到的长度为7的path，注意一个就是走过的格子还可以再回来，也就是访问过的格子不被标记。我一开始看到这个grid先想到了bfs，于是就按bfs的套路写，写到后面发现好像不太对，没法记录path。停下跟他讨论，发现还是应该用dfs。其实他一开始也暗示了dfs，我说用bfs他question了好几次。不过最后他说，那based on我现在写的这样怎么修改一下可以继续按bfs写完，解决方法就是在每一个path node里存一个已经visited过了的linked list。这样就不需要path.push_back(node)了。
-google 1point3acres
下午第一轮，白人大胡子大哥（貌似看到其他一篇里面也提到同样的人，估计就是同一个），问的是怎么设计一个linux里的find function，一模一样。我开始晕了半天，过一会他给我写了个File的class，里面有string name, bool isDir, vector<File> children，children里面是下一层的所有file/dir 名字，然后根据这个我写了一个 find class。基本就是loop当前层的所有file/dir name，判断这个东西是file还是dir，是dir的话继续recursive find。

最后一轮，美国大叔，system design，怎么collect ads的clicks的frequency，答的很差。。感觉他提示了很多实际场景，然后问我该用什么record click。最后问db怎么设计，说要存的时候可以按click happen的timestamp/frame 存，但是read的时候可能要按照advertiser来collect frequency。我画了半天也没画出个所以然。最后大叔终于放弃了我让我走了。。

第一轮 两个咖喱小哥哥（？也许不是）都工作了一年左右 主要是一号小哥问问题打字，二号小哥纯打字不出声，和口音相当重的一号半蒙带猜欢乐地聊完一堆BQ之后 coding题问的是涂色，就是画图工具那个填色，特别简单，我开始用了recursion,一号问说巨大的图怎么办，我就说再大的图，你要改的地方不大就行啦，然后小哥说就是要改的巨大，那我就想recursion的确性能不行，那就iteration呗，傻兮兮地想遍历的办法，结果突然就像柯南破案时候那个一道闪电打过！艾玛，这不是BFS嘛！然后就吭哧吭哧重新写代码。两个都写完正好时间到了，感觉一号有点不开心，心里有点方，感觉要没戏了，赶紧再找小哥挽回一下，结果1号还是不太开心，但是开始冷脸的二号开始笑嘻嘻的，结果一轮完了，他俩出去走了两步发现没地方可以去，又回来了！chance啊！我赶紧找他俩坐下又唠了几句，1号继续冷脸，二号继续笑眯眯，不知为啥。。。微笑送走。。。后来二号小哥哥路过我房门的时候还微笑跟我打了个招呼


第二轮 一个资深淡定咖喱小姐姐，说是已经工作了六七年了，见证亚麻的成长。也是先BQ，问完了之后，问了找出输入串istream里的各字符中最早出现的distinct的那个字符，我就hashmap搞定了，感觉也好简单，问了时间复杂度，也没别的follow up啥的，问完问题聊了聊公司就走了.留学论坛-一亩-三分地

.本文原创自1point3acres论坛
第三轮 两个dev manager，我猜应该就是bar raiser了，一个穿粉色polo衫的商务精英帅大叔主考官和一个穿印满粉色火烈鸟polo衫的澳洲口音（他自己说的）缓和气氛萌大叔shadow，问完BQ之后问了一个设计vending machine的题，而且要求找的零钱数量越少越好。我中间定义硬币的时候还因为不知道5分硬币叫啥问了一下，萌大叔立马接上说 这道题考的就是美国文化的认知，然后说开个玩笑，他也不知道。反正很萌！然后帅大叔告诉我了之后，我发现我还是不会拼，就这样吧，再问拼写有点傻，我就直接写五分了。。。最后我问问题的时候，时间有多，聊着聊着结果跟萌大叔聊得有点嗨，原来亚麻现在在加拿大推广的不太好，我立马说，就是就是，我现在在学商，知道全球化可难了，差点想给他背个波特的五力法则，然后发现帅大叔有点无聊之后，赶紧弥补一下，结果气氛又有点冷，我问了两个问题脑子有点空白，帅大叔就问我说，你不想知道你要去的组的详情吗？我心里一个哆嗦，艾玛，药丸！关键的忘问了！然后就赶紧问了，帅大叔一顿自豪地介绍之后，我有点想买个fire tv是怎么回事。。。


第四轮 是我最喜欢的一个疑似咖喱小哥哥（也可能是中东的？所以我说我分不出来啊），有点口音，刚工作了9个月，一脸朝气蓬勃长的也帅！斯斯文文的简直是我的type！他貌似是唯一一个看了我的简历的，还说我的经历很有趣。BQ的时候，我说的好了，他就说“make sense”，感觉简直是在夸我编得好，编的真有道理！我说偏了，他就赶紧让我再换个例子。。。然后一个设计题，是给了很多很多不间断的log，里面有各个模块，其中有个exception模块，好几条log拼成一个完整的exception，找出某个特定的app的Top 5的exception模块。我第一直觉用PriorityQueue，后来还是改HashMap了，全程小哥哥看我方向偏了就来提醒我，最后顺利设计了几个类和function就过了，我问问题的时候，觉得他挺亲近，就问了他传说中的加班问题。他说他每天10点上班，6点下班！纳尼(òωóױ)！这跟我听到的完全不一样啊！！！他每天都过得特别充实开心！他出门的时候，说他应该是最后一轮了，然后会是HR把我送走或者还要见什么人，结果正好HR来了，他问了之后，有点失望的祝我好运，所以我那时候满心都是凉凉了。。。

先说BQ。BQ我写了20多页没有重复的例子了，还怕你？随便你横着问，竖着问，我例子信手拈来。后面面试官都说我BQ答得不错。而且我BQ都是遵循“客户第一，省钱第二”的原则，想套路我也没那么容易，哼。

第一轮BQ，然后系统设计网上购物系统，面试官列了一大堆Feature让我设计，开始吓到了，这么多Feature，后来发现每个Feature说几句就行了，因为没那么多时间，所以面试官也没有针对每个Feaeture很深入的提问，所以总体蛮简单的。后来问了Scalibility和优化，无非就是Load balancer, replication, partition, single point of failure, CDN, cache什么的，面试官都没有细问任何细节。

第二轮全是BQ。

第三轮BQ，然后就是地里出现过的面经，给一堆用户浏览网站的Log，找出现次数最多的Transition，比如“主页->个人主页”，或者“个人主页->结账”，写完代码，面试官提醒了两次优化，终于把代码优化成一个For循环，最后还问了要是想找出现次数Top K的怎么办，用最小堆和最大堆都行，解释了下最小堆时间复杂度是nlgk，最大堆是nlgn。不知道这轮怎么算，因为让面试官提醒了两次要优化。

午饭，没什么说的，东西难吃死了。

第四轮BQ，然后就是岛的数量，还有一道类似的题，都是用BFS做。

第五轮BQ，然后也是刷题网站原题，外国字典。这题烙印有点坑，我一开始就说出了最好的答案，他说不可，让我用图来做，然后磕磕巴巴写了个有向图，写完了又说我该用无向图。而且中间他的很多观点都是错的，我都指正出来了，他和认为他是对的，我也懒得争，就按他的套路来。最后写的答案不是最优解，也没时间优化了。

我三年前去Amazon Onsite的时候完全不知道BQ这回事，答的一塌糊涂，虽然算法题答的好，但是没有Offer。今年又一次Onsite，Onsite前，我花了两个星期准备BQ，这两星期基本停止刷题了。针对不同的问题（这些问题地里都能找到），我写了20多页的例子。我之前在地里也看过帖子，有的人说Coding写的一般，但是BQ答的好，最后还是拿到了Offer。这次去面试我感同身受，有两轮我的Coding都答的一般般，但是最后还是拿到了Offer。甚至我和面试官谈笑风生，BQ聊了30分钟，最后面试官没那么多时间，只能出道简单的算法题哈哈。

所以，兄弟们，真的要重视BQ，在Onsite前两周开始准备。Coding部分，你只要有解法，代码写的一般也没关系，不是最优解也没关系，但是BQ答的好，你还是有很大可能拿Offer的。-google 1point3acres
记住回答BQ问题时永远不要违背Amazon的最重要的两点：一切为了顾客（最最最重要）；能省钱就省钱。

至于System Design的话，Youtube上多看几个视频，再读几篇博客就行了，没那么难。

另外，Hiring Manager一直夸我BQ答的好，大手一挥，给了120K Sign on bonus。

共4轮。. 牛人云集,一亩三分地
1. 很友善的白人小哥。从BQ开始，最后code.
给一个string,比如“hello, world!” 然后一组 2d array, [[2,6,a] [3,9,b] ,[5,10,c] ] , a,b,c 是xml 的tag, 2 代表string中的起点， 6 代表string中的end position， 写出有效的 xml string。 "he<a>l<b>lo<c>w</a>....." 但是需要valid, 就是要最后变成 "he<a>l</a><b>lo</b><c>w</a>....."这样
时间少了10分钟，我自然是没写完，给了个大概思路，小哥连声说very good. 现在想起来，小哥只是安抚我。汗。
2. 这个是重点！！！！！
阿三哥 加白人女shadow. 留学申请论坛-一亩三分地
一上来BQ， 然后coding. more info on 1point3acres
阿三哥一开始问我玩不玩ball game, 我赶紧说不玩，然后又问，知道怎么玩吗，我说不知道。真是听都没听说过。然后shadow 看向阿三，意思很明显呀，不应该问我不知道的game呀，可阿三哥眼睛不眨一下开始给我讲规则，我去，我听都没法听全规则，怎么写code? 阿三连屁股都不想挪，不把规则写在白板上。反正我就这么稀里糊涂地边问边写。他坐一边纠正我。基本是到了最后一分钟我才明白这个ball game到底是咋回事。
就是一 board 有n 个cells, 有一个die, 1-6, roll 出多少就跳几步。 cell 有 3 种情况，如果是字母就前行几步，如果是蛇就后退几步。如果是空的就重新扔die.  最后就最少的步数到终点
不知在蠡口上有没有这样的题？
3. 印度小姑凉，很友善。 Bq + coding : 找出字符串组中包含两个words的字符串。 bq 问得非常细。
4 两个很友善的白人帅哥，(觉得他两基情满满) 一个是hm,另一个应该是bar raiser.
BQ + system design  设计tinyurl  BQ问得比较多，但过程感觉很轻松 来源一亩.三分地论坛. 

Round 1 
烙印 有口音 先BQ瞎BB 10分钟后上板

Given a list of folder names, findout their top most common parent folder
[abc/def/opq, abc/def, xyz ]
return [abc/def, xyz]
用Trie结构秒

让你介绍下你现在工作的产品 来源一亩.三分地论坛. 
主要想听你讲你负责的那部分


Round 2
白人小哥 已秃头
BQ 20分钟 问你有没有自己主动做project 聊的略high

上板 Design AWS marketplace， 你没听错
小哥出题先画出大致流程， 感觉他也不知道要问啥。。
我说这块traffic会比较多 需要用cache缓冲 他点点头
那块storage需要replica防止single point of failure 他又点点头. 1point 3acres 论坛
然后让我写出API出来 啊， 顺间变OOD Design了
思维有点跳跃 感觉到最后10分钟意识到题的意思. more info on 1point3acres
结束时小哥握手无力 估计没戏 还拍了照
饭都吃不下了

Lunch 
中东小哥 刚来两年 开门见山说他不参与面试 你尽管吃
我问他拍照了是否就GG了
他说每人面试方法不一 有的喜欢记笔记 有的喜欢拍照
他应该面每人都拍照， 没事的
然后说他当年面试也被拍了 结果进了
不知真假 只能调整心态 下午再干. From 1point 3acres bbs

Round 3 
烙印 hiring manager 果然是领导 英文特6 毫无口音
全面BQ 围绕2B 军规 问的非常Technicial. visit 1point3acres for more.
要注意了 如果是编的故事 必须得符合实际 不然会被问傻.留学论坛-一亩-三分地

半小时后上板设计两个UX页面， 一听就开心，终于问到拿手活了
答得烙印乐呵呵的开始和我讲team里的流程了

Round 4
白人 视频面 屎一样的experience
白板反光他看不清楚 只能写下半部 字还得写的大 不然他视频看不见
已经只有半块板了 还要我字写得大 真想把电视机砸了
面对黑板讲话他又听不清 小哥又生病一直咳嗽和我道歉

BQ: A time when you work so hard but everyone disagrees with you
根本他妈没发生过啊， 只能硬编 结果还被疯狂追问 回答一般般

还是上板做题：
LRU Cache 瞬秒
Find circular dependency: DFS解 有BUG 但面试结束前发现了. 牛人云集,一亩三分地
. more info on 1point3acres
感觉这轮答得最差 可能是下午状态不好加2B视频面试


Round 5
认真脸白人 爸爸级人物 说话非常Calm 不怎么笑 但很强
BQ: A time when you face a challenging problem and how you solve it.
问的特别详细， 听得头头是道， 完全听懂的我的例子还同意了我的解决方案. 围观我们@1point 3 acres

笑着说 我知道你挺累了 但你不介意咱就上板吧
岛题 变种 0 and 1 都被看成是岛
找到0 和 1岛的最大size 还是标准DFS秒， 毕竟原题是可以闭着眼睛写的
追问当矩阵大到内存放不下怎么解 （没答出 大牛求助！）

面之前在地里看见说A家痴迷于问bq，于是专门找时间看了板上大牛总结的bq帖子，帮助很大！！主要就是对着14条a家leadership principle想例子，一个例子可以套用到多条principle上。这个时候千万不要限制自己的想象力！！一定要放飞自我！做过的没做过但是见过的都可以讲！

我是找同学内推的，直接推的go的岗位，然后联系oa，店面，中间隔了都有一个礼拜，不得不说a家还是挺慢的...onsite一共五轮，加午饭，当天面试楼还在整体搬家，所以面试官都是直接从家里赶过来专门为了面试的，感恩￼
{hide=188}
1. 第一轮hiring manager面，问了大概有半个小时的bq，全方位立体化，还好是早上精力充沛脑子也还可以，基本都招架住了
coding不难，具体题目忘了，之后还有一个debug，就是看两个代码小片段，先说bug和有bug下的输出，怎么改进，如果要变成multithread怎么加锁
2. 国人大哥，sde2 十分nice，问了几个bq
coding是bigInteger lc题，给两个很长的linkedList代表两个数，输出他们相加的结果，结果也用linkedlist表示
秒了之后大哥指出了一些可以让code看起来更加clean的地方，总体ok，还顺便提了一句他面到现在我是唯一一个做出这个题的 ORZ
3. 天竺姐姐manager+shadow 给出一个string，里面是26个字母，大小写都有可
定义string的变形就是可以把string里任意一个字符大写变小写或者小写变大写
i.e. input: iT output: it,IT,iT,It
午饭：印度哥哥，从a家印度那边transfer过来的，带去了go的店里买午饭
4. 忘了...
5. 毛姐姐！金光闪闪的大链子可吓坏宝宝了，还有一个shadow 这轮也问了很多bq，各种给我一个情景***你是怎么处理的
system design 设计一个chat system 从1对1聊天开始，最后没时间了简单说了一下group chat和推拉模型

整体感觉就是coding不难，然后一定要好好准备bq，这样可以在面试当天省下很多脑细胞，可以更加focus on coding和design
{/hide}

Onsite:4 rounds. 15-20 mins for behavior questions in each round.
1. Packagedependency （topological sorting）
2. Designgoogle drive or dropbox. (System design)
3. Poker design（follow up: other poker game，even not poker）。（OOD）
4. 2problems: Print bottom view of a binary tree;
Dictionary ----> phone number, 4 digits,e.g., DEAD -> 3323, FEBE->3323.
. from: 1point3acres 
Given a phone number, find all possibleletter combinations in the dictionary.

. 一亩-三分-地，独家发布
behavior questions就参照14个principals准备，每个都准备至少两个stories。

最后想说的是，一定要坚持，在暗处的日子不好过，多想想坚持的理由吧。
希望大家都能收获心仪的offer。

昨天刚面完，总共5轮。
先说BQ。BQ我写了20多页没有重复的例子了，还怕你？随便你横着问，竖着问，我例子信手拈来。后面面试官都说我BQ答得不错。而且我BQ都是遵循“客户第一，省钱第二”的原则，想套路我也没那么容易，哼。


第一轮BQ，然后系统设计网上购物系统，面试官列了一大堆Feature让我设计，开始吓到了，这么多Feature，后来发现每个Feature说几句就行了，因为没那么多时间，所以面试官也没有针对每个Feaeture很深入的提问，所以总体蛮简单的。后来问了Scalibility和优化，无非就是Load balancer, replication, partition, single point of failure, CDN, cache什么的，面试官都没有细问任何细节。

第二轮全是BQ。

第三轮BQ，然后就是地里出现过的面经，给一堆用户浏览网站的Log，找出现次数最多的Transition，比如“主页->个人主页”，或者“个人主页->结账”，写完代码，面试官提醒了两次优化，终于把代码优化成一个For循环，最后还问了要是想找出现次数Top K的怎么办，用最小堆和最大堆都行，解释了下最小堆时间复杂度是nlgk，最大堆是nlgn。不知道这轮怎么算，因为让面试官提醒了两次要优化。

午饭，没什么说的，东西难吃死了。

第四轮BQ，然后就是岛的数量，还有一道类似的题，都是用BFS做。

第五轮BQ，然后也是刷题网站原题，外国字典。这题烙印有点坑，我一开始就说出了最好的答案，他说不可，让我用图来做，然后磕磕巴巴写了个有向图，写完了又说我该用无向图。而且中间他的很多观点都是错的，我都指正出来了，他和认为他是对的，我也懒得争，就按他的套路来。最后写的答案不是最优解，也没时间优化了。


店面: 利口 二舅舅， 奶牛

昂赛: Behavior 必问，楼主就昨晚飞过来的时候看了一下，很多就把我问蒙了，都不知道怎么现场编故事。

一轮：白人小哥：儿茶树，计算每一列的和，就是利口里 假设根位子为0，往左减1，往右加1，然后相同位子的算和，从左往右根据顺序返回一个vector
                                      然后计算每一行的和
                                      然后自己创造一个儿茶树，去演算自己的代码

二轮：白人小哥：设计题，有很多主机在不同的路由器下，主机上跑很多kvm, 然后这些路由器又都在一个根路由下面，设计一个服务，根路由想要知道任意一个kvm跑了多少流量。
                         后来简化了一下，梗路由子网之间的kvm流量不需要算，只要知道经过梗路由出去的流量。 来源一亩.三分地论坛. 

                         楼主扯了半天才搞明白题意，就说KVM假设192的地址，主机是10的地址，做静态的NAT绑定，加端口号，所以每次kvm出去的包，源ip地址就是10，这样梗路由根据地址+端口号可以做key，然后每次去加包的大小，最后小哥哥说至少能做，但是怎么scale? 但是，没有但是，最后没时间了。欢迎大家一起讨论讨论。

三轮：看上去像三哥哥，带去吃个午饭，我以为仅仅只是吃午饭，没想到1点的时候他还是老神在在的坐在那儿，进来一个国人大哥，三哥哥说他是hiring manager, 他们两个面，全是behavior，所以一塌糊涂，最后国人大哥说我问你个算法题吧，不需要写，1）怎么找一个array的top k, 答：priority queue. 2)如果这个array非常非常大，机器内存一次读不了，怎么办？答：我感觉做法是不是利口 死 稍微改改能做，就说假如这个array被分到n个机器上，然后排序，每次对比每个机器上的k/n最大的那个，就表明，这个机器上前k/n个肯定是答案的一部分，然后再继续对比（k-k/n)/n，一直到只剩最后一个，大哥说可能能做，然后问大小对是怎么工作的。
三哥哥后来也加了一个问题因为我是做c的，所以问局部变量，堆，全局变量分别存哪儿？2）段错误是什么？cpu, kernel对段错误是怎么工作的

四轮：白人小姐姐，说是要设计一个最近看过的书或者电影的列表，根据每个客户的记录。我说不是lru吗，就写了双链表的增删，弄了一个map做哈希。但其实类设计的很乱，感觉很不好，最后小姐姐拍了一下，我记得之前有个帖子说是写的东西也被拍照了，然后挂了。好吧。。。

五轮：三哥哥和一个国人小姐姐，三哥哥主问，小姐姐助攻，利口 二舅起

楼主之前在亚马逊的网站里面投了一堆职位，一直以来也没啥回音。这个月前一段时间突然接到亚麻HR的邮件，说有一个PM的职位，问我感兴趣不。我说可以。然后很快就和HR有了第一轮电面，解释聊了一下职位，我的背景，介绍，一些有的没的东西。
第二面和HM刚面完，说最多45分钟，结果面了一个小时。而且全程没有BQ，我也是觉得我自己面了假的亚麻。
HM上来先介绍组，然后闲聊了两句，然后就是让我自我介绍。接下来，全程都是case。我已开始想，估计一个case，余下都是BQ了，结果没想到没有一个BQ。
这个是在amazon supply chain底下的。所以Case基本都是怎么预测需求，然后预测完了，怎么安排车，安排人。对于peak的season，如果我们要加人怎么办，然后还有讨论到一些time series的方法各种各样，还有一些计算题。我面着面着感觉说这个PM职位怎么会这么technical，如果这么多事情都要PM做，那PM哪还有精力管项目啊。
结果等我面完了，HM说他下面有PM的职位，也有BIE的职位。他觉得我的背景更适合BIE，所以就问了这么多technical的问题。然后问我考不考虑BIE，我说可以没问题。然后他就说必须让我选一个，一个劲儿引导我选BIE。我说可以。我暂时也更喜欢做一些hands-on的东西。然后说他就跟HR说一下之类的。

之前准备了几天的BQ，一个没问。而且我看地里的面经，亚麻也很少问case。没想到今天被我碰到了个特例。整整一个小时啊。

希望有onsite，同时希望以上对大家会有帮助。

周五刚面的，趁记得内容赶紧和大家分享一下
总共五轮，午饭不算
这个组在aws里面算比较新吧，虽然有不少烙印，但是人都特别好，陪我吃饭那轮的三哥全程陪笑，可爱到不行
下面是干货
第一轮：可能是中东人吧，也特别客气，先bq，问了利特抠212，也是给了字典是否存在单词的api，所以代码量没有很多
之后就吃午饭了。。。。因为他们安排的关系吧
第二轮：大小manager，大manager shadow，bq+系统设计，系统设计考了淘宝网站鼻祖的竞拍模式，lz表示近大半年没见人面过这题，所以就只能基本套路，往high level套，什么hosting server啊，lb啊，身份验证，竞拍行动的服务器，加上用户数据库，竞拍货物数据库，每次bid的数据库，monitor，sharding啥的，毕竟面sde2。据说扯api，interface什么的都是刚毕业孩子玩的。。。人不待见。当然反响感觉也一般，两个manager可能见惯了我这种吹牛逼的，所以也有点虚
第三轮：我最虚的一轮，国人小哥加印度小兄弟，人都很好，英语说的贼溜。还是BQ+coding，来了道简单到感动的题，基本上就是map里面配个heap，问题是这个heap需要保持，所以每次poll出来再送进去我表示很不喜欢，想一步到位，用了iterator，结果国人小哥当场搜索java 库，提示我这个iterator是随机的，呵呵呵呵，玩砸了。只能从pq里面拉出来推到list再塞回去，lz觉得这么做反正是死定了。后来回程飞机上想到可以用bst去维护，但是时间长了这个bst还是会严重的unbalanced,所以。。。。要挂的话这轮肯定是最主要的。当然国人小哥还是一直在善意的提醒，有错的地方也很及时提醒，这点需要表扬。。。in case这哥们也上这里寻找素材，马屁先拍好。
第四轮：来了个l6的吧，别问我为什么会知道，这年头不认识几个亚麻的朋友还好意思出去跟人打招呼。bq+coding，题很简单，画题板。不会做的把bfs dfs整明白了先。先用dfs写了，考官说不错，但是太吃内存，我表示那就bfs吧，说了说思路， 考官说不用写了，懂你。接着就继续聊天，这轮属于纯聊天，coding是给大家一个喝水的机会吧，这轮应该不会有什么问题
第五轮，其他组的l6，纯bq，我就直接问他是不是br了，人家害羞的一笑，你咋知道， 我说你电脑上贴着s3和prime video，反正我今天面的肯定不是这两组。问了一堆跟客户满意度有关的bq，确实刨根问底的厉害，反正不光问了你怎么处理，还问为什么要这么处理，有什么好处。鉴于lz多年工作经验，应对这种有意也好无意也好的打断，假装不懂，真不懂，完全不当回事。小年轻们记得表情要真诚，哪怕你觉得对面是故意搞你，你就当他是有些健忘的亲奶奶，亲外婆，一年就见一次，好好哄着。
总结一下，我这个面试应该算运气不错，没碰到特别的题，系统设计也没有为难我，虽然我答的也一般。bq我觉得还行吧，我每条都有两个左右例子。
祝大家都有理想的offer，加油

BQ:
1. Tell me about youself. . from: 1point3acres 
2. What is the project that you are most proud of.

code:
lc 347的变.

去年去亚麻的纽约office的video组面了一把，回馈给大家。时间有点久远，记得不太全

1. 系统设计：设计一个图片上传和浏览系统，算是很经典的一道题目啦
使用prefix tree存储电话号码

2. 算法：从一个数字stream不停读取数字，获取当前最大的N个数字
有N个数字stream，读取并merge它们

3. Behavior问题：略

总的来说不难，behavior相关的问题倒是又多又无聊


BQ: What drew you to your current team? How did you handle competing priorities?
What happens after you press the power button on a Linux OS?
What happens after you enter a url in the browser?
given a log file of each operation and runtime, output each operation’s min and max runtime
input: operation1, 100
          operation2, 200
          operation1, 400
          operation2, 500
output: operation1, 100, 400
             operation2, 200, 500


介绍自己
问project(问得很细)
最感兴趣的project
举个为了project完成的牺牲
project要deadline了，完不成怎么办？
怎么实现一个set（答hashmap） 来源一亩.三分地论坛. 
最喜欢的data structure, why. (priority queue,全能型)
有什么会影响hashtable的efficience（答 hashcode collision.）. Waral 博客有更多文章,
怎么找facebook  A和B是有联系的。follow up 是怎么缩短time complexity.（答BFS, 两点一起BFS）
怎么找linkedList里有circle(双指针，slow and fast. 面官纠结万一一个指针一直是odd,另一个是even呢？后来他自已想了一下，没让我答了，slow那个是odd even 都跑的)

以上问题搞完，只剩下15分钟了（45分钟里的最后15分钟）。我心里想：这么好？不用coding？只要说一下就好了？ 然后就是太天真了，下面是coding
说实话，也不难
找两个arrays里两个相同的数。(把一个array放hashmap里，另一个遍历在hashmap里找。). 1point 3acres 论坛
follow up 是怎么做到O(1)空间（sort 一个array, 另一个遍历，Binary search sorted array）

设计广告campaign系统的一个功能，用来插入或者修改campaign。数据结构自选。两个campaign的运行时间不能有交叉。我用的双向链表和HashMap，还想用二叉树搜索来加快速度，被告知不用那么复杂，O(n)就行了。感觉有点被自己复杂化了，还好及早悬崖勒马。答完后还有10分钟，就闲扯了会儿。面试官感觉像ABC，不确定。

aws glue经理直接推荐的面试

是一个三姐，但一听就是美国人。

上来25分钟的bq，就很正常的bq，问项目，问怎么解决困难之类的

code：
1. reverse string
2. implement queue

都是在collabedit上写，全是空的，她口述题目你来写。

queue用doubly linked list写的， 当时有点紧张把class fields全放 constructor里面declair了，估计是挂在了这里， 面官从头到尾也没指出，今天自己才想到。 其他就是实现enqueue，dequeue，delete （面官让自己想queue需要实现什么function）

一共50分钟吧

隔天就收到了拒信，不提供理由。

最想做的方向和公司，然而自己的细节没做。 那个组有一点不好，从recruiter到engineer到manager全是三哥三姐

近期的亚麻店面，蠡口785，没有变形。
没做过，边做边上网看资料，理解题意后，发现是图的遍历加状态维护，楼主用BFS做的

code写出来了，但没有考虑到edge case图是否是强连通图, 最后问了一下时间复杂度和空间复杂度

走过路过加个米，有些帖子还是看不到，谢谢大家！

BQ
1. 最有挑战的项目
2. 和teammate有冲突怎么办
3. 做过的项目的tradeoff

Technical
链表和数组的区别
用数组实现queue

面的是湾区的组，但是放到了虾图面。一共4轮，三轮烙印，凉凉送给自己。
1. bq  + 题 一个arr存bit，一个数组的list，每个数组两个数字，求arr里对应的两个index的这段range的或值。要求算法复杂度O(n)。
2. bq + 系统设计：停车场
3. bq + 蠡口 姚伞玲
4. bq + json parser. 围观我们@1point 3 acres

每个题 大概都只给了15min。。。
卤煮蠡口 没练的很熟。。时间感觉很紧。。

round1: 一个senior manager和烙印哥， bq20分钟，system design是做netflix的视频在线播放，system design我很弱，答的不在点上。
round2: 两个烙印组合，bq20分钟，里抠骑士，step变成n。
round3: 小姐姐，bq20分钟，利口吾霸拔，题目稍微改了，所以要考虑一下case
round4: 白哥，bq20分钟，李扣遥而遛。

1. 白人小哥和国人shadow bq + log题目，有customID，sessionID，timestamp，url，返回top 5 most frequent last update的session的url
解释有点复杂，其实就是log里面的一个session会有很多url，假设最后一个url才是要统计的，之前的都不算，找到所有last url一样的session的count，top 5 most. 1point3acres
2. 隔壁组的白人manager，听一块的小伙伴说是bar raiser。 bq + 第一个非重复的字符，要求一遍， 然后问了个树序列化，开始蒙了说了要用前序+中序两个遍历来保存树的结构，后来提醒说任意字符都能保存，才想起来应该直接一个前序就行，然后解释完了没有code
3. 国人manager+白人manager， bq+设计社交网络
4. 三哥 bq+蠡口其实无，从hashmap方法说起，讲了几个笨办法，但是说到hashmap的方法就让我写了，没有写两个指针，不知道有没有被坑；. 牛人云集,一亩三分地
一个巴士有好几个stop [1，2，5]， [5， 8，9]， [8，7，6]，起点2，终点7，最少换乘的巴士数量

Amazon 西雅图downtown campus onsite面试
14原则要好好读，每一个coding面试后面都会问几个小问题，感觉都是围绕着14原则。
我面的是web前端工程师

1. 年轻烙印小组长：system design问题，设计一个简单的calendar web app，类似google calendar

2. 白人美女：问如何不用任何框架下（如jquery），用js生写一个支持动态update的table
3. 年轻白人小伙+一个烙印妹子intern：简单BFS问题，后来问题变化了一下，改用DFS。基本上考简单数据结构
4. 白人老头（貌似是bar raiser，言语特别苛刻）：问著名的josephus problem，生写code
5. 中年烙印经理：全问behavior问题，拥抱14原则

上午面完，下午马上有通知了。拿到recruiter口头上的SDE II的offer &#128591;

我打乱下顺序

1. jukebox 系统设计。 这个cracking貌似有
2. fill 这个功能，在画板里。就是把一块区域颜色涂成想要的颜色。 不解释啦，直接DFS
3. 把睿蛇（如果能辨别这个人是把睿蛇，就看他的team和其他人的team不一样）： 围棋判断一个子被capture与否，被capture的定义就是这子或这子属于的整块同色子区域被另外颜色子包围。 
解法也很简单， dfs。 每次recusive call返回是否被capture, 遇到异色子或者出界都是true, 遇到同色子就recursively去call它。 
4. 纯BQ
5. 纯BQ

amazon的BQ问得非常非常做，每轮都要10分钟以上在讲那些。很多问题都需要给出例子：比如你做过最失败的事情的是什么 - -！ 无语了。
我敢说这些没准备好，无论你技术答得多好都有可能挂！ 很傻B吧， 我也觉得很傻B，但他就这样。

楼主技术题全部秒过了， 第4轮BQ有个BQ问题没答好，然后真的那个hiring manager就没要我，我也不想鸟他，感觉有点傻B傻B的。 
后面的BQ还聊得行，加上把睿蛇围棋那轮代码写得很快很简洁，onsite后3小时就直接受到offer了。 

后面问得知，把睿蛇那轮起决定性作用！ 那轮没答好，可能会秒挂！ 大家注意啦。得把那人聊开心了！

之前看了地里面经，所以感觉有义务回报！ 住大家面试顺利

Round 1: 
nice lady, aws组的
先是BQ 30mins. 然后算法题链表基本操作, 找到第k个node, 还有 intersection of linkedlist 比较简单, 注意边界条件
面试过程中面试官pager还响了, 处理了一小会儿. = = 

Round 2:
大叔. BQ 20mins
然后系统设计, CAP理论, 一致性hash, 设计一个爬虫爬Amazon.com.
然后是一道多重背包题目. 大意是: 有一些不同容量的盒子来装棒球, 比如6, 9, 15  然后有一个n个棒球, 求恰好装满情况下, 使用最小盒子的情况. 留学申请论坛-一亩三分地

Round 3:
德国lady
基本全程BQ, 最后问了一道关于invoice怎么判重的题目, 因为国内没有这类发票操作, 没有太明白 :(

Round 4:
白人妹子和肌肉男
基本全程BQ, tell me a time you overcomimt to your constumers之类的, 开启尬聊模式
. 留学申请论坛-一亩三分地

Round 5:
白人妹子和小哥
也是先BQ, 然后问了简单算法题目, 关于二叉树和链表的操作的



估计下周出结果吧. 求不跪.

体验就是:
亚麻真是出了名的BQ啊
leadership principle中每一条至少要准备一个例子吧
不过面试官都还是很nice的

1月底内推，三天后回复…oa和电面隔了不到两周…速战速决
上周五下午电面，白人小哥，名字叫Travis.
1. 双方自我介绍，聊简历和project
2. 有一些customer的数据，每个customer都有一个rate，给两个sorted customer list
我说写个comparator，新建个list，放进去就自动排好了（想得美），小哥说不不不直接sort，可以arraylist，可以linkedlist，然后写代码
(Leetcode: Merge two linked list)
追问：时空复杂度。如果数据是immutable的，时空复杂度还一样么？
3. OO题. 有个Shape父类，设计Circle, Rectangle, Square…子类. 畅所欲言就好了，主要考继承和多态.
4. 什么是Balanced Binary Search Tree? 为什么要Balanced的?应用有哪些？
5. 又有一些customer的数据，你想要怎么存？
在给答案之前问了： 数据有多少？(多) 
我给了两个：BST(方便插入，排序）和TreeSet（进一步方便遍历，打印名单这类…). 其实这类问题应该多问些具体要求的，比如quick insert？quick search? traversal?
小哥追加了要求：不要求排序，只要求快速插入
给了arraylist. 追问：run out of space怎么办? 我说拆成几个arraylist，组成个arraylist<arraylist>
追问：还是有run out of space的问题…最后磨蹭了半天，讨论了一会儿，给了linkedlist，因为只用存reference…
6. 问问题环节…小哥说这周二或周三出结果…已经周三了还没信…发面经攒点人品先…
自我感觉面的题挺简单的，但答得不太好…还是求offer吧…再求点面试…

1. BQ
烙印大叔hiring manager。问BQ的项目的时候还问我系统设计相关的，问我怎么知道我的项目可以release了，万一服务器占用率超高80%怎么办。其间还做了一道简单的统计文件里面的数次出现次数的题，follow up是如果有1m个文件怎么办，我说可以用map reduce 来处理。
2. BQ + OOD
白人大哥视频面试。 设计一个linux文件查询系统，根据文件路径和constraint来查找返回符合的文件。比较开放的问题，返回类型，constraint的定义，各种corner case都需要和面试官讨论出来。

中午和一个白人小哥吃饭，就扯些有的没的。他打lol我打dota,互相鄙视了一番。


3. BQ + 做题.1point3acres网
也是视频面试，三哥hiring manager + 白人大哥非shadow. 三哥负责BQ，在我回答过程中连说great, great, great。白人大哥出了道题，具体是给你一一段话把里面的price reduce by 15%。比如：xxx xxxx xxx $100, xxxxx 然后返回： xxx xxxx xxx $85。一开始他input没有打双引号以为就是一串数字，扯了10分钟才意识到。这个问题也比较开放，不要求写出完整代码。我的思路是用空格split string转换成array， 如果遇到$ 标志则判断isNumber，如果是然后用String.replace替换成折扣后的价格。其中有个bug, 如果里面价格有duplicate结果就会出错，这个是我主动提出来的，然后自己也想到解决方案。

.本文原创自1point3acres论坛
4. BQ + 做题
还是视频面试。。。真是大规模电面演练啊。西雅图的白人大叔，应该是bar raiser。 BQ前面实在问得太过例子不够了，一开始卡壳，然后他换了一个问题我答的很流畅。题是利口药饵榴简化版。半个小时做这个题，没人能写得出来。他问我怎么表示graph, 用什么方法来输出路径。我一开始说BFS，居然没有提醒我BFS是错的，不能得到路径。写完了才意识到。然后我立马反应过来用DFS，这个时候他又要求输出最短路径。这不就是单词爬梯贰吗。。最后说了下思路，没有写完代码。. 1point 3acres 论坛


5. BQ + 系统设计.1point3acres网
现场面，白人大叔hiring manager。设计以一个user rating 系统，比较简单。我先是扯了流量和storage预测，然后画出来high level design, 把scalability 提前考虑进去了。然后他叫我写api定义。api parameter用了userid，在他的提示下改成session key了。还把我的high level design照了下来。正面面试结束后又花了15分钟给我仔细介绍亚麻，他们组做什么，亚麻的内部transfer政策这些。


整体感觉是BQ多得超乎我的预期。幸好我准备充分，几乎没有卡壳的地方，也能接住在BQ中面试官的challenge。题的话似乎亚麻不在意最后能不能写出bug free的完整代码，因为一是时间不够，二是题是开放式的，最后做出来讨论出来的结果每个人都不一样。关键是要和面试官多交流，自己要主动出击而且能接得住面试官的刁难。. visit 1point3acres for more.


发个面经攒攒人品求过啊。

个人感觉直接OA2拿到面试的不多的 其实大多数人还是要面试的 所以还是请同学们尽早准备
然后约了2月13号早上11:00的电面
接电话的是个三哥 一开始没听出来. visit 1point3acres for more.

一共两个问题：. from: 1point3acres 
第一问：
  上来就让我想一个数据结构来实现三个功能
     insert(key,value){}
     search(){}
     delete(){} .本文原创自1point3acres论坛
  让我用尽可能优的时间复杂度
  我说hashMap他说换一个
  当时脑子一热没想起来其他的 乱说了一个heap
  三哥提示说balanced BST
  我说我知道BST的时间复杂度是O(logn)
  然后三哥问我最坏情况 我说O(n) <当时没反应过来这是hint>
  于是老实说 我想不起来了但是实现的时候 我应该会做. 围观我们@1point 3 acres

第二问：.1point3acres网
以下内容需要积分高于 155 才可浏览

就是word Ladder 我想了一下我说 是不是BFS做的... 
  因为面试准备的一周时间把lintcode做过的100多题刷了一遍
  面经群里大家多次提到这题 于是leetcode里面也刷了几遍 于是20分钟就写完了 
  然后让我check一下... 口头跑case 和分析时间复杂度 
  只用ABC三个字母 用了很多很多提示 最后我说是O(k^3) 三哥说是O(3^k)

亚麻艾利克斯啊sunnyvale的 之前以为H1b没中就投了一个，寻思至少能够外派他乡，就急急忙忙约了OA。结果H1b抽到了，也通知我要去onsite了，约到了上周五7.20的onsite，今天早上HR发邮件问什么时候可以电话，中午打来电话说有offer了，不过hiring mannger还在match组，说是明天聊package。
Onsite总体感觉体验还不错，吐槽一点那个大楼地址是1120并不是邮件里说的1200，害得我饶了两圈不敢进，最后还是一个同去面试的小哥告诉我就是这个楼才进的。

第一轮 是个白人小哥，一看就感觉很geek，略微有口吃这种的语言障碍，说话非常非常非常慢，上来问的BQ：说一个别人觉得还不错可以停下，但你还是坚持做的更好的案例； 说一个你拿了什么奖或者荣誉；说一个take risk的；说一个你比较创新的 我感觉我说了一大堆，他没有任何反馈，说了一句 我很想问你点follow up 但不知道该问啥。。。 之后问了一个 OO design， 让设计一个在线可以买电脑的系统，要求客户可以定制显卡，cpu之类的，然后可以生成订单，还有一些model是预设的，用户可以选择这些model，也可以再基础上定制。做完之后大概剩10分钟，我问了一下他工作相关的，明显感觉他可以流畅一些的对话了，感觉聊天聊得挺开心的。

第二轮是个三哥哥的hiring maneger， 上来也是问bq：tough comment；take risk； innovation 好像是，感觉他不断chanllange我为什么bq里的这个实例要这么设计，搞得我又涂又画的，最后剩下20分钟，coding 一个 serialize and deserialize 一个binary tree， 就是蠡口hard那个。。 5分钟白板画了个图，解释了一下，然后开始写， 估计写了10分钟。follow up是如果不是一个integer node， 是个string node， 可能包含你的spliter， 怎么办。。我一开始没反应过来，说可以再弄个array，记录一下是node还是spliter，后来他提示说能不能把spliter escape掉，才想到可以escape， 解释了一下 感觉他还挺满意的。 之后聊了两句就没了

第三轮是个三姐，上来问system design， 设计一个 %&%￥#￥一样的app， 我完全没听懂是什么东西，他说类似于Expedia的旅游app。。。我本人从没用过那个，之前都是studentuniverse买票，或者官网直接买票有积分的，能给我讲讲都啥功能么。。。她就把题简化了（貌似）， 说要设计flight查询，可以查non-stop 或是不non-stop的所有从A到B 的航班。 我大概问了一下QPS什么的，其实不重要，她说你就想象成需要你scale的那么多就好。 我一开始没太理解这个stop的玄机，以为一个航班从A到B stop直接就有了。。她说要像
101 A-》B
102 A -》C 
103 C-》B
104 A-》C -》B
这种的。。。感觉是个graph的题，我说我想把non-stop限制到小于3， 然后如果是non-stop 就直接查表，1 stop 就两个query A-》 *（！B） 然后从这个list里 再 query -》B 的把结果放进另一个表里。 其实不知道可不可行，没什么这个的经验。。然后她就问了怎么improve performance啊，其实就是cache，问了cache key啥的。。 之后就是BQ， 问我怎么debug， 如果一个website down了，你会怎么debug。。。感觉就是各个layer查log。 之后又问了你被maneger disapprove 了的事例 之后就聊聊天就没了

第四轮是个白人小哥，有三年经验。 BQ：dive deep an issue and find the root cause 之类的，还有take risk的。。 可能还有别的，忘记了。。 之后coding， 一个n-nary tree，要给定depth的level的最大值， 就一个bfs。 然后follow up 是返回每一层的最大值的一个list， 没啥差别感觉。。。 大哥感觉对bfs不是很熟，问我为啥不用dfs。我觉得这个题应该是bfs比较直觉吧，再说dfs， recursive写法用call stack空间，相比较heap空间容易爆栈。 我极力避免在production code写recursion。。 然后最后我问了 what is your favorite perk here？ 他说没perk。。。你要是想要perk你不该来这。。。你手里那个bottle water 是只给面试人的，面试官都没有。。。 然后就walk out了。。。

过resume 自我介绍
BQ 问customer focus的經驗
string reverse
判断 BST - 我用recursion做, 要求case带入 (recursive code 带入case还真麻煩)
判断 BST - 要求用iterative做

1. 亚裔硬件项目经理，全程BQ，挖的很深：问了组员不合作怎么办，如何让他们合作；跟老板意见不同怎么办，列出听老板的和没听老板的情况；等等
    每个问题都聊得很仔细，需要举例给出比较细节的过程。
2. 印度经理BR，谷歌跳过来的，人非常友好。题目是LRU，然后边分析边写，看楼主的思路都有就没有让楼主去Add方法，中间被拍照了，说是因为白板不够大需要记录。最后又问了两个BQ。. 一亩-三分-地，独家发布
    补充一个细节：面试完楼主想要去厕所，厕所在面试区域外。这个经理亲自给楼主开门，然后在厕所外等楼主去完再把楼主送回面试间，整个体验非常赞。.本文原创自1point3acres论坛
3. 用美国人名字的烙印，开始想问LRU，楼主说刚刚被问到了，然后换了一个题目。给一堆（员工，经理）的对对数组，让找出每个经理管理员工的数量。
    例如：输入是（A, B）(C, B) (B, D)，结果就是（A, 0）(B, 2) (C, 0) (D, 3)
    题目问完依旧是两个BQ
4. 两个烙印，一个工作3年多的主面，另一个刚入职的做影子。题目是OOD，设计File System。结束依旧是两个BQ，而且居然问到了为何要来亚马逊这样的问题。
    主面的烙印显得非常油条，新来的烙印则是非常青涩友好，感慨一下日子混久了人是会变的

BQ
- Most Challenge Task?
- Tell me a situation when you do the work outside of your scope?
- Tell me a situation when you are unhappy with that current status?
- What is your passion?

Coding - LRU

利口140变种，只要求输出任意一个结果


不算难的一道题，而且面后发现一个星期之前才做过，可当时就是没想起来，然后用利口139的方法去做，用dp array去记录word分隔的位置。因为用的方法比较麻烦，figure out offset等细节花时过长，导致没做完而且有bug。
原因：头两晚因要准备面试加上紧张，觉没睡好，结果到面试前还是不大清醒，记忆缺失。面试官不友好，全程不提示，而且一有停顿就问我在干什么或想什么，打乱我思维。.留学论坛-一亩-三分地
不过归根结底还是自己的问题，关键还是要自己强，解题熟练。像这样的题，应该能秒过，就算面试官不友善，他也不能把你怎么样吧
考前休息好很重要啊！希望能对大家有所帮助

Behavior问题是Amazon面试的重中之重，每轮面试都有一半的时间在回答behavior问题，一定要好好准备。回答这类问题采用 Situation, Task, Action, Result四步走的模板，也就是遇到了某种问题后(situation)，确定某种目标(Task)，自己是怎么去做的 (Action)，以及最终的结果是什么(Result)。重点在于Action，在于描述自己如何努力、怎么做的，最终结果是否理想并不重要。切记回答这种问题不能讲大话、讲套话、讲空话（比如说自己一般遇到这种问题会怎么怎么做），而是要讲一个具体的故事，最好不要编造，因为面试官会问很多follow up问题。

1st round: Given a 3D map of celestial bodies, find the closest 10 to earth. Assume earth is E(0, 0, 0).

2nd round: System design: Design a distributed JukeBox System

3rd round: LFU - Least Frequently Used Cache

4th round: all LP behavior questions.

5th round: 输入2维字符串数组 String[][]，每个数组String[]第一个String表示父母的名字，剩余的该人的子女的名字。every name is unique。 问题： Who has the most children? (Hash table); Follow up: who has the most grandchildren? (Hash table) Follow up, if the data is so huge, how to process. (MapReduce)[br]

一共五轮，每轮45分钟，没两轮之间没有break，但是你可以花上3minute左右喝点水和去卫生间. from: 1point3acres 
第一轮：（烙印）
hiring manager面试的，也是我以后mobile team的manager。没有coding。对着我的简历，一个项目一个项目的去问。 每个技术细节问的很深，比如细到这个请求网络的服务是用什么Framework类来实现了，这个Framework类比着别的Framework类有什么优点？  另外，他对我的一个多媒体播放的一个项目特别感兴趣。问了好到技术细节，以及其中的一个我们设计的很关键的算法。我给他这whiteboard上面画图详细的描述我们当初设计的这个算法。结果这个面试官一眼找出了我们设计的一个漏洞。我告诉他这个问题我至今还没有解决，他也没有继续追问下去。

第二轮：一个年轻的印度三哥。.留学论坛-一亩-三分地
以下内容需要积分高于 188 才可浏览
. 留学申请论坛-一亩三分地
这货上来也没有寒暄，也没有微笑，直接说题目。我当时也挺紧张的，感觉这货要挂我。
他的英语我也没有听的很懂。我反复给说他pardon 和Do you mean by ....? 无数次之后才弄明白他的题目意思。 他的题目的意思是：输入a list of sections, list<section>, 在每一个section中有很多product，每一个product有两个属性：user，relevancy ，你可以通过调用系统API得到这两个值。 每一个section有score所有的product的score之和，每一个product的score是user * relevancy 。 最后给这个list of section排序，使得score大的section在前面。 这个题目其实很简单，但是他前面描述这个问题花了很多时间。
第二题：设计一个 in memory cache system，支持 来源一亩.三分地论坛. 
1. capacity（这个system有一定的容量） 来源一亩.三分地论坛. 
2. TTL（time to live）. 围观我们@1point 3 acres
3. LRU (least recently unused)
参考leetcode https://leetcode.com/problems/lru-cache/
.本文原创自1point3acres论坛
follow ups:让你扩展到一个distributed in memory cache system怎么设计

. 1point3acres
第三轮：老美
继续问简历上面的一个项目，然后给了一个leetcode的原题https://leetcode.com/problems/surrounded-regions/。
由于问我简历，问的时间太久了，结果算法题目的时间就很短了，算法最后没有在whiteboard写完，但是思路给他们解释清楚了。
. Waral 博客有更多文章,
第四轮：老美
以下内容需要积分高于 133 才可浏览

第一题：给我展示了他们组做的一个APP: Myhabit,（可以在AppStore上面下载看看），面试官给我指着Myhabit上面的一些功能，让我去自己设计。在白板上写出自己的思路。


第二题目： linkedlist 每个节点多一个random pointer。leetcode原题。我用hashMap做出来的。. visit 1point3acres for more.

第五轮：（老美）
. visit 1point3acres for more.
第一题： 设计一个大楼的电梯（Amazon经典面试题目，面试前面我专门总结了一下^_^）. 围观我们@1point 3 acres
第二题：继续问简历上面的项目。. 围观我们@1point 3 acres
-google 1point3acres
总体感觉，对自己以前做过的简历上面的项目一定要熟悉。两道算法都是leetcode中等题目。回答问题时最好要以customer为中心。

第一轮面了多线程锁
第二轮面了排序阵列跟二叉查找树互相转换
第三轮要求设计机场跑道tracking system，保证每个飞机能顺利使用跑道升降
第四轮利扣第贰百，然后又出一题sorted pair array查找漏掉的element(用二叉搜索，力叩原题)
. 1point3acres
来源一亩.三分地论坛. 
今天聊完发现他们很喜欢问behavior questions，问了很多在不同情况下你要怎麽办的问题，hr说两天后回复
做的东西挺large scale的，个人觉得还不错，目前大量招人，有机会可以投了或请人内推试试看
由于之前受了不少地裡帮助，在此回报地裡，也请你们不吝啬给个米

就四轮，三轮coding一轮design，感觉应该划水过了
1. LC 59
2. LC 103
3. 设计一个亚马wishlist的数据结构， 就是吧product， host，guest和wishlist怎么混在一起，我选的用non sql来实现，讨论完了又聊了下用sql怎么设计schema，分享wishlist就发wishlist ID 到url里面，然后很简单的聊了一下如何提高performance和如何cache数据的问题，我就提了下用redis就行因为我也只用过redis。 然后大概估计了一下latency和throughput，然后讨论了一下db读写和如何隔离优化。讨论了一下cache的优先级选择，我就提了下LRU，用欢迎度和时间来决定cache优先级。就提了一下LRU是一个hashmap + linkedlist就不再问了，本来还想给他现场写一个LRU搞个妥帖的，结果不问了。主要就半小时，好像也没啥太多能问的。
4. LC 53

第一个答得不是特别好，思路写对了，code感觉有点bug，东岸过去第二天一早起来面试感觉不够high。。后面都是bug free应该没问题。亚麻好像没啥大包，等真有offer再看吧。


前几周面的亚麻昂赛，已经过了，给大家发发面经。因为是跳槽，所以面的特定的一个组。三轮算法一轮设计一轮Hiring Manager。每一轮都十几二十分钟的BQ，因为亚麻要考leadership principles，那些问题具体都不怎么记得了，反正大家每个principle都准备一个例子，可以是工作，也可以准备一个生活的例子，我有一两题就不是用工作的例子。不用太头疼，自圆其说，言之有理即可。

1. 利口以伞令。就DFS一下。
2. 利口以令。我一开始用DP解，写了方程，但面试官一直有疑惑。最后他让我写个递归的，没剩多少时间了，我也只能草草把几种情况的递归写出来，没有把整个题连base case一行一行写好，只是在写递归方程的时候写了base case怎样初始化。交流和沟通能力很重要
3. 午饭和店面我的人吃，就聊聊他的工作经历。店面的题细节记得不太清楚，大体上就是一个矩阵，每个点有一个海拔，只能从高到底走，问所有downhill paths。DFS ＋ backtrack。要path延伸到无法延伸了，才加到最终结果里。讨论为什么没有环。最后问了些scalability的东西，我和他讲怎么shard database，distribute load，replica去做fault tolerance和load balancing的问题。. 一亩-三分-地，独家发布
4. 利口期溜。双指针＋哈希表。之后问了利口伞令以（三种不同括号）。我说这个DFS／BFS，每个括号算它在或不在的情况，复杂度是2^N的。面试官问怎么优化。一开始没什么头绪，他问我括号匹配怎么做。我知道用stack。他说能不能用那个去优化。其实意思就是把能匹配的先匹配了，看到match剩的，再去做recursion。Asymptotic复杂度没变，剪了下枝。后面这题没写，只是谈思路，因为第一题我写好了还给他跑了两个例子。
5. HM就纯问BQ。
6. 设计问了聊天App，算经典题目了吧。

来源一亩.三分地论坛. 
总体而言题目中规中矩，不算难。BQ很多答得挺累的，但面试多了BS能力就上去了，其实对方也不太在意很多细节，人家工作了一天脑子也累，只要你一直有话说，不要尬聊，基本上没什么问题，表现得积极有热情就可以。


记录面经回馈本版。最大的感受就是亚麻印度人真心多啊，感觉都多到影响西雅图城市人口构成了。然后印度人参与面试真的非常积极，国人们一定要多当面试官这样才能跟在tech领域跟印度人抗衡啊。话不多说，上面经。

第一轮 小韩面试官加三姐shadow。小韩长得一般但是打扮有型在马工里不可多得，更可怕的是人超nice加上一口纯正美国西北口音英语，一开口就让我把持不住不再高冷。开始翻简历说我们原来前些年在同一个城市啊，我心中暗喜你这是在跟我套近乎嘛，我来者不拒问了他觉得那个城市跟西雅图比如何，简略回答发现他不是很想继续，就此作罢，直接上bq，接着技术题目是
以下内容需要积分高于 188 才可浏览
来源一亩.三分地论坛. 
kuaidi baoguo进guizi的问题，版上哪里见过但没做过也没见过答案所以start from scratch，以为是个设计题装模作样跟他交流沟通只为了多看他几眼，他一开始还一副欲拒还迎的姿态，后来被我问多了就说直接上。。。答案。网上不都说多交流互相了解比较重要吗，怎么这么不经撩，猴急。于是快速写出几个核心class，被小韩打断，进入coding阶段，实现怎么选择guizi。

当时有点跟不上节奏，一直以为是设计题，没想到这么快要换姿势。行，随你，谁叫你是面试官。期间讨论了下方案觉得没问题，迅速写出线性解法，然后说如果有成千上万个guizi，怎么优化，我心想我这辈子也没见过这么多guizi，但客人的要求总得满足不是，继续讨论优化，最后快结束让我又码了段简单的code。全程隐身的三姐这个时候突然冒出来一个很弱的问题，明显跟不上我们的节奏，小韩都不想解释，跟我说没事我懂你，出于礼貌我还是跟她解释了一下。随后我提问，我就问问在亚麻生活可好过的是否开心，不开心来找我呀，然后互留微信显然是不可能的，依依不舍目送离开。

第二轮 烙印hm。其实面试前两天收到schedule发现一半都是烙印就有种不祥的预感。再加上shadow两个你们都占绝大多数了，而且就接触的这几个都是在印度亚麻转到美国来的，于是我本着练手的心态来的现在更不愿意去了，否则我在美国摸爬滚打这么多年好不容易练6的纯正英语要被你们带得veli veli bad。全程bq，问的很细，直接说以前远的经历就不说了，就说近的吧，反正我记性不好要我说远的也说不出来。于是各种扯，问的问题都逃不过版上总结的那些，面试前一定要结合14条认真准备。至于扯的好不好就不知道了，反正他全程冷漠脸，我说的唾沫横飞地他却不苟言笑，好吧我黔驴技穷不伺候了，客官慢走，永远也别再来了。

第三轮 来个胖墩老美加上一张娃娃脸着实可爱，笑容可掬实在让人很想跟他做盆友。一开始他自我介绍说自己做的东西，我说我擦我还用过啊，这玩意儿真神奇，怎么做到的，我是真的很感兴趣啊，过了十分钟才会过来不是我面试他，于是我说客官你什么要求啊。于是又是老一套bq，伦家以为你会跟别人不一样，结果你们男人都一个样。回答完毕，上题。是一个系统题，
以下内容需要积分高于 155 才可浏览

大概意思就是说要在网页上显示ku cun信息，数据从好几个数据库里面抓，当然速度慢，但是，数据库不能动它因为还有别的系统依赖，怎么优化。装模作样问了些问题，

其实聪明如我早就识破你了，不就是要加缓存吗。各种讨论优化，非常会引导我，跟这样的面试官交流简直是一种享受。都是些开放性问题，答的有理有据就行，最后分析下trade off。问罢终于又轮到我面他，接着他的工作又提了些问题，相言甚欢，握手，目送离开。

然后是年轻三哥请吃午饭。一看就很稚嫩原来刚从印度搬来不久，说话略显腼腆，以我阅人无数的经历判断，是个还没有被发达的资本主义腐蚀的单纯心眼不坏的印度小男生，算了还是不撩了怕你看上我爱笑的眼睛。小哥还算热情，聊工作但其实面了三轮你们做的那些东西我真的不想再听第四遍，聊感情聊人生显然三观不合又聊不到一起，然后就聊了下亚麻在印度混的怎么样，他说不怎么样，我说在中国也是，没什么人用，谁不知道马爸爸，马爸爸还说要在美国开拓市场，你们怕了吗，哈哈哈哈。感觉一群老中面烙印的日子指日可待。期间他还透露说亚麻最近招人很猛，我问你们组几个head count啊，小伙子果真很实诚，好样的。然后说周五亚麻的感觉就像放假，周五中午都是组员一起出来吃饭，到四点办公室就没人了，好吧，怪不得街上空气中咖喱味更浓重了。吃完还说要带我去拿亚麻在街上免费派送的香蕉，哼，谁稀罕，别想用一根香蕉收买我。对了，他还说去年一年西雅图有260天在下雨。。。 


午饭归来第四轮接着面， 天竺小胖墩儿加天竺shadow。上来又是bq十几二十分钟吧，然后上题吧。利口 伞把而。 这道题闭着眼睛也能做出来啊，假装问了下问题，故意先说了o(n) time o(n) space的map做法，正在为自己演技洋洋得意的时候，他说要优化时间，我有点懵逼，o(n) 你还要我怎么优化？我假装思考状，然后说，想到个不要map的利口最优解法，你看行不，他说，先来吧。三个步骤每次循环一遍，他接着纠缠能不能优化时间，我想丫的利口最优解还怎么优化，他提醒说后面两个步骤合并在一个循环里面，就从三遍循环变成两个。原来你是这个意思！！一个内部有6步的循环，跟两个各3步的循环，有意思吗，你有意思吗？也许performance会有那么一点点区别，但是面试要吹毛求疵到这种程度，你不是来黑我鬼都不信。我怒怼说我三步走逻辑清晰可读性更高，他用他的大体位怼回来说如果链很长的话。。没等他说完，我表示你赢了，懒得跟你纠缠，合并就合并，多大的事，写完跑了一遍test case，改了一个地方，然后我说你要不要照下来免得你以后黑我。然后他问如果有环怎么办，这时他的shadow发现天竺小胖墩明显没听讲忙着打code，就跳出来说人家刚才跑的test case就有loop了。收官结束问问题，其实我一点问的欲望都没有了，但必须陪聊满一个小时啊，谁叫是你出钱定机票订房间把我飞过来的呢。天竺小胖墩全程冷漠脸，我也懒得跟他笑了，最受不了的就是他的摇头yes点头no，后悔当初没深入研究下印度人摇头108式的含义。shadow小哥倒是不错，有时候还跟我笑笑，有那么一点点互动。想想真是人之初性本善，刚入职的天竺人多么和蔼，越老练越不可一世，不像话，本来就是个相互选择，你不止我一个我也不止你一个，看不上眼move on到下一个，但是人与人之间最起码的友善与微笑都舍不得给一个。写到这里，脑海里又浮现出小韩的音容笑貌，恩还是他对我最好。
.1point3acres网

最后一轮 美国小哥，一碰面我虎躯一震，我去，跟史泰龙神似啊。来了个有力的握手，发现问题了，这小哥不会跟史泰龙一样面肌瘫了不会笑吧，表情真的很严肃啊。一上来就码code，这节奏我喜欢，别上来整那些虚的。利口 吧。 我虎躯再震，印象中是个medium的题，但是通过率史上最低啊，惊呼这道题很tricky啊，很多edge case，他说那你就列edge case吧，我就如此这般列了一堆，他猴急地不行，说得得得，够了，开始码吧，我说行，码的时候有case我再提。一气呵成，途中又发现个edge case询问处理方法，然后指出有两行code可以refactor一下你要不要我改，他说无所谓他知道我知道，让我解释了下逻辑，指出了一个小错误，面到这个点精疲力竭了谁没个马虎，但是的确是我错，赶紧改了。一来二去他实在找不到什么好问的了，他能想到的edge case我都列了，他突然对我一笑，说我们bq吧，把我吓了一跳，我还真以为你面瘫了。反正无外乎还是那些题那些事翻来覆去说来说去，有个故事说了四遍我真不想再提了。但是在交流中他透漏出，customer obsession是最重要的，原来如此，怪不得在14条中位列第一。小伙伴们bq答案一定要尽量往这点靠啊。聊完他一看手机，怎么还有这么多时间，于是不知从哪里有翻出来一道bq题，更加让我坚信他们家bq就那几道题库。聊完提问walk me out。

on site完接近一个礼拜都没回音。不敢去问怕来拒信。顺便发一下楼主收集到的在职社招on site的面经集合造福后人. 1point3acres

非technical的问题真的要好好准备。提前写一遍然后自己读读，不亚于刷题刷设计的重要性。

面经来源地里，感谢各位的贡献，如果有人觉得侵犯版权或者隐私的，请DM我我去删除。
括号里是具体帖子里比较重要一点思路或者重要的follow up question，楼主只是做一个微小的贡献
. 围观我们@1point 3 acres
System Design:
1. Design a Uber 设计一个简单的Uber，包括检测周围空闲的车，用户打车付账流程和到目的地时间估计.
(将城市化成许多个矩形block（区），可以借鉴二维k-d tree那个思想。每个车实时更新当前位置坐标和是否available，找用户最近八个区的空闲的车，然后时间就是车速和距离的关系，这个没错。地图api这种你需要什么和interviewr说就好了，如果不是考察项目的话一般都会说可以默认给出的。). visit 1point3acres for more.

2.TinyURL
(Write heavy? improve Security? 怎么scale? 一个region上的服务出问题了怎么处理?)
以下内容需要积分高于 188 才可浏览

3. Repository system, design commit fuction and branch function.
.留学论坛-一亩-三分地
4. Video/Movie System (given a list of videos, return top 5 rated videos)

5. Sotre the livestreaming video and watch it later function

6. cc150 JukeBox

7. Amazon gift card printing machine. (实就是general的说一下你对一个application architecture的理解，面试官会引导你，比如用啥样的db，用rest/soap，某一步失败了怎么办，data consistency一类的随便扯一扯)
.留学论坛-一亩-三分地
8. One hour delivery system

9. Explain Agile, Waterfall, Pro & Cons

10. Predict User purchase
(先分析什么因素判断用户买不买这个商品，浏览记录，购买记录，在页面停留时间，浏览这类商品的次数，现在火的top 100商品等等。然后分析架构，
给的答案是首先master slave避免single point failure，用户点击商品后先通过dymanic dns look up找到距离最近的CDN，然后http request传过来给那个cluster的master server, mater本身有cache看看这个请求的结果是不是已经cache过了有的话直接返回（这里cache的是这个请求对应的购物车html页面），没有的话master做负载均衡下传给空闲slave server（rmi call）, slave有自己的local cache因为对这个预测结果每个slave cache可以不consistent， 可以不用时刻recon每个不同的server cache。所有的数据存储都用in memory database并设置time to live， 因为这个是一个读取大于写的系统数据也不需要持久化不用支持transaction, scale也更容易。master如果挂了重启就可以，因为都是预测数据丢失了也无所谓。如果要更优化可以在浏览器端也做一层cache，如果用户反复点击同样的商品，就不用每次都make http call了)
. 牛人云集,一亩三分地
11. Card game , and write shuffle method

12. Amazon Locker 就是Amazon买东西可以运到一个Locker然后pick up的那个.
(仔细想一下你就会发现就是一个Parking Lot.Package有Small,Medium,Large.一个Location的 Lockers也有Small,Medium, Large。面试官主要想知道一个送货小哥去的时候怎么分配给他个大小合适的Locker。要写那个method。我就按照Parking Lot做的。我觉得一模一样。恩恩，我那时侯一开始考虑也想是不是Order生成的时候就匹配了一个Locker，还有挑选哪个Location,但跟面试观官交流以后，他就说假设只有一个Location然后主要想知道送货小哥去的时候怎么分配，别的先不考虑。)

13. Reader System

14. Parking Lot, Airport etc...(http://stackoverflow.com/questio ... n-an-oo-parking-lot )

15. Amazon address book
   (1. What's in web server
    2. What's the API for address service-google 1point3acres
    3. What's in the storage
    4. How to improve the performance)
(user 发送与address 相关的请求到web server，　然后web server 获取／更新相关的记录。大概说了下DNS根据user ip访问临近的web server, 问到了web server 里头有哪些与address 相关的function 以及参数，具体说了下getAddressLists. 期间提了下cache 面试官表情不对了。后边问了有多少个表，怎么设计，怎么提高profermance. 楼主提到说作no sql 做sharding。面试官说时间到了没有给反馈，多半是设计太狗血). 围观我们@1point 3 acres

16. Design system to store user info and address info. Address info changes frequently. Need to notify address change.

17. Design a Log application. (就是开发从上面获取 bug log 信息，用户可以往上提交。开始我并不知道log application怎么工作的，是程序员往上提bug 还是test人员往上提。跟面试官一步步讨论的，然后写了些前后端的 process。中间很多问题，他们会顺着你的思路往下问)
-google 1point3acres
18. 给了一堆 商品，每个有不同的分类tag 比如 book, music, sports... 然后按顺序输出，就是输出这里他描述的特别不清楚，于是开始先按tag sort了，然后顺着输出。他说不行，想要控制每行的个数，然后就控制个数输出。然后他比较满意，follow up 了随意更改每行的个数，不要求写代码，也写上去了

19. OOD。设计一个SQL parser（不是compiler，这里强调如何解析SQL语句中的变量，比如table name，和关键字， 比如select 语句），关键在于怎么用好interface

20. 设计一个big integer类。实现其中的add和multiply。先是讨论了要使用的数据结构（数组和链表）并对比优缺点，然后用数组实现（非高效压缩那种的，一个数组元素是大数里的一位数）。multiply只要写伪代码，出了错，不过他不介意

21. 设计个API，满足两个function，一个是往list里面丢string，还有一个是统计top k frequent element. 对于API实现scalability.

22.  Design pattern: strategy, observer   设计模式那个就是duck/toyduck的变形。Observer那个也是比较教科书的东西

23. 如果有一个service, 要求设计方法支持query，比如最后一秒的访问数，最后一分钟的访问数，。。。。最后一小时的访问数。。。
(1.把timestamp 写到磁盘上，然后用hadoop 来算。面试官问pros and cons. visit 1point3acres for more.
2. 为了改善读的速度，我说把这些timestamp存到in-memory buckets里面，最后还是 hadoop
根据我的buckets排序思路提示我，可以不用存timestamp。。。。我有点惊呆了，但是转念一想，你这些query的时间段是last second/minute/hour。我觉得就可以只有这三个buckets，每次call 这个service的同时，检查当前的timestamp，如果超过1秒，我说就去aggregate/update last minute和last hour的总数就好了。。。 到最后我脑子里有点捣浆糊了，但是面试官看到我最后的思路解释说可以work))


24. 手机公司的bill系统，手机计划有免费时段，比如晚7点到第二天早7点和周末免费。短信和数据有各自的价格，用超过计划允许的数量怎么办。最后完成的感觉还算不错。这一轮也问了oo的一些基础知识，比如inheritance 和 composition的区别，什么时候用哪种？




Algo: 亚麻很少出原题，但经常出变型，感觉挺灵活的。难度比较上属于中等和偏简单，偶尔有些hard属于经典题或者bar raiser吧。仅供大家参考。
. 一亩-三分-地，独家发布
1. Unique Path 变形（可以上下左右，可否回溯，不可return false且原地不动）
2. lc239  .留学论坛-一亩-三分地
3. Max Subtree Sum
4. Longest Substring without duplicate char
5. Find leftmost node of the lowest level
6. Two sum
以下内容需要积分高于 188 才可浏览

7. Merge qua-tree
color: black, white, misc
class Qua-tree
{
    Que-Tree[] children; //0 or 4 children-google 1point3acres
        int color;
        ....
}

Merge two tree, black is dominate color: black vs anything -> black;

8. 围棋判断一个子被capture与否，被capture的定义就是这子或这子属于的整块同色子区域被另外颜色子包围。 
   (解法也很简单， dfs。 每次recusive call返回是否被capture, 遇到异色子或者出界都是true, 遇到同色子就recursively去call它)
(那假设只有同色的子（没有对手的子），也算是被capture么？（这个点很好！！  可以当作edge case处理单独处理。）

9. Latgest rectangle area
10. Search word in Trie
11.Lowest LCA
12.Top k nearest point
13.给出的是一个目标文件名，自己提出假设定出file class 和 directory class，找出所有符合目标文件名的文件的path
14.job failure root search
(相当于一颗倒的树，root fail了，找导致这个failure的最高的ancestor。DFS, 顺着fail的path往上找)
15.多米诺骨牌，找出最少数量的能推倒所有牌的牌
(大概思路就是循环把入度为0的点当作起点dfs，把能traverse的点mark as visited，把起点加入result，然后如果还剩下没有visited的点，就说明有环，所以就再loop剩下点，每一个dfs，mark能traverse到的点as visited，把起点加入result，如果碰到了之前visited的起点，就把这个起点从result里面删掉，加入当前的起点。)
16. Shorest Path
17.Find heavier ball in ball array
18. Work Break.本文原创自1point3acres论坛
19.  Word Ladder II(原题是变一个字母，这里是去掉一个字母)
20. string to int.留学论坛-一亩-三分地
21. int to roman
22. There is list of price at each day，and only one selling window is allowed. The selling price  is the minimum price of start day and end day of that selling window, and price is flat during the selling window. The selling amount is constant per day. Find out the selling window gives maximum profit, output max profit.
23. Graph. graph. 实现画板的brush功能： 一个画板上面已经有一些图案，用户在画板上点任意一点，画板会自动paint包含该点的封闭的多边形。实现这个功能
24.Merge Interval
25. Matrix原题
26. 有一个Task clas包括两个int, start and end; 有个list有很多个Task, 计算需要多少Thread 来run这些task.
27. Serialize and Deserialized Binary Tree  . visit 1point3acres for more.
（中间穿插了多线程的问题，以及 abstract class 等知识。
Follow up :
    1. What if the TreeNode class value is string (instead of int) which may     including newline, space, comma
. 留学申请论坛-一亩三分地
    2. 如果不是二叉树，是多叉树怎么办？
正确的方法是在序列化的时候 存孩子的数目，存数据的长度，再存数据。需要一个结构化的序列化操作。.本文原创自1point3acres论坛
new line, space 这些只是给你增加难度，你可以把数据当成binary来存; 我的想法是可以存字符串的ASCII码或者UNICODE编码，然后用space或者newline隔开存到文件里
）
28. 一个matrix，里面有一些锁（1表示）和空白（0表示），问每个空白到最近的锁的距离。简单bfs. from: 1point3acres 
29. 算法+search suggestion设计，算法：给个word，给个dict判断给定的word是不是anagram. 围观我们@1point 3 acres
30. numbers of islands 
（ follow up：有多少个形状不同的岛？
这个Follow up是经典 number of distinct islands
比之前的明显要难些。 需要用到hashing得思想。 
每一个岛将遍历完的点id(每个cell 可以分配一个id, id = i*m+j) 组合起来， 返回字符串，比如 “1/2/3/5”  这个岛有四个点。如果另一个岛是 "11/12/13/15"  只要把它offset下， 第一位归1， 它也变成"1/2/3/5"， 所以这2个岛的shape是一样的。 将这些第一位归1的字符串往set里丢。自然就除重了.留学论坛-一亩-三分地
中心思想： 将CELL ID组合来表示一个岛(hash to string)，然后变形string, 最后往set里丢。 done
. 留学申请论坛-一亩三分地
）
31. kth largest number in array，quick selection
32. LRU cache. 留学申请论坛-一亩三分地
33. Number to English words
34. Valid Parenthesis
35. given n pairs of numbers (1122...nn) and arrange them so that the each number x is x spaces apart from another number x. 
(数字必须紧挨着，思路就是DFS)
36. Given a dictionary of words and a word, return the word if it exists in dict, else return the top 5 words in the dict that are closest to the given word;
37. 2D array is immutable. Give 2D array of 1s and 0s, 1 is island and 0 is sea. Return the maximum island size
38. 给了一棵树，让给每个node 加一个pointer 指向sibling.
(用了queue level order traverse 加了。然后follow up 让优化，no extra space) 来源一亩.三分地论坛. 
39. Reconstuct itinerary
40. 一个non-negative integer array里找subarray sum。. 留学申请论坛-一亩三分地
(followup: 数字可以为负)
41. 有一堆时间连续的purchase records (id, timestamp, userId, productId)，找出最常被同一个用户连续购买的三个商品
42. 找出数组中唯一出现奇数次的数字，保证只有一个，(hashset解决)
43. reverse linkedlist
44. kindle界面是黑白的，黑色区域是一个shape，然后输入一个界面且可修改，返回shape的个数。
(这里我用了二维数组作为输入，0是空白，1是用pixel。然后dfs即可。 其实就是Number of island.)
45. Intersection of two linked list
46. Group anagrams.留学论坛-一亩-三分地
47. Convert binary tree to double linked list.  In-order order
48. 写一个class要求push/pop和get minimum都是O(1)
49. 给一个数组的object，用里面的key来sort，keys 只有有限的几个 . 1point 3acres 论坛
(这个题我先用的priority queue，让我继续优化，我用了bucket sort，到O(n), 让我继续优化用in-place，我用了两个pointer;
我最后用2个pointer排序的，但是一个while loop 下面嵌套了四个sub while loop。比如，这些objects的key 只有 X, Y, Z. 排序的要求是把这三组按照XYZ的顺序排好。

前两个sub while loop 对调X 和 Y或Z; 这轮结束后，X的位置应该都是在正确的位置上了. more info on 1point3acres
后两个 sub while loop 对调 Y 和 Z。). 牛人云集,一亩三分地

50. wiggle sort 2 
(给一个数组，里面有负数和正数，让输出负数／正数间隔的数组，我用了两个pointer从头到尾／从尾到头同时扫一遍。估计这题没法做成in-place，最后没时间写完code，只是大概说了一下，最后面试官觉得可以work)

. more info on 1point3acres
51. find # of distinct islands in 0-1 matrix.


补充内容 (2017-6-7 02:29):. from: 1point3acres 
Update一下吧：Recruiter让面Senior妥妥地跪了。吃一堑长一智，这几个月都在刷题，感觉easy/mid都没问题了。9月底解冻顺求Amazon的朋友到时候能不能给个SDE1/2内推？

补充内容 (2017-6-28 12:13):. visit 1point3acres for more.
BQ: 发不全，简洁点
Why work for us
Build relationship with co-worker
Disagree with Group decision
Why hire you
Disagree with boss.留学论坛-一亩-三分地
Can't meet deadline
Could done better
Significant improvmenet ever

和大家分享一个去年在A面试的经历。

面的是广告组，在PaloAlto office。Building后边貌似就是火车站。和面试官闲聊了解到这个Office比较偏研究一些算法之类的，比西雅图清闲一些。
楼里没有食堂，中午manager带着在附近餐馆找饭吃。manager也是才到这一个月。 总体感觉team比较中规中矩， 和一般startup比team没有那么年轻话。 有些大公司的感觉。

第一轮，白人大叔。关于多线程的。 如何调用一个function，如果在规定时间没有完成计算就直接返回。比如 function(200)， 200代表这个function最多跑的时间如果没有在200毫秒完成久停止计算直接返回

第二轮， 印度大哥。找一个lis里边第二大的数。这个用quickselect做。followupshi问如何处理tie的情况。最后问了一下现在公司的project。

第三轮， 印度大哥likou要司令。用的是dp的方法。第二题是合并两个平衡而茶树。先说了nlogm的方法，再说m+n德方法。最后问如何减少空间 复杂度。

第四轮， 设计搜索引擎，设计customer also viewed 产品的功能。

有一个教训是第三轮和面试官讨论的时候，感觉他对dp接发不是很理解。当时我表现的有些没耐心。后有些后悔，面试不论碰到什么面试官都应该耐心讲解沟通，这也是沟通能力的体现。

今年投A家跟去年不太一样，首先，OA题目换了（还来两轮OA，一轮phone screen），然后同时有两个不同组约面试，之前7月有发一个组的面经。
本次昂赛一共6轮，基本每轮都有BQ就不展开说了：

1. 立德扣200原题，做法很多，本人用了union find，应该是最优解了。

2. 立德扣48，in-place rotation，这种都是熟练到烂的的题目，简单到以为幻觉。

3. system design，设计一个股票查询系统，要求能查询当天的价格信息，一切过去任何一个时间段的价格信息，要scale，大家自己想想解法就好了，不展开。

4. lunch

5. 纯BQ

6. 立德扣238，题简单解法就不说了，主要是面试官会问你testcases，稍微注意下，以及返回的error output是否make sense什么的。

贡献一个亚麻纽约广告组onsite面经， 总共4轮1. 主要考察面向对象设计，设计一个电梯系统
2. 首先问了为啥amazon，然后问如何设计一个分布式系统
3. HM面，各种behavior
4. 两道算法题， 求二叉搜索树的第K大元素， MergeKSortedList. 1

给定一个大数据量未排序数组和int k
这个数组满足这样的条件: 
排序过之后数组和原数组比较，每个位置的移动范围小于k
写出排序算法

我想到的思路是，类似冒泡排序，但是只需要做k轮冒泡。
挂了

没明白面试官的思路，他想要考察什么。大家有好的想法么？

解题思路是：

使用一个大小为K的最小堆，开始将前K个建一个最小堆，然后将最小的取出，然后将第K+1个元素添加到最小堆，然后取第二个最小，然后将第K+2个放入最小堆，...

如此可以使用O(N*log(K))的时间可以排序。

证明为什么可以使用最小堆来做：

1. 首先可以证明最小的一个一定出现在前K个元素中，否则排序之后最小的元素和原来的位置相差一定超过K。

2. 利用1的性质可以知道第二小的元素一定出现在去掉最小元素后的堆和K+1的元素集合中，而不可能出现在第K+2及其以后的元素中

好像是那个geeksforgeeks上的那个k sorted array排序， 题目是意思是input的数组本身就满足排序之后每个数都移动不超过k这个性质, 不是说让找到一个算法满足这个性质 所以只需要维护K大小的heap，时间是NlogK

http://www.geeksforgeeks.org/nearly-sorted-algorithm/

1. 全程行为问题
2. 大半程行为问题 + 从日志中找出频率最高的路径(长度为3的路径)，例如：
jack, /home
lucy, /home
jack, /product
jack, /search
lucy, /product. visit 1point3acres for more.
lucy, /profile
jack, /catatory. 留学申请论坛-一亩三分地
mary, /home. 牛人云集,一亩三分地
jack, /product
jack, /search

/home/product/search -> jack, lucy; /home/product/profile->lucy; /product/search/catatory-> jack;
返回/home/product/searc
3. 全程行为问题
4. 半程行为问题，系统设计监测系统
5. 大半程行为问题 + 将字符串中空格替换成%20

感觉应该是系统设计跪了，和面试官思路有些不同吧。我感觉我这次面试行为问题也太多了，大家好好准备行为问题。

1. 国人面试官 很nice 问了一道利口三二二 + BQ
2. 白人PE 问了差不多的一道利口三二二BFS 我跟他说第一轮问了 他说没事儿 然后问complexity + BQ BQ问得很细 有点push
3. 三哥 + ABC 影子 问了类似岛屿问题 DFS很简单 很快做完 影子接着问了一道比较简单的sort 然后iterate的问题 具体不记得了 + BQ.1point3acres网
4. 跟三哥小哥吃饭
5. 国女 odd 停车场 + BQ 感觉打得不是很好
6. 白人hiring manager 全是 BQ

三天后hr约电话告诉过了

西雅图的on site, 面后一周通知挂了..
5轮全阿三:


1.HM: 全BQ: 怎样跪舔customer, conflict(我赢/别人赢), 没做好的事/教


2.OOD 交通灯,


3.lunc


4. 4sum


5. binary tree level order traversal,
binary tree max
level
sum


6. find k largest nu; design data structure

来我们划下重点，今年 onsite video 只考OA2，随意穿，分三组，ABC每组三十人，HR把你领进门，记得带ID，记得带协议，楼下十点见，只有半小时。 讲题，讲思路，讲improvement，讲复杂度。

在地里有一段时间了，学习了很多地里的同学都经验交流，虽然是挂了，不过还是再这里分享一下我的面试经验，反馈地里。处于保护，我不会分享具体的题目（4道题也就一道士leetcode上的而已，其它的基本上是面试官根据自己的兴趣，自己编的:).

1.关于算法及LeetCode上的公司Tag
很遗憾，一个都没有
我面试中用到了 Trie 和 DFS
还有，平时我们做LeetCode的题目，除了输入null的判断外，我基本上不考虑其它数据的有效性（比如说除0的话，要不要捕获异常，数据应该是数字字符，但传进来是其它怎么办）。但面试官等我写完算法后，就是抓住这些平时没注意到的细节。
另外，大家还是要注重对各种算法的掌握而不是光做题。我自己就是在面试的时候，发现自己原来还没有完全掌握我自己认为会的东西。
还有，没有问到时间空间复杂度。 也有可能希望我自己主动去说出来。

2.关于系统设计
出了一个从来没见过的设计，而且我准备的数据库，缓存，LB基本上所有的东西面试官都不在乎，甚至直接告诉我内存足够大。

4. 关于BQ
超多，有70%的时间就是问这样那样的场景问题，用STAR 方法可以梳理思路。14条Leadship Principle, 一定要牢记而且准备好各种各样的例子。特别是你解决了什么问题这类，大家最好准备一些高大上的（比如说处理完后，性能提高了。。。）

5. 关于冷冻期
明确告诉我欢迎12个月后再投

6. 关于我的面试准备
虽然这次失败了，但我觉得自己还是有收获。感觉这个公司不再像以前那样，觉得自己要不可及－ 感觉跟面试官的交流还是很顺畅，就像平时工作一样。至于为什么面试失败，一个可能就是自己准备还没到位（毕竟时间比较仓促），另外也可能是其他的候选人更加优秀吧（希望不是我阿Q）。Anyway.

另外，我在后期也按各种题型（比如Tries, Slinding Windows, Union Find, DFS, BFS），练习完感觉自对网上玄乎的问题都没那么怯了。
系统设计的话，我主要是用 “Grokking the System Design Interview”复习的，基本上很多问题大概都会有思路，而不是像准备之前那样，一下子不知所措。感觉很多时候，面试也有运气的成分在里面

7. 下一步怎么办
今天收到邮件后，心情很是沮丧，但是，总归还是要继续努力。下一步，一个还是要继续做题（准备先把微软的TAG题目做完先）。另外，争取做到看到题目，就能想起具体的代码，及注意事项；对于系统设计，继续消化“Grokking the System Design Interview”同时也在网上多找找其它解决方案以便更好的面对面试官的其它角度的提问。

8. 感谢
地里的战拖给我很大的动力去练习题目，另外，淘专辑里面很多特辑，也帮我减少了很多时间。同时也感谢战友们的分享。祝愿我们都可以有一天心想事成！

面了四轮
第一轮：两个印度gg，设计uber，不是很友好，估计这轮不好
第二轮：米国gg，给出一些pair，是categories里的父子关系，让建立树，然后打印出来
第三轮：设计一个schedule系统类似outlook的calendar，可以帮助team来schedule meeting room
第四轮：设计停车场，是个越南gg

感觉设计题很多，不知是不是因为有了几年工作经验，分享面经，求大米，谢谢

1. compress一个string，举个例子是"aaaabbcaddd" => "4a2bca3d"
2. system design 设计一个git系统

1. 给定一个set，你可以往里加新的key，要求你实现一个iterator，特点是如果你已经开始遍历，之后加入的新的key都不会被return。比方说set原先有1，2，3，你开始遍历这个set，此时你往set里加入4，确保4不会被遍历到。
2. verify balanced tree

Behavior：
1. 你和你的组员发生冲突，你怎么处理？
2. 工作中有没有过遇到一个复杂的问题，然后自己用了一个特别简单的办法就解决了的例子？

哎，跪就跪在coding方面，过去两年工作太安逸，刷不动题，一共4轮，3轮的coding基本都不理想，还有1轮OOD被自己气死
第一轮： 老美，巨硬跳到亚麻的，一半bq， 剩下时间问了一个 find a number in a sorted 2d array 
第二轮： 烙印带个小白shadow，mmp，一上来啥都没问，直接coding， hard copy LinkedList with random pointers, 当时没解出来，现在想想自己真是蠢，明明就是easy 的题目
第三轮：两老黑，考OOD，
第四轮： 老美，女，一半bq，一半coding

4轮一口气面完，人都瘫了，累死了，

第一次发帖，工作一年，前年接触react之后然后想做前端，没什么plain js经验，内推了Amazon Studio前端Santa Monica office，很快收到电面，上周四面的，1个小时，没考算法，问了很多前端general questions，有些问题记不得了。interviewer是白人，他自己介绍是team lead。
开始introduction，然后扯了一点behavior questions，最近的projects，以后想研究的技术什么的。

1. introduce js closure，记得不太清楚了，怕说错，直接说不知道。
2. css specificity，没接触过这个词，问他什么意思，他解释了一下，然后我介绍了一下css selectors，inline style > id> class 和 node，工作中没怎么用过node所以不敢确定class和node谁优先级高，没有正式看过前端书很多术语感觉说的不对。
3. 还问了几个小问题，貌似都答出来了，不太记得了。
4. 剩25分钟，写代码：实现amazon的star评分的UI，5个star，要求点击某一个star的时候，前几个star和这个star都改变颜色，用过amazon应该都见过这个，比如点击第三个star，前三个star都变色。蛋疼的事他prefer plain js和plain css，特马这个年代谁还写plain js和css，直接说不会，可以用react吗，他说行，但是又说了prefer plain。到这里我就觉得自己差不多挂了，毕竟closure和css specificity感觉是必须知道的，所以也不管那么多了，强行用了react。感觉写的没什么问题，也注意了代码分离。
follow up是hover的时候也实现点击一样的效果，但是在处理style的时候他要求用css控制前几个star的style不能用js。
大概知道要用类似
star:n-th-node()
之类的pseudo函数，但是不知道具体该怎么写，所以说不知道。
然后让我问几个问题结束。

之前完全没想到会纯考前端，所以完全没准备到这些。。。第一次发帖，感觉新人不易，所以不设置限制了。

付个amazon alexa的面经

- 1. Number of Islands. 先用dfs流畅的写出来，剩余的时间还挺多，面试官就让我用bfs又写了一遍。再看看时间还有富余，面试官就又问了我两种的优劣，时间复杂度空间复杂度。behavior: 举一个例子证明你dive deep to find root cause of a problem
- 2. binary tree, 求有没有哪一层的所有叶子和加起来为Target。behavior: 讲一个你得到bad review的经历
- 3. design locker。 behavior: 有没有哪次你是用了一个很简单的方法解决了一个看起来很复杂的问题
- 4. 设计一个data structure来模拟file system. behavior: 不记得了

隔天收到拒信。说真的不知道为什么，每一轮都答得很好，每一轮的题都很快做出来而且回答出了所有follow up。behavior也答得很到位。不明白为什么给拒信。

顺便附加一个twitter的面经
- 1. Flatten nested list
- 2. log file, file 中的内容格式是：
“
[2017-01-01 9:0:0] I ate breakfast
[2017-01-02 0:0:1] This is a sunny day,
I took flight to Seattle.
...
[2017-12-09 0:0:9] Damn I want to take days off
”
要求写一个search(startdate, enddate)返回所有在给定时间内的log
file 很大有50G
- 3. Design Twitter
隔天收到拒信，信里Recruiters让我二月份再去面一下其他组。。。不知道是客气还是啥意思，因为我面试的时候说我四月份才能过去工作，而Twitter那边可能急着要人？？？

说实话收到这么多拒信挺不爽的，最重要的是我题都做出来了呀。

求加米求安慰。。

第一轮 烙印
bq + print BST zigzag 原题leetcode上有， 然后follow up 是如果不能用int level来track怎么半


第二轮 烙印+shadow
给一个字母然后dictionary， 比如 "amazon"， dict {a-> @, o -> 0} 
然后打出 {@mazon, am@zon, amaz0n, @m@z0n...........} 典型back tracking


第三轮 烙印
有3个无限但是sorted stream， 要求在任意时间内可以query他们3个目前的数字的mean。 

第一轮电面是利口三一，然后问了些hashmap的基础知识，然后又问了2的N次方的bit表达式
然后不到两天hr就来了电话约onsite
onsite:
第一轮：白人大叔，先来BQ，问了差不多20分钟，开始写代码，停车场OOD
第二轮：白人大哥，还是20分钟BQ，然后问些数据结构，接着是写题，分别是利口一二五和四零九
中午吃饭尬聊
第三轮：白人大叔，没有BQ，问了快半小时的virtual memory, 然后又问了些别的系统方面的知识，楼主表示知道的不多，然后大叔就说他没什么问题了，让楼主问他问题。。
第四轮：老印，全程BQ，揪着简历上一个project问的特别特别细
第五轮：白人妹子，20分钟BQ，然后设计一个餐馆的resevation machine。
一周之后接到hr电话，和我说被推给别的组了，要再加一轮电面
接着这周一电面，大叔问了30分钟BQ，然后我问他没有code问题么，大叔说本来准备了现在觉得没必要问了。。。
然后一个小时之后接到电话说是给offer
感觉问的并不是很难，可能因为楼主是个妹子，长得也不丑，面试官全程笑呵呵一点也不难为我。
有问题的话欢迎大家留言，最后祝大家offer多多身体健康。

9月末接到OA邀请， 24小时内做完OA1&2，等了三四天收到白板onsite。
第一轮，墨西哥小哥，人不错，BQ问了如何坚持自己的目标或兴趣？code问了用stack实现queue；
第二轮， 美国小姐， 貌似是个manager，BQ问了怎么reaction fast， code题：让我design一个DVD租赁，各种开放，写完以后也没有问太多细节，人nice；
第三轮，拉丁裔的大哥，面无表情加些许口音，BQ问了我经历中的一个项目，问的很细，可能因为我转专业，他问的是我一个ME的项目，code题是让我deseries a tree，输入是一串字符，给了每个node的Id，和他的parent id 和他的displayname，要求输出root。一开始我以为相当于一个链表，顺藤摸瓜上去就行。但后来问了半天才发现是一棵树，每个parent可以有很多children。等我回过神来，已经没时间了，我就说了个BFS，他就打断了我，问我怎么实现啥的，code基本没写。
后来也就是大面积电话拒，原因大家也知道。

前几天的面的马鬃昂赛，今天收到HR的口头offer。找工作时受到地理诸多帮助，发一波面筋回馈下地理～
5轮
1. BQ
2. BQ + 电梯
3. BQ + 一道算法题，输入一个String检查语法。三个要1.每句话首字母大写。2. 每句话必须以 . ? !结尾。3. 每个单词都要valid。第三点可以直街call他提供的API isWord()来检查.
4. BQ + 两道题。 1. 返回一个树的叶子的所有的祖父节点. 2. 给一串单词，返回所有的公共字母。就是所有单词里都包含了这个字母。
5. BQ + 一道题，给一个list，里面是【parent，child】，根据这个建立一个多叉树。返回根节点。

总结一下就是算法题都不难，BQ巨多而且很重要，很重要，很重要！大家多准备一点例子，我就是例子准备的不多，所有有的例子说了两三遍，当时觉得有点尴尬。OOD电梯仍然很经典。

下面是我之前在地理找到的一些面筋的汇总。希望可以帮到大家～

on-site 印象中被問到了
number of island
tree level traversal 
一題 不是原題 有點忘了

這次亞麻on site 面經很沒有用 而且難度很不一 有些特難
很多人都遇到 非amazon tag的題 
遇到LC還好 
遇到非LC, (e.g. AVL tree, red-black tree, ... 其他神奇的data structure) 真的崩潰
還有人遇到OOD 停車場 等等的
on-site 我估計大概 有1000中國人拿到 但真正拿offer 聽到的不到5個....

第一轮一个中国小哥：
bq 时间紧的时候怎么处理的。
在大亚麻程序的运行可能有要求。
比如说：
A
B C
D E F
运行A需要加载B，运行B需要加载D和E。编写程序返回运行A所需要加载的包。
图
public List<String> findAllPrerequisite(Map<String, List<String>>, String target)
Queue<String> queue = new Queue<>();
BFS…
问了时间复杂度，follow up 如果运行A需要运行E，运行E也需要运行A怎么办。图有环。
第二轮白人manager
bq 谈一下你take extra responsibility的时候。
第一题是：
给定API
boolean isOpen()
void openLog()
void closeLog()
boolean hasNext()
boolean readNext()
让编写程序返回两个log中相同的entry。
第二题是：
User1
User2 User3
User4 User5
每个User都有自己的朋友，每个User都会推荐一个书单。List<Book>
返回指定一个user关系网中所有人推荐的书。
follow up 如果限制好友关系只能到第二层怎么办？ 查下层数呗。
第三轮犹太人：

故事背景是每个人都有一个浏览记录。List<Page>，让实现几个函数。
boolean exist(Page page) 返回某人是否看了某个页面。
List<Page> nextFewPages(Page page, int number) 返回某人看了某个界面之后的几个界面。
void remove(Page page) 删除浏览记录中的某个界面。

全部要求时间O(1)

这周亚麻onsite结束，一共四轮。。面筋真的没什么可以当数据的地方。。
系统题：自动售货机
OOD：设计一个游戏，任务可以上下左右动
另外都在聊天。
感觉OOD聊的有点崩

但是这几天做BQ真的把自己做傻了。

楼主每次Onsite之前的晚上基本上都睡不着。。最多5小时。。这种状态到onsite最后一轮简直要命啊。。不知道大家有没有神马解决办法。。


两轮国人大腿（全程中文），中间穿插一轮不知道哪里口音

1. Most challenging project
LC 236

2. Experience: project approaching to deadline
LC 74 follow up: LC 23 -> flatten 2d array to 1d array

3. Experience: project approaching to deadline
Experience: adding more features in addition to basic ones
LC 120

1. 树的镜像+各种follow up
2. 类似combination sum
3. 二叉树每一列垂直求和
bq大概就是proj，ddl，遇到的技术难题
其实题目都不难的，只怪自己太蠢，第三题懵逼了不会做，提示了一下才写出来。哦对第三轮最后还问了个完全不相关的min stack。
还有，我去了之后觉得亚麻挺好的呀，不知为啥从来没有听到过他家的正面评价。我觉得有必要传播一点积极正面的东西~别没事就怪人公司找人政策奇怪，你咋不怪自己运气不好实力不佳呢！找工作本来就很看缘分的嘛。真的，公司挺好的，是我自己不够好！毕竟第一次昂塞，积累宝贵的经验，感激亚麻给了面试机会！


第一次用chime还以为要视频，结果就是语音
白人小哥，一上来打完招呼就做题，完全没问bq简历
1. 输入一个int和一个i，返回第i个LSB
2. 里扣 伞思久 + unit test
3. 判断两个string是不是anagram.... follow up如果字符不止256个怎么办（LZ就简单粗暴地sort了， 还问了时间复杂度
4. 设计车库。这个lz完全没准备...想到啥说啥，不过好像这种设计题回答不出来也影响不大，因为据说有小伙伴直接说不会也拿了offer = =

1. 针对Python选手：如果你对C++和Java也熟悉，不要用Python！不要用Python！不要用Python！重要事情说三遍！这个project的skeleton code很明显是业余python选手用Java翻译过来的，很多设计会在python里出现奇怪的bug。别人帖子也提过。为了规避风险，还是换语言吧。实现方法都一样。
2. 在场会有几位Proctor，他们会帮你解决问题。但是不要抱太高期望。他们自己可能连project都还没看过。我是第一轮面试第一个时间，面我的是三哥。我拿code过去的时候三哥一脸迷茫，结果跟他解释了半天才发现他不知道milestone1是做什么的。。。耐心讲了一下milestone1题目他才懂我的code，说good，very good，go ahead。。。三十分钟就过去了。。。顺便提一下，他也不会Python。。。
后面用python不断出现bug，问proctor 1，2，3，4，5， 他们就说一句："I'm not familiar with Python..." 。研究半天，然后只是跟你说"If this doesn't work, do something else that works"...我只想说谢谢啊。。。到最后时间就这样都耽误掉了。。。还是那条建议：不要用Python！如果你已经网上选了用python，立即联系HR改。面试当天好像是不能改

3. 早餐要吃好。中午你coding的时候是没有时间吃的。比如我这个一直在debug修skeleton code的。。。

随缘了。忙别的去了。祝大家好运。生命苦短，我用python。

电面:
友好国人大哥: 就把 和 而伞斯

onsite:
video形式四轮
白人大妈： 留领吴， 斯而
三哥：BQ磨蹭了20多分钟, 思思
白人manager，纯BQ
友好国人大哥: hashmap, 以留领

每轮大概45min

07.31 网上海投了amazon,因为已经有了脸家的return offer,所以直接申请跳过了OA电面，从onsite开始。HR光速安排在Palo Alto面试，面试职位是SDE II.

除去午饭，一共五轮面试:
1.第一轮是三哥面试，很nice的三哥，一半时间BQ，一半时间coding. 面试题目是利口伞妖四，follow up是，如果是n-array tree怎么处理
2.第二轮是国人大哥面试，也很nice，一半时间BQ，一半时间coding. 面试题目是给一颗binary tree, 每个节点要么黑色要么白色，给定起点u和终点v,找出从u到v路径上最后一个白色节点，本质上是利口耳伞刘
3.第三轮是HM面试，全部是BQ
4.第四轮是三哥面试，一半时间BQ，一半时间coding. 面试题目是给定一个graph，以及图上两个节点，判定这两个节点是否是连接的，自己定义数据结构，输入输出。要求用bfs和union-find各自实现一遍
5.第五轮是国人小姐姐，一半时间BQ，一半时间system design. 要求设计一个用户在线提交machine learning 代码和数据，server自动帮用户训练model，并部署model在线做inference的系统。被全程教做人。

比如如果一直有小的order进来，大的order永远不会被process（我之前给的是greedy的思路）。
还有如果有大量的order，怎样提高效率，这题我一开始答的distributed processing，明显不是面试官想要的答案，最后也没想出什么好的方法面试官跟我说it's ok 这个是above and beyond question。

1. BQ 老印manager 事无俱细的把过去的事情问了个遍，最重要的是每个人的问题都特别要求举例子，我一直还真想不出那么多例子来。。。
2. 码 小白remote Seattle, 还是上来先问了半个小时的BQ，然后就是 刷题网尔散酒，这个题我没有太记得最优解，在用heap的时候卡住了，没写完。。。
3. 设计 小印 是的，又是BQ，然后设计T家的系统，问到了如何解决latency问题，我卡住了。。。显然推拉组合还不能让他满意。。。大神可以解决一下吗？
4. 午饭 小白 没有BQ了，它家在湾区没有免费饭，但是cafe有日料还不错.本文原创自1point3acres论坛
5. 码 小印女 跑不掉的BQ，然后刷题网 尔酒气，秒了之后 跟进了 死尔爸 ，她自己应该也不太会，我给她讲了思路，没有写码
6. 码 老印田 你猜有没有BQ？ 然后刷题网 气腰留 ，没有给用双向链表的最优解，是真的累了，而且都是老小印，真的没什么兴趣。。。

no chinese inputmethod so I am typing pinyinganggang wancheng le yama de onsite.  wuluan mianshi, meilun yixiaoshi. dajia haohao zhunbe BQ, shuode wokouganshezao.  taiduole !
round1: BQ + zhaochu lianxu santian nei meitian doudenglu de yonghu id. input is log list. out put is custermer id list. 
round2: BQ + zhaodao magic number,   shuzi i zai di i ge weizhi.  erfen chazhao solution . from: 1point3acres 
round3: BQ + xitong sheji. shejige jiaotong xitong. zaixian cha gongjiaoche or ditie de schedule. 
round4: quanchong BQ
round5: BQ +  leetcode 341, wo dangshi naocan meiyou quan fangjin zhanli , ershi ba qiandao de list fangdao le deque, daozhi daima liang biancheng. mengkui si. zhelun zuode buhao , 
qitai chuqiji ba. shangdi baoyou wo. 

OA：就是地里的高频题目，一模一样的

onsite 是6月底去Seattle的Alexa的hiring event，但是职位是湾区的，也不知道为什么要去Seattle Onsite。。。。

onsite 一共4轮，算法都普遍简单，感觉还是要用时间去准备leadership principels BQ，感觉 A家真是对问BQ 走火入魔了。。。
(1) 算法：蠡口 流逝而 变型。大概意思是有1个筛子，上面是1-6，扔一次得到的数字就是你可以往前走的步数。然后matrix有一些点比较特殊，有可能1个点和另一个点是联通的。比如A点和B点联通，你停到A点的时候，相当于可以自动“移动”到B点，下次从B点开始走。问最少丢几次筛子，可以从起点走到终点。(感觉这个题目有点小众，没什么参考价值。。。)
(2) bar raiser, 算法 + 设计：设计 Amazon Locker，主要需要写code 设计的部分就是怎么找到最合适放某个package的那个locker。
(3) HM, System design: Amazon 主页你搜索一个东西的时候，会出来 most viewed related items，设计这个功能怎么实现。
(4) OOD：design Cache

运气好，遇见的题目不难，但是我感觉每一轮差不多一半的时间在问BQ，题目根本就没有太多时间聊。A家招聘确实有点玄。。。

第一轮，印度HM， 语气比较冷，BQ之后问了系统设计：设计一个订票系统。
第二轮， 白人HM, 人热情也nice， 问了几个数学相关的Coding题，还记得里扣而令四，一点点变化，要打印出来。
第三轮，拉丁engineer， 开始比较冷后来还好，问了里扣而散，和里扣斯.1point3acres网
第四轮，印度HM， 人挺好，BQ之后问了里扣斯令九


这次没有问OOD，系统设计题有点新，感觉很难答。

昨天让朋友帮忙查了下状态，仍然是available, 但是负责我的recruiter换了一个，换成了面试中其中一个组的recruiter。.留学论坛-一亩-三分地
想请教一些各位这种变化算是好还是坏。

多谢多谢，祝各位好运。

上周五刚面了亚马逊fulfilment后端工程师level 5（亚麻最坑爹的就是我被内推的岗位知道面试当天才知道是level5的，提前也不会给你JD）。第三次从波士顿飞到西雅图接受6轮面试被虐。。。这次为了攒人品分享一下面经：第一轮设计一个load balancer。给你2个方法：forwardRequest(httpRequest), 和requestComplete(httpRequet)。 让你implement 这个两个方法。
第二轮是和manager面，基本都是behavior question和一些小的知识点，如https certificate的基本原理，@transctional的用法
第三轮是algorithm：给你长string，以及一个valid word set. 让你判断这个长String 是不是可以分成若干个valid word.
第四轮是system design,设计一个chat log. 因为面试官跟我一样玩dota2,所以是参照dota2里面的频道。用户创建频道，加入频道，并且可以在频道里面聊天
最后一轮还是system design: 你获取一个log stream, log的内是若干的key value pairs 对应userId->visited url。让你求most frequent user visited chain.
比如user1 访问过的url 依次是B->C->D
user2 A->B->C->D
user3 B->C->D->E
那么答案是B->C->D。

除了system design 和 algorithm, 每一轮都会有整整十分钟左右的behavior question, 问你诸如和上司有分歧怎么办，如何平衡代码质量和deadline. 还会就你做的项目问一些问题。

第一轮，白人感觉是manager级别，很友善，一上来说我喜欢第一个面因为大家给我的问题最多。blah blah blah。BQ+OOD停车场。
第二轮，三哥senior了吧也许不是，一上来说，我可能会不make eye contact，可能一直打字，可能打断你，请见谅。我一听这难道是bar raiser的节奏？BQ+ linux find。
第三轮，白人小哥，听口音像澳洲人，上来说给你留多时间写码。给一个串，里面有一个一对一的上司-下属逻辑，要你找出一个人的总下属个数，包括下属的下属。总体不难我写得不好，逻辑自己绕晕了最后没写圆满。小哥脸上的表情都是：你挂了。勉强挤出一点时间BQ。
午饭，白人美国小哥，尬聊尬聊尬聊，泰国菜满辣的，不过他说他是system development engineer招进来的？不是很懂这个hierachy。
第四轮，澳洲小姐姐，系统设计，图像处理系统，基本功能有生成thumbnail，raw 转jpeg/png。人很nice，表情反应还好虽然我就是在瞎几把扯。
第五轮，黑皮肤大哥口音不是特别像美国黑人，纯BQ，不断深挖不断反问，我已经run out of stories了，大哥是微软来的，夸了一大通亚马逊真的对客户很obssesive很amazing。

On-site 总共四轮每轮大概四十分钟到半小时，每轮都有bq
给出inorder和post order的array，构建tree
给m个骰子，每个骰子有n面，求sum是k有多少种可能
Design a juice box
给一个integer stream，如果数字是404，就print出最大的k个数字

强烈吐槽一下亚麻的recruiter，从最开始联系到最后面试来回每封邮件必有出错，包括最关键的面试时间都能发错。。。。

天竺小哥 上来问了两三个bq都是很正常的那种
然后来了一道 lc 刘久思  秒了
然后又问 如果形状一样就算相同怎么办，大致说了一下没写代码，估计就是为了蹭过时间

共五轮，顺序打乱发
国人女  bq 半小时 +  lc幺三九 
白人女 bar raiser  bq半小时 + lc其就把
天竺女， bq半小时  + lc 尔尔思 （只有+ - 以及括号的） follow up：lc齐齐而 讲思路
hiring manager 纯bq. 留学申请论坛-一亩三分地
白人男 bq半小时 货仓机器人取箱子设计 （OOD）

1, BQ + 系统设计：设计一个推特
2，BQ + OOD：设计一个音乐播放器的歌单接口
3，黎口 壹厮遛
4，全程BQBQBQBQ （这一轮非常enjoy）
5，黎口：壹，石舞，石巴


首先開始15min BQ, 1: Tell me a project that you're proud of, 2: Tell me a situation when you have to take risk, 3: A simple way to solve complex problem. 1point3acres

做題：Input 給head of linkedlist and List<Node>, 必須找出這串node之間有幾個斷點(breaks)
. visit 1point3acres for more.
For example 1->2->3->4->5->...->n; [5, 1, 3]長度m, m <= n, 必須return 2 因為 1-3之間不連續，3-5也不連續

live coding但面試官沒跑code，就是用看的並且溝通是否有bug，一開始用traverse LinkedList的方式並非最優解，給了一個hint之後解出來，面試官還算滿意。

以下内容需要积分高于 100 才可浏览
. From 1point 3acres bbs
最優解：Set 記下List裡面的所有Node，然後iterate 一遍，如果currentNode.next不在Set裡，就是有斷點。
必須說明edge case，例如5的下一個6雖然不在Set裡面，但5本身已經Set裡面最後的一個Node，就不算一個斷點。
O(m)

Coding:
1. find the smallest element in a BST
2. find the inorder successor of a node in a BST
3. determine whether a BT is a BST 
Design:
1.a data structure to store a word and its definition
2.what if the data is too big, how could you do?
3.a data structure to improve the performance of query a range of word
ex. apple->cat (return all entry in-between apple, boy, ball, ...... cat)

在职跳槽
内推，社招，第一轮电面
贡献面经给大家

开头20分钟，问了几道bq和技术类的问题
1. why amazon
2. any pround project
3. 英文忘了怎么说了，大意是如果你离开了你现在的公司，你觉得你给你们公司留下了什么财富/永久的贡献之类的 (楼主表示，并没有留下什么LOL）

1. process和thread区别
2. 内存里的stack和heap怎么作用的
3. thread pool是什么，有什么好处
4. 还问了我好多关于锁的问题，楼主表示很久没碰过这些都忘光了
还问了几个system的基础知识吧，忘记了，答得也很烂

Coding的题目反而很简单

给一个string like ‘aaabbabccdc’， 返回 'a4b3c3d'

写一个很久之前的亚麻AWS前端（Web Development Engineer）电面面经吧。
一开始就是互相介绍，聊聊项目之类的。
然后问了几个问题：怎么给网站加速，如果让你选择一项技术你会考虑哪些方面。
之后是代码：第一题就是关于 const，let，var，scope的问题。 第二题javascript FlattenArray()。最后一题UI， 做一个tooltip widget。就是鼠标一hover上去可以弹出内容的。

艾力克灑組波頓
先問BQ:
1.怎麼完成目標
2.系統bug你的解決順序
其他忘了

唎code:
1.dp：
機器人左上角到左下角幾種方法那一題

2.系統設計：
給一個URL API呼叫他可以得到網頁URL
請給出所有子網頁名稱
