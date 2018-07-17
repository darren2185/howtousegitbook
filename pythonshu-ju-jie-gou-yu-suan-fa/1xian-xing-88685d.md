# 线性表

---

集合E上的一个线性表就是E中一组有穷个元素排成的序列L=\(e0, e1,...., en-1\)，其中ei属于E且n ≥ 0。在一个表里可以包含0个或多个元素，序列中的每个元素在表里有一个确定的位置，称之为下表，Python一般从0开始。一个表中包含的元素的个数称为长度，显然，空表为0。在一个费控的线性表里，存在着唯一的首元素和一个尾元素，除首元素外，表中每个元素都有一个前驱元素，与之相对的除尾元素外，表中每个元素都有一个后驱元素。

#### 线性表抽象数据类型

```ADT
ADT List:                           # 一个线性表抽象数据类型
    List(self)                      # 表构造操作，创建一个新表
    is_empty(self)                  # 判断self是否为空表
    length(self)                    # 获得self的长度
    prepend(self, element)          # 将元素element加入表中作为第一个元素
    append(self, element)           # 将元素element加入表中作为最后一个元素
    insert(self, element, index)    # 将元素element加入表中作为第index个元素，其他元素的顺序不变
    del_first(self)                 # 删除表中的首元素
    del_last(self)                  # 删除表中的尾元素
    del(self, index)                # 删除表中的第i个元素
    search(self, element)           # 查找元素element在表中的出现位置，不出现则返回 -1
    forall(self,op)                 # 对表中的每个元素执行操作Op
```

### 顺序表

表中元素顺序存放在一片足够大的连续存储区里，首元素存入存储区的开始位置，其余元素依次顺序存放。元素之间的逻辑顺序关系通过元素在存储区里的物理位置表示。

表的顺序实现（书序表）的总结：

优点：O\(1\)时间的（随机、直接的）按位置访问元素；元素在表里存储紧凑，除表元素存储区之外只需要O\(1\)空间存放少量辅助信息。

缺点：需要连续的存储区存放表中的元素，如果表很大，就需要很大片的连续内存空间。一旦确定了存储块的大小，可容纳单元个数并不随着插入/删除操作的进行而变化。如果很大的存储区里只保存了少量数据，就会有大量空闲单元，造成表内的存储浪费。在执行加入或删除操作时，通常需要移动许多元素，效率低。建表时需要考虑存储区大小，而实际需求很难事先估计。![](/assets/shunxubiao.png)

##### 总结

采用顺序表结构实现线性表：

* O\(1\)时间的定位元素访问，很多简单操作的效率也比较高
* 由于元素在顺序表的存储区里连续排列，加入/删除操作有可能移动很多元素，操作代价高
* 只有特殊的尾端插入/删除操作具有O\(1\)时间复杂度，插入操作复杂度还收到元素存储区固定大小的闲置。通过适当的存储区扩充策略，一系列尾端插入可以达到O\(1\)的平均复杂度。

顺序表的优点和缺点都在于其元素存储的集中方式和连续性。从缺点看，这样的表结构不够灵活，不容易调整和变化。

#### 链表

1， 能够找到表中的首元素，2，从表里的任一元素出发，可以找到它之后的下一个元素，3，并不一定需要连续存储元素，基于链接结构，用链接关系显示表示元素之间的顺序关联（连接表）

![](/assets/danlianbiao.png)为了掌握一个表，只需要用一个变量保存这个表的首节点的引用（表头指针）

##### 链表操作的复杂度

总结下链表操作的时间复杂度：

创建空表：O\(1\)

删除表：在Python里是O\(1\)，当然Python解释器做存储管理需要时间

判断空表：O\(1\)

加入元素：

* 首端加入元素：O\(1\)
* 尾端加入元素：O\(n\)
* 定位删除元素：O\(n\)，平均情况和最坏情况

其他删除：通常需要扫描整个表或其一部分，O\(n\)

扫描、定位或遍历操作都需要检查一批表节点，其复杂度受到表节点数的约束，都是O\(n\)操作。

#### 不同链表的总结

