# 数值的整数次方
剑指16 | [Link](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

## 题目
实现函数double Power(double base, int exponent)，求base的exponent次方。不得使用库函数，同时不需要考虑大数问题。

```
示例 1:
输入: 2.00000, 10
输出: 1024.00000

示例 2:
输入: 2.10000, 3
输出: 9.26100

示例 3:
输入: 2.00000, -2
输出: 0.25000
解释: 2^(-2) = 1/2^2 = 1/4 = 0.25

限制：
-100.0 < x < 100.0
n 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。
```

## 解答
因为 $x^n=x^{n-1}x$ 我们可以通过迭代的方式计算。为了简化运算量，我们可以把指数看作二进制，然后做除法，也就是快速幂算法。它实际上是一种二分法的思想。具体来讲，对于一个一个任意指数
$$n= 1 \times a_1 + 2\times a_2 + 4 \times a_3 + ... + 2^m \times a_m$$, 于是有
$$x^n = x^{a_1} (x^2)^{a_2}...(x^{2^m})^{a_m}$$，其中$a_i$都为0或1。每次迭代中，把$x$变为$x^2$实现到下一项。如果指数（二进制下）所在位是1（n%2 == 1 或者 n&1 == 1），结果就乘x否则乘1，然后下一个循环指数>>1右移，或者//2。

注意指数是负数的情况。

时间复杂度：O(log<sub>2</sub>N), 空间复杂度: O(1)
```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n == 0:
            return 1
        if n < 0:
            return self.myPow(1/x, -n)
    
        if n % 2 == 1:
            return x*self.myPow(x, n-1)
        else:
            return self.myPow(x*x, n//2)
```
----
用bit manipulation提高速度，同时可以写成递归的形式。
```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n < 0:
            x, n = 1/x, -n
        
        res = 1
        while n > 0:
            if n & 1 == 1:
                res *= x
            x *= x
            n >>= 1
        return res
```