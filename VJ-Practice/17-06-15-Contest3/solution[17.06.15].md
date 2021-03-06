# Solution
```
/******************
  开始编辑时间：  17:22 17/06/15
  结束编辑时间：  

    VJudge链接：  https://cn.vjudge.net/contest/167386
CodeForces链接：  http://codeforces.com/contest/535

题目按CF顺序排序
******************/
```

***

## #A Tavas and Nafas
```
/******************
    VJudge链接：  https://cn.vjudge.net/contest/167386#problem/B
CodeForces链接：  http://codeforces.com/contest/535/problem/A

      时间限制：  1s
      空间限制：  256MB
      主要算法：  我不知道…
******************/
```
### 题意
唔，大致题意就是给出一个0到99间的数字然后输出对应的英文？
没啥好讲的……

***
## #B Tavas and SaDDas
```
/******************
    VJudge链接：  https://cn.vjudge.net/contest/167386#problem/E
CodeForces链接：  http://codeforces.com/contest/535/problem/B

      时间限制：  1s
      空间限制：  256MB
      主要算法：  dfs
******************/
```
### 题意
把仅由4和7组成的数字称为**幸运的数字**，给出一个**幸运的数字**，求它在所有*幸运数字*中排第几（从小到大）？
### 题解
dfs枚举全部情况即可，最多只有9位，就是最多2^9种情况233，一道水题。

***
## #C Tavas and Karafs
```
/******************
    VJudge链接：  https://cn.vjudge.net/contest/167386#problem/C
CodeForces链接：  http://codeforces.com/contest/535/problem/C

      时间限制：  2s
      空间限制：  256MB
      主要算法：  二分答案 数学
******************/
```
### 题意
给出一个无限长的等差数列（首项为A，公差为B），再给出n个询问，每个询问有3个数l,t,m，要求一个数r，使该等差数列中第l项到第r项能被至多t次m-bite操作减为0。定义一次m-bite操作为，选取m个数字，使每个数字减少1。
### 题解
可以发现任意一个数最多能减t次，故l至r中任一个数不能大于t。而该等差数列单调递增，所以只要第r项小于t，整个子序列的数都会小于t。可以计算出r的最大值为[(t-l的高度)/B]+l。而r>l，所以容易算出r的取值区间。由此可以想到二分答案。对于r值正确性的验证，只要子序列所有数之和小于(m*t)即可。
### Note
额，对于二分答案，这次找到了一个好一些的方法。代码
```C++
while (l != r) {
    mid = (l + r) / 2;
    ***
    if (check(mid)) l = mid;
    else r = mid - 1;
}
```
在l+1=r时容易死循环。所以把上方的`mid = (l + r) / 2;`改为`mid = (l + r + 1) / 2`，这样就可以啦233

***
## #D Tavas and Malekas
```
/******************
    VJudge链接：  https://cn.vjudge.net/contest/167386#problem/A
CodeForces链接：  http://codeforces.com/contest/535/problem/D

      时间限制：  2s
      空间限制：  256MB
      主要算法：  字符串匹配（KMP）
******************/
```
### 题意
有一个字符串s，它的长度已知为n。另有一个模式串t。现给出t，以及t在s中能够匹配的若干位置（非全部位置），求n的所有可能情况数，答案对1e9+7取模。
### 题解
给出的匹配位置已经是升序的了，只要将相邻两个位置比较，如果差距大于等于模式串t的长度，就是能刚好存下一个t，那就不存在冲突；如果两个字符串有重叠，那么如果要没有冲突，两个字符串重叠的部分必须要相同。可以发现，此时的重叠部分正好是串t的前后缀。由此可以想到KMP的next数组。首先将串t预处理出next数组，之后可以从最后一位向前跳直到不再有相同前后缀，这个过程中跳到的有效值即为容许的重叠位数。在之后的过程中，每当重叠的位数不被容许，即为一个冲突。当任何一个冲突发生时，可以直接判定方案数为0。如果没有冲突，那么除去模式串的匹配位置，剩下的未被覆盖的位置每个位置可以填26个字母，所以答案为26^(未被覆盖的位置数量)。可以用快速幂加速。
***
## #E Tavas and Pashmaks
```
/******************
    VJudge链接：  https://cn.vjudge.net/contest/167386#problem/D
CodeForces链接：  http://codeforces.com/contest/535/problem/E

      时间限制：  1s
      空间限制：  256MB
      主要算法：  计算几何 凸包
******************/
```
### 题意
有一个比赛，分为两个阶段，每个阶段为竞速的形式，路程未知，先到终点者胜出。现给出n个人每个人在两个阶段分别的平均速度si和ri，求哪些人有机会赢。
### 题解
可以发现，对于每个人，它的总用时为(S/si + R/ri)（S，R分别为两个阶段的路程），这个数即为向量(S, R)与(1/si, 1/ri)的内积。
# To be continued...
