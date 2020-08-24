# 正则表达式匹配
剑指19 | [Link](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/)

## 题目
请实现一个函数用来匹配包含'.'和'\*'的正则表达式。模式中的字符'.'表示任意一个字符，而'\*'表示它前面的字符可以出现任意次（含0次）。在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但与"aa.a"和"ab*a"均不匹配。
```
示例 1:
输入:
s = "aa"
p = "a"
输出: false
解释: "a" 无法匹配 "aa" 整个字符串。

示例 2:
输入:
s = "aa"
p = "a*"
输出: true
解释: 因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。

示例 3:
输入:
s = "ab"
p = ".*"
输出: true
解释: ".*" 表示可匹配零个或多个（'*'）任意字符（'.'）。

示例 4:
输入:
s = "aab"
p = "c*a*b"
输出: true
解释: 因为 '*' 表示零个或多个，这里 'c' 为 0 个, 'a' 被重复一次。因此可以匹配字符串 "aab"。

示例 5:
输入:
s = "mississippi"
p = "mis*is*p*."
输出: false

限制：
s 可能为空，且只包含从 a-z 的小写字母。
p 可能为空，且只包含从 a-z 的小写字母以及字符 . 和 *，无连续的 '*'。
```

## 解答
dp的题一般都比较绕，想清楚之后代码量其实不大。这题有几个难点，首先是如何定义dp。我们这里用dp[i][j]表示s的前i个字符和p的前j个字符是匹配的。
|特殊字符|含义|
|----|----|
|'.'|任意一个字符                     |
|'*'|它前面的字符可以出现任意次（含0次）|

然后就是要分类讨论可能遇到的情况。

- s[i] == p[j] &nbsp; __情况1__
- s[i] != p[j]
  - p[j] == '.' &nbsp; __情况2__
  - p[j] == '*'
    - p[j-1] != s[i] &nbsp; __情况3__
    - p[j-1] == s[i] or p[j-1] == '.' &nbsp; __情况4__
  - p[j] = others __情况5__

分析：
__情况1&2__： dp[i][j] = dp[i-1][j-1]
__情况3__ ：* 代表取0个字符。dp[i][j] = dp[i][j-2]
__情况4__ : 
  * dp[i][j] = dp[i][j-2] (*取0个字符)
  * dp[i][j] = dp[i-1][j] (取多个字符)

__情况5__ : dp[i][j] = False


时间复杂度：O(MN), 空间复杂度: O(MN)
```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        s, p = '#'+s, '#'+p # 帮助空字符匹配
        m, n = len(s), len(p)
        dp = [[False]*n for _ in range(m)]
        dp[0][0] = True

        for i in range(m):
            for j in range(1, n):
                if i == 0: # 空字符的时候单独讨论，初始化
                    dp[i][j] = j > 1 and p[j] == '*' and dp[i][j-2]
                elif p[j] in [s[i], '.']: #情况1，2
                    dp[i][j] = dp[i-1][j-1]
                elif p[j] == '*': #情况3，4
                    dp[i][j] = (j > 1 and dp[i][j-2]) or (p[j-1] in [s[i], '.'] and dp[i-1][j])
                else: #情况5
                    dp[i][j] = False
        return dp[-1][-1]
```