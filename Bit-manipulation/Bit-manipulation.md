# Bit manipulation

## 1. 与操作

### 342. Power of Four

学习一条位运算基础知识：如果n是2^m，那么n-1是m-1个1的重复而n是1后面跟着m-1个0，这样的话n & (n-1) == 0

接着这道题要用到的就是等比数列求和，Sn = a1(q^n - 1)/(q - 1)，赋值q=4, a1 = 1，得到(4^n - 1)必然为3的倍数

```py
return num > 0 and num & (num - 1) == 0 and (num - 1) % 3 == 0
```

### 191. Number of 1 Bits

继续刚才的那条奇技淫巧，n & (n - 1)能够消掉二进制数字最末尾的1，为什么呢？因为最末尾的1以两种形式出现，1后面n个0和1，前者的话，1后面n个0减去1=n个1，两者与操作一下就变成n+1个0，后者的话1-1=0，两者与操作还是0；这题了解这项奇技淫巧之后就反复消掉末尾0即可，我就不上代码了

### 201. Bitwise AND of Numbers Range

与操作的性质：无论多少个数字进行与操作，中间只要有一个0那么结果就必然为0

所以找到开始与结尾数最靠后的一个共用1就行了

```py
def rangeBitwiseAnd(self, m, n):
    r = 2 ** 32 - 1
    while((m&r) != (n&r)):
        r <<= 1
    return m&r
```

## 2. 掩码操作

### 190. Reverse Bits

位操作即使是很基础的技巧也会被认为是魔法的……

这个题的知识点是掩码操作，比如下面例程里的第3行代码，原数字比如是0xabcdefgh，两个掩码操作分别得到0xa0c0e0f0和0x0b0d0f0h，然后一个右移4格（16进制里的1位），一个左移四格，加一起就是0xbadcfehg，连续进行五次即可

```py
class Solution:
    # @param n, an integer
    # @return an integer
    def reverseBits(self, n):
        n = (n >> 16) | (n << 16)
        n = ((n & 0xff00ff00) >> 8) | ((n & 0x00ff00ff) << 8)
        n = ((n & 0xf0f0f0f0) >> 4) | ((n & 0x0f0f0f0f) << 4)
        n = ((n & 0xcccccccc) >> 2) | ((n & 0x33333333) << 2)
        n = ((n & 0xaaaaaaaa) >> 1) | ((n & 0x55555555) << 1)
        return n
```

## 3. 异或操作

### 136. Single Number

基础题，0^x = x，x^x = 0，不上代码了，不难但很基础

### 260. Single Number III

这次是`2n+2`个数字里n个数字出现过两次，两个数字出现过一次

1. 一串数字进行xor操作的话，重复出现的数字就都不存在了，只剩`a^b`了
2. 求这个`a^b`的最低位1，a跟b在这一位上必然是不同的
3. 然后把数组里所有这一位为0的数字和为1的数字分别进行xor操作，因为xor的性质出现两次的数字就消失了，只剩下a和b

```py
def singleNumber(self, nums):
    xor, a, b = 0, 0, 0
    for num in nums:
        xor ^= num
    mask = xor - (xor & (xor - 1))
    for num in nums:
        if num&mask:
            a ^= num
        else:
            b ^= num
    return [a, b]
```

### 268. Missing Number

题目要求说n个数字里包含[0,n+1]每个数字，只是漏掉一个，那么就从0开始每一位异或两次，一个异或角标i，另一个异或值nums[i]，最后再异或一个n，这样我们一共做了2n+1次异或，相当于[0,n+1]每个数字异或了两遍，除了那个漏掉的数字只异或了一遍

## 4. K-map

终于到了通用方法，本科一年级数字电路

### 137. Single Number II

这个题目要求在一群出现过3次的数字里找唯一一个只出现过1次的，可以理解成一个状态机，3个状态的话，00->01->10->00，很容易画出来K-map，求出来两个状态机方程，a = (a^b) & (a^c); b = (b^c) & ~a，后面就不用写了。。。