1. 基本单链表包含一系列节点，通过一个方向的链接构造起来，支持高效的\(O\(1\)\)前段插入和删除操作，定位操作或尾端操作都需要O\(n\)时间
2. 增加了尾结点引用域的单链表可以很好的支持首端/尾端插入和首端弹出元素，他们都是O\(1\)时间复杂度的操作，但不能支持高效的尾端删除
3. 循环单链表也能支持高效的表首端/尾端插入和首端弹出元素。在这种表上扫描，需要特别注意结束判断问题
4. 双链表中每个结点都有两个方向的链接，因此可以高效地找到前后结点。如果有尾结点引用，两端插入和删除操作都能在O\(1\)时间完成
5. 对于单链表，遍历和数据检索操作都只能从表头开始，需要O\(n\)时间。对于双链表，这些操作可以从表头或表尾开始，复杂度不变。与它们对应的两种循环链表，遍历和检索可以从表中任何一算法 个地方开始，但要注意结束条件。

链接表有一些重要**优点**：

* 表结构是通过一些链接起来的结点形成的，结点之间的顺序由链接关系决定，链接可以修改，因此表的结构很容易调整和修改
* 不需要修改结点里的数据元素或移动它们，只通过修改结点之间的链接，就能灵活的修改表的结构和数据排列方式。
* 整个表由一些小的存储块构成，比较容易安排和管理。

连接表的一些明显**缺点:**

* 定位元素需要线性时间，这是与顺序表相比的最大优势
* 简单单链表上的尾端操作需要线性时间，增加一个尾指针，可以将尾端插入变成常量操作时间，但仍不能有效实现尾端删除。双链表通过在每个结点增加第二个链接，可以实现两端的高效插入和删除。
* 要找当前元素的前一个元素，必须从头开始扫描表结点，这种操作应尽量避免。双链表可以解决此问题，但每个结点要付出更多存储代价
* 为存储一个表元素，需要多用一个链接域，这是实现链接表的存储代价。双链表可以提高链表操作的灵活性，但需要增加两个链接域。

#### 实现：

![](/assets/shuxubiaoandlianbiao.PNG)

#### 1.简单顺序列表

```py
class SimpleSequenceList:
    """简单顺序表
       实现以下功能：
       _num                     记录有多少个元素，即长度
       is_empty(self)           判断是否为空
       length --- property      属性长度, 只读属性
       append(elem)             末端添加
       pop()                    删除前端元素
       prepend(elem)            前端添加
       pop_last()               删除末端元素
       insert(i, elem)          根据位置i添加元素
       """
    def __init__(self, *args):
        self._num = 0
        self._container = []

        if len(args) != 0:
            self._container += args

    @property
    def length(self):
        return len(self._container)

    def is_empty(self):
        return len(self._container) == 0

    def append(self, elem):
        self._container.append(elem)
        self._num += 1

    def prepend(self, elem):
        # 1
        # 不保序前端加入
        # if self.is_empty():
        #     self._container.append(elem)
        # else:
        #     self._container.append(elem)
        #     self._container[0], self._container[len(self._container) - 1] = \
        #         self._container[len(self._container) - 1], self._container[0]
        #
        # 2 保序前端插入
        if self.is_empty():
            self._container.append(elem)
        else:
            self._container.append(elem)
            p = elem
            for i in range(len(self._container)-1, 0, -1):
                self._container[i] = self._container[i - 1]

            self._container[0] = p

    def __repr__(self):
        s = ""
        for i in self._container:
            s += str(i)+", "
        return s

    def travel(self):
        for i in range(self.length):
            print(self._container[i], end=" ")
        print(" ")

    def pop(self):
        if self.is_empty():
            raise ValueError('此表目前为空表')

        return self._container.pop(0)

    def pop_last(self):
        if self.is_empty():
            raise ValueError('此表目前为空表')

        return self._container.pop(len(self._container) - 1)

    def insert(self, index, elem):

        if self.is_empty():
            self._container.append(elem)
            return

        if 0 < index < self.length:
            self._container.append(elem)
            for i in range(self.length-1, index, -1):
                self._container[i] = self._container[i - 1]

            self._container[index] = elem
        elif index >= self.length:
            self._container.append(elem)
        else:
            self.prepend(elem)
```

#### 简单单链表

