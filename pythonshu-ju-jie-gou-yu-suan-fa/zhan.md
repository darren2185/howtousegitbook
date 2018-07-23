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



