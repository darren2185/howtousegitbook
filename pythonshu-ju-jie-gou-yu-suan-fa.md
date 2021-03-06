# Python数据结构与算法

---

算法\(Algorithm\)是实际生活中某类问题而概括出的解决问题方法，程序开发本身就是为了解决某一问题实例而进行的活动，相对而言，设计阶段的工作更困难，其工作基础是问题的说明性描述，有关信息并不是简单地能映射到问题的操作性求解过程中，需要人的智力参与。主要参考用计算机解决问题的已有经验、已开发的技术和方法。编码阶段的工作相对容易些。

算法是对于一个给定的问题，用某种严格方式描述一个求解过程，且对该问题的每个实例，该过程都能给出解。从算法到与之对应的程序，映射关系比较清晰。

算法经验也只是经验，在设计新算法时可参考，但不能保证有效.

#### 算法的性质

1. 有穷性
2. 能行性
3. 终止性
4. 输入/输出

确定性算法和非确定性算法，顾名思义，根据其结果的确定性来区别

#### 算法的描述

描述过程，通常用于交流，而内容是问题的解决过程，有关一个计算应该如何进行。主要目的是帮忙人理解和思考相应的问题求解方法、技术和过程。由于主要为了方便人们的阅读和使用，算法可以采用不同的描述形式，需要在易读、易理解和严格性之间取得平衡。

* 自然语言描述，容易阅读，也比较冗余，易现歧义
* 自然语言、数学记法或公式的结合
* 严格的形式化记法
* 类似于编程语言的形式描述算法过程
* 伪代码

#### 算法设计与分析

所谓算法设计，就是从问题出发，通过分析和思考最终得到一个能解决问题的过程性描述的工作工程，其设计过程中一些常见的通用想法可以称为算法设计模式。

* 枚举法：根据具体问题的枚举出各种可能，从中选出游泳信息或者问题的解
* 贪心法：根据已知的局部信息，完成更多可能的工作。这样做通常可以找到正确的解，但并非最优的答案，而对于复杂的问题，全面考虑的工作代价可能太高，为得到实际可用的算法，会需要在最优方面做出妥协
* 分治法：先将复杂问题分解为相对简单地子问题，分别求解，最后通过组合起子问题的解的方式得到原问题的解
* 回溯法：通过探索求解，如果问题复杂，没有清晰的求解路径，可能就要分步骤进行，而每一步又可能有多种选择，只能采取试探方式，根据实际情况选择一个可能方向。当后续步骤无法继续时，则返回前面步骤，另行选择求解路径。
* 动态规划法：后续步骤根据已知信息，动态选择已知的最好求解路径
* 分支限界法：在搜索过程中，确定某些可能的选择实际上并不真正有用，及早将其删除，以缩小可能的求解空间。

算法的研究和分析中，人们主要关注算法的最坏情况代价，有时也关注平均代价

#### 算法的时间复杂度

常见的几种时间复杂度

![](/assets/shijianfuzadu.png)

在编程中使用一种对象时，只需考虑应该如何使用，不需要（最好是根本不能）去关注和触及对象的内部表示。

抽象数据类型的基本想法是把数据定义为抽象的对象集合，只为他们定义可用的合法操作，并不暴露其内部实现的具体细节，不论是其数据的表示细节还是操作的实现细节。一个数据类型的操作通常可以分为三类：

* 构造操作
* 解析操作
* 变动操作

AD是一种思想，也是一种组织程序的技术，主要包括：

1. 围绕着一类数据定义程序模块
2. 模块的接口和实现分离
3. 在需要实现时，从所用的编程语言里选择一套合适的机制，采用合理的技术，实现ADT功能，包括具体的数据表示和操作

一个类定义确定了一个名字空间，位于类体里面的定义局限于类体，且局部名字在该类之外不能直接看到，不会与外部的名字冲突。

实例：有理数数据类型

```py
class Rational:
    @staticmethod
    def _gcd(m, n=1):
        if n == 0:
            raise ZeroDivisionError("错误：分子为零")
        while True:
            if m == 0:
                return n        
            m, n = n % m, m 

    def __init__(self, num, dec=1):
        if not isinstance(num, int) or not isinstance(dec, int):
            raise TypeError

        if dec == 0:
            raise ZeroDivisionError

        sign = 1

        if num < 0 or dec < 0:
            sign = -sign

        if num < 0 and dec < 0:
            sign = -sign

        num, dec = abs(num), abs(dec)
        g = self._gcd(num, dec)

        self._num = sign * (num // g)
        self._dec = dec // g

    def __add__(self, other):
        return Rational(self._num * other._dec + self._dec * other._num, self._dec * other._dec)

    def __mul__(self, other):
        return Rational(self._num * other._num, self._dec * other._dec)

    def __sub__(self, other):
        return Rational(self._num * other._dec - self._dec * other._num, self._dec * other._dec)


    def __repr__(self):
        return "{0} / {1}".format(self._num, self._dec)

    def __str__(self):
        return "{0} / {1}".format(self._num, self._dec)


r1 = Rational(-16, 32)
r2 = Rational(4, 7)
r1 + r2       # 1/14
```

如何求最大公约数的问题

```py
# 辗转相除法 -- 循环
def gcd_o(m, n=1):
    if n == 0:
        raise ZeroDivisionError("错误：分子为零")
    while True:
        if m == 0:
            return n        
        m, n = n % m, m


def gcd_or(m, n=1):
    # 辗转相除法 -- 递归
    if n == 0:
        raise ZeroDivisionError("错误：分子为零")
    if n % m == 0:
        return m
    return gcd_o(n % m, m)


print(gcd_or(144, 256))


def gcd_j(m, n=1):
    # 更相减损术（等值方法）
    while True:
        if m == n - m:
            return m
        if m > n - m:
            m, n = n - m, m
        else:
            m, n = m, n - m


def gcd_jr(m, n=1):
    if n == 0:
        raise ZeroDivisionError("错误：分子为零")
    if m == n - m:
        return m
    return gcd_jr(*((n - m, m) if m > n - m else (m, n - m)))


print(gcd_jr(32, 1024))
```

动态约束确定调用关系的函数称为虚函数

```py
class B:
    def f(self):
        self.g()
    def g(self):
        print("B.g Called")

class C(B):
    def g(self):
        print('C.g Called')

x = B()
x.g()    # B.g Called
y = C()
y.f()    # C.g Called  当y是C的实例，当y调用f函数时，本身的self指的是当前y，所以self.g()也是调用当前y下的函数
```