```py
class SingleNode:
    """
    结点定义:
    elem      Property
    next_node Property
    """
    def __init__(self, elem=None):
        self.__elem = elem
        self.__next = None

    @property
    def elem(self):
        return self.__elem

    @elem.setter
    def elem(self, elem):
        self.__elem = elem

    @property
    def next_node(self):
        return self.__next

    @next_node.setter
    def next_node(self, node=None):
        self.__next = node
    
class Node(SingleNode):
    def __init__(self, elem=None, prenode=None, nextnode=None):
        self._pre_node = prenode
        super(Node, self).__init__(elem, nextnode)

    @property
    def pre_node(self):
        return self._pre_node

    @pre_node.setter
    def pre_node(self, node):
        self._pre_node = node

class SingleLinkList:
    """实现单链表
       is_empty                判断是否为空
       length                  property 链表长度
       travel                  遍历链表
       prepend                 首端添加结点
       append                  末端添加结点
       insert                  指定位置插入
       remove(item)            删除结点,指定元素
       search(item)            查找含有item的节点
    """
    def __init__(self, node=None):
        self._head = node

    def is_empty(self):
        """链表是否为空"""
        return self._head is None

    def length(self):
        """链表节点数量"""
        # _cur表示当前游标
        _cur = self._head

        # _count表示计数器
        _count = 0

        while _cur:
            _count += 1
            _cur = _cur.next_node

        return _count

    def __len__(self):   # 使用len(object)函数获取长度
        return self.length()

    def travel(self):
        """遍历单链表"""
        # _cur表示当前游标
        _cur = self._head

        while _cur:
            print(_cur.elem, end=' ')
            _cur = _cur.next_node
        print(" ")

    def __str__(self):
        """返回所有元素字符串"""
        _l = []
        _cur = self._head

        while _cur is not None:
            _l.append(str(_cur.elem))
            _cur = _cur.next_node

        return ", ".join(_l)

    def prepend(self, item):
        """首端增加节点"""
        node = SingleNode(item)
        if self.is_empty():
            self._head = node
        else:
            node.next_node, self._head = self._head, node

    def append(self, item):
        """尾端增加节点"""
        node = SingleNode(item)

        if self.is_empty():
            self._head = node
        else:
            _cur = self._head
            while _cur.next_node:
                _cur = _cur.next_node
            _cur.next_node = node

    def insert(self, pos, item):

        """插入某个节点位置，如果pos值大于length则在尾部添加，如果小于等于0则首端操作"
           其余则正常处理
           :param pos  从0开始
           :param item 节点元素
           """
        node = SingleNode(item)
        _count = 0

        if self.is_empty() or pos <= 0:
            self.prepend(item)

        elif pos > self.length() - 1:
            self.append(item)

        else:
            _cur = self._head

            while _count < pos - 1:
                _count += 1
                _cur = _cur.next_node

            node.next_node, _cur.next_node = _cur.next_node, node

    def remove(self, item):

        """删除数据，使用两个指针，_cur表示当前指针，_pre则表示当前节点的上一节点，"""
        """这样处理便于删除当前节后，前后两节点链接_pre.next_node = _cur.next_node"""
        _pre = _cur = self._head
        while _cur:
            if _cur.elem == item:
                if self._head == _cur:
                    self._head = _cur.next_node
                else:
                    _pre.next_node = _cur.next_node
                break
            else:
                _pre, _cur = _cur, _cur.next_node

    def search(self, item):
        """查找节点元素"""
        _cur = self._head
        while _cur:
            if _cur.elem == item:
                return True
            else:
                _cur = _cur.next_node
        return False

    def __contains__(self, item):
        return self.search(item)
```

#### 带尾指针的单链表

