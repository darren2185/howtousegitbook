# 栈和队列

---

栈和队列主要用于在计算过程中保存临时数据，在后面的计算中可能需要使用它们：工作中产生的中间数据暂时不用活着用不完，就有必须把当时不能立刻用掉的数据存起来。栈和对列就是使用最多的缓冲存储结果。

```
ADT Stack:
    Stack(self)                  # 创建空栈
    is_empty(self)               # 判断栈是否为空，空时返回True否则返回False
    push(self, elem)             # 将元素elem加入栈，也常称为压入或推入
    pop(self)                    # 删除栈里最后压入的元素并将其返回，常称为弹出
    top(self)                    # 取得栈里最后压入的元素，不删除
```

实现代码如下：

```py
class SStack:
    def __init__(self):
        self._elem = []

    def is_empty(self):
        return len(self._elem) == 0

    def top(self):
        if self.is_empty():
            raise ValueError('Stack is empty!')
        else:
            return self._elem[-1]

    def push(self, elem):
        self._elem.append(elem)

    def pop(self):
        if self.is_empty():
            raise ValueError('Stack is empty!')
        return self._elem.pop()
```

线性链表实现栈

```py
class LStack:
    def __init__(self):
        self._top = None

    def is_empty(self):
        return self._top is None

    def top(self):
        if self.is_empty():
            raise ValueError('The Stack is empty!')
        return self._top.elem

    def push(self, elem):
        node = SingleNode(elem)
        node.next_node, self._top = self._top, node

    def pop(self):
        if self.is_empty():
            raise ValueError('The Stack is empty!')

        node = self._top
        self._top, node.next_node = self._top.next_node, None
        return node.elem
```

检查括号配对的原则：在扫描正文过程中，遇到的闭括号应该与此前最近遇到且尚未获得匹配的开括号配对，由于存在多种不同的括号，由于存在多种不同的括号，每种括号都可能出线任意多次，而且还可能嵌套。为了检查是否匹配，扫描中必须保存遇到的括号。由于写程序时无法预知要处理的正文里有多少括号需要保存，因此不能用固定数目的变量保存，必须使用缓存，匹配原则：当前闭括号应该与前面最近的尚未配对的开括号陪陪，下一个闭括号应与前面次近的括号匹配。后存入者先使用，复合LIFO原则。

1. 顺序扫描被检查正文（一个字符串）里的一个个字符
2. 检查中跳过无关字符（所有非括号都与当前处理无关）
3. 遇到开括号时将其压入栈
4. 遇到闭括号时弹出当时的栈顶元素与之匹配
5. 如果匹配成功则继续，发现不匹配时检查以失败结束

任何一个递归定义的函数（程序），都可以通过引入一个栈保存中间结果的方式，翻译为一个非递归的过程，与此对应，任何一个包含循环的程序都可以翻译为一个不包含循环的递归函数。

如果遇到一个递归算法，希望做出它的一个非递归实现，更合适的方法是分析算法的具体情况，弄清楚计算的细节，然后根据得到的认识自己设计出相应的非递归函数。

#### 栈的应用：简单背包问题

问题描述：一个背包里可放入重量为weight的物品，现有n件物品的集合S，其中物品的重量分别为w0, w1,....,wn-1。问题是能否从中选出若干件物品，其重量之和正好等于weight。如果存在就说这一背包问题有解，否则就是无解。