```py
class SimpleSingleLinkWith:
    """带尾指针的单链表，self._rear->最后节点，便于尾端插入、删除"""
    def __init__(self, node=None):
        self._rear = self._head = node

    def _length(self):
        _cur = self._head
        _count = 0
        while _cur:
            _count += 1
            _cur = _cur.next_node
        return _count

    def __len__(self):
        """返回链表长度"""
        return self._length()

    @property
    def is_empty(self):
        """判断列表是否为空"""
        return self._head is None

    def prepend(self, item):
        """首端添加结点"""
        node = SingleNode(item)
        if self.is_empty:
            self._head = self._rear = node
        else:
            self._head, node.next_node = node, self._head

    def append(self, item):
        """尾端添加结点"""
        node = SingleNode(item)
        if self.is_empty:
            self._head = self._rear = node
        else:
            self._rear.next_node, self._rear = node, node

    def insert(self, pos, item):
        """插入某个节点位置，如果pos值大于length则在尾部添加，如果小于等于0则首端操作
           其余则正常处理
           :param pos  从0开始
           :param item 节点元素
           """
        if pos <= 0:
            self.prepend(item)
        elif pos > self._length() - 1:
            self.append(item)
        else:
            node = SingleNode(item)
            _cur = self._head

            _count = 0
            while _count < pos - 1:
                _count += 0
                _cur = _cur.next_node
            node.next_node, _cur.next_node = _cur.next_node, node

    def pop_first(self):
        """删除头结点"""
        if self.is_empty:
            return None
        else:
            elem = self._head.elem
            self._head = self._head.next_node
            return elem

    def pop_last(self):
        """删除尾结点，同时需要考虑如何使尾结点前移的操作，找到尾结点的上一节点_cur.next_node == self._rear"""
        if self._rear is None:
            return None
        else:
            elem = self._rear.elem
            _cur = self._head

            while _cur.next_node is not self._rear:
                _cur = _cur.next_node

            self._rear = _cur
            return elem

    def remove(self, item):
        """删除含有item的节点,需要注意两个特殊位置（首端节点、尾端节点）"""
        _pre = _cur = self._head
        while _cur:
            if _cur.elem == item:
                if self._head == _cur:
                    self._head = _cur.next_node
                elif self._rear == _cur:
                    self._rear, _pre.next_node = _pre, self._rear.next_node
                else:
                    _pre.next_node = _cur.next_node
                break
            else:
                _cur, _pre = _cur.next_node, _cur

    def search(self, item):
        """查找含有item的节点,如有则TRUE，否则FALSE"""
        _cur = self._head
        while _cur:
            if _cur.elem == item:
                return True
            else:
                _cur = _cur.next_node

        return False

    def __contains__(self, item):
        return self.search(item)

    def __str__(self):
        """返回所有元素字符串"""
        _l = []
        _cur = self._head

        while _cur is not None:
            _l.append(str(_cur.elem))
            _cur = _cur.next_node

        return ", ".join(_l)
```

#### 单向循环链表

```py
class SingleLinkCircle:
    """单向循环列表"""
    def __init__(self, node=None):
        """判断node，如果为None,则初始化self._head=None,否则node.next_node指向自己，构成闭环"""
        self._head = self._rear = node
        if node is not None:
            node.next_node = node

    def _is_empty(self):
        """首节点为空，则为空"""
        return self._head is None

    def _length(self):
        """需要注意当节点为1个时候，如何去判断，其余的判端条件_cur is not self._head"""
        _cur = self._head
        _count = 0
        if self._head is None:
            return _count
        elif _cur.next_node == _cur:
            _count += 1
        else:
            while _cur is not self._rear:
                _count += 1
                _cur = _cur.next_node

            if _cur.next_node is self._head:
                _count += 1
        return _count

    def __len__(self):
        return self._length()

    def prepend(self, item):
        node = Node(item)

        if self._is_empty():
            self._head = self._rear = node
            node.next_node = node
        else:
            node.next_node, self._head, self._rear.next_node = self._head, node, node

    def append(self, item):
        node = Node(item)

        if self._is_empty():
            self._head = self._rear = node
            node.next_node = node
        else:
            node.next_node, self._rear.next_node, self._rear = self._rear.next_node, node, node

    def insert(self, pos, item):
        node = Node(item)

        if pos <= 0:
            self.prepend(item)
        elif pos > self._length() - 1:
            self.append(item)
        else:
            _cur = self._head
            _count = 0

            while _count < pos - 1:
                _count += 1
                _cur = _cur.next_node

            node.next_node, _cur.next_node = _cur.next_node, node

    def remove(self, item):
        """删除特定item元素的结点"""
        _pre = _cur = self._head

        while _cur and _cur is not self._rear:
            if _cur.elem == item:
                if _cur == self._head:
                    if _cur.next_node == _cur:
                        self._head = self._rear = None
                    else:
                        self._head = _cur.next_node
                        self._rear.next_node = _cur.next_node
                    break
                else:
                    _pre.next_node = _cur.next_node
                break
            else:
                _pre = _cur
                _cur = _cur.next_node

        if _cur.next_node is self._rear and _cur.next_node.elem == item:
            _pre.next_node, self._rear = self._rear.next_node, _pre

    def __str__(self):
        _l = []
        _cur = self._head

        while _cur is not self._rear:
            _l.append(str(_cur.elem))
            _cur = _cur.next_node
        if _cur.next_node == self._head:
            _l.append(str(_cur.elem))

        return ", ".join(_l)

    def __contains__(self, item):
        _cur = self._head

        while _cur is not self._rear:
            if _cur.elem == item:
                return True
            _cur = _cur.next_node

        if _cur is self._rear and _cur.elem == item:
            return True

        return False
```

#### 双向循环链表

此处忽略双向链表，其操作功能与循环列表类似，仅尾部判断条件有区别。

```py
class DoubleLinkCircle:
    """ 双向循环列表， 每个结点有后指针并含有前指针，首端结点的pre_node指向尾结点，末端结点的next_node指向首结点"""
    def __init__(self, node=None):
        self._head = node

    def is_empty(self):
        """判断是否为空"""
        return self._head is None

    def __str__(self):
        _l = []
        if self.is_empty():
            return None
        else:
            _cur = self._head.next_node
            _l.append(str(self._head.elem))

            while _cur is not self._head:
                _l.append(str(_cur.elem))
                _cur = _cur.next_node

        return ", ".join(_l)

    def prepend(self, item):
        """头部添加节点"""
        node = Node(item)
        if self.is_empty():
            self._head = node
            node.pre_node, node.next_node = node, node
        else:
            node.next_node, node.pre_node = self._head, self._head.pre_node
            self._head.pre_node.next_node, self._head.pre_node = node, node
            self._head = node

    def append(self, item):
        """尾部添加节点"""
        node = Node(item)

        if self.is_empty():
            self._head = node
            node.pre_node, node.next_node = node, node
        else:
            node.next_node, node.pre_node, self._head.pre_node.next_node, \
                self._head.pre_node = self._head, self._head.pre_node, node, node

    def insert(self, pos, item):
        """从中间pos位置中，添加节点"""
        if pos <= 0:
            self.prepend(item)
        elif pos > len(self) - 1:
            self.append(item)
        else:
            _cur = self._head
            _count = 0
            while _count < pos - 1:
                _cur = _cur.next_node
                _count += 1

            node = Node(item)
            node.next_node, node.pre_node, _cur.pre_node.next_node, \
                _cur.pre_node = _cur, _cur.pre_node, node, node

    def __len__(self):
        if self.is_empty():
            return 0
        else:
            _count = 1
            _cur = self._head.next_node

            while _cur is not self._head:
                _count += 1
                _cur = _cur.next_node

            return _count

    def __contains__(self, item):
        """判断是否含有item，有则True, 无则False"""
        _cur = self._head

        while _cur and _cur.next_node is not self._head:
            if _cur.elem == item:
                return True
            else:
                _cur = _cur.next_node

        if _cur.next_node is self._head and _cur.elem == item:
            return True

        return False

    def remove(self, item):
        """删除含有元素item结点, 无需借助另外的_pre来寻找上一个节点"""
        _cur = self._head

        while _cur and _cur.next_node is not self._head:
            if _cur.elem == item:
                if _cur == self._head:
                    _cur.pre_node.next_node = self._head.next_node
                    _cur.next_node.pre_node = self._head.pre_node
                    self._head = _cur.next_node
                else:
                    _cur.pre_node.next_node = _cur.next_node
                    _cur.next_node.pre_node = _cur.pre_node

                break
            else:
                _cur = _cur.next_node

        if _cur.next_node == self._head:
            _cur.pre_node.next_node = self._head
            self._head.pre_node = _cur.pre_node

        _cur.next_node = _cur.pre_node = None
```



