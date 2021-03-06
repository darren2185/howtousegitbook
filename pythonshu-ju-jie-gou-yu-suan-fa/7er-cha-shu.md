# 二叉树

---

##### 二叉树的性质

1. 在非空二叉树的第i层中至多有$$2^i$$结点
2. 高度为h的二叉树最多有$$2^{k + 1} - 1$$
3. 对于任何非空二叉树_T_，如果其叶结点的个数$$n_0$$，度数为2的结点个数为$$n_2$$，那么$$n_0 = n_2 + 1$$。
4. 满二叉树里的叶结点比分支结点多一个
5. （扩充二叉树的内部和外部路径长度）扩充二叉树的外部路径长度_**E**_是从树根到树中各外部结点的路径长度之和，内部路径长度_**I**_是从树根到树中各内部结点的路径长度之和。如果该树有n个内部结点，那么$$E = I + 2 * n$$
6. $$n$$个结点的完全二叉树高度$$h = \lfloor \log_2n \rfloor$$，即为不大于$$\log_2n$$的最大整数。
7. （完全二叉树）如果$$n$$个结点的完全二叉树的结点按层次并按从左到右的顺序从0开始编号，对任一结点$$i$$（$$0 \le i \le n-1$$）都有：

8. 序号为0的结点是根。

9. 对于$$i \gt 0$$，其父结点的编号是$$(i - 1) / 2$$.

10. 若$$2 \times i + 1 \lt n$$，其左子结点需要为$$2 \times i + 1$$，否则它无左子结点

11. 若$$2 \times i + 2 \lt n$$，其右子结点需要为$$2 \times i + 2$$，否则它无右子结点

12. **完全二叉树**

对于一棵高度为$$h$$的二叉树，如果其第0层至第$$h - 1$$层的节点都满（也就是说，对所有$$0 \le i \le h - 1$$，第$$i$$层有$$2^i$$个结点）。如果最下一层的节点不满，则所有节点在最左边连续排列，空位都在右边。就是一棵完全二叉树

树形结构也是由结点和结点之间的链接关系构成，其结构与线性结果不同：

1. 一个结构如果不空，其中就存在着唯一的起始结点，称为根结点
2. 按结构的链接关系，根结点外的其余结点都有且只有一个前驱，一个节点可以有0个或多个后继
3. 结构里的所有节点都在树根结点通过后继关系可以达的结点结合里。从树根结点出发，经过若干次后继关系可以到达结构中的任一结点
4. 结点之间的联系不会形成循环关系

```
ADT BinTree                                   #一个二叉树抽象数据类型
    BinTree(self, data, left, right)          #构造操作、创建一个新二叉树
    is_empty(self)                            #判断self是否为一个空二叉树
    num_nodes(self)                           #求二叉树的结点个数
    data(self)                                #获取二叉树根存储的数据
    left(self)                                #获取二叉树的左子树
    right(self)                               #获取二叉树的右子树
    set_left(self,btree)                      #用btree取代原来的左子树
    set_right(self, btree)                    #用btree取代原来的右子树
    traversal(self)                           #遍历二叉树中各结点数据的迭代器
    forall(self, op)                          #对二叉树中的每个结点的数据执行操作op
```

如果知道了一棵二叉树的遍历序列，又知道另一遍历序列（无论是先根还是后根序列），就可以唯一确定这个二叉树

### 优先队列

存入其中的每项数据都另外附有一个数值，表示这个项的优先程度，称其为优先级。优先队列应该保证，在任何时候访问或弹出的，总是当时在这个结构里保存的所有元素中优先级最高的。在一些情景中，可能出现不同元素具有相同优先级的情况，如果不止一个元素的优先级最高，优先队列将保证访问或弹出的是它们中的一个，具体是哪个元素由内部实现确定。

##### 有关实现方法的考虑

* 在存入数据时，保证表中元素始终按优先顺序排列，任何时候都可以直接渠道当时在表里最优先的元素。采用有组织的元素存放方式，存入元素的操作比较麻烦，效率可能较低，但访问和弹出时比较方便。
* 存入数据时采用最简单地方式，需要取用时，通过检索找到最优先的元素。采用这种无组织的方式存放元素，把选择最优元素的工作推迟到访问、取出时，存入操作的效率高但取用麻烦。

##### 若使用二叉树来表示优先队列，必须解决一个问题：如何在反复插入和删除元素的过程中，持续保持树结构的特点和操作效率

### 堆

堆是结点里存储数据的完全二叉树，但堆中数据的存储要满足一种特殊的堆序：任一个结点里所村的数据先于或等于其子结点里的数据：

1. 在一个堆中从树根到任何一个叶结点的路径上，各结点里所存的数据按规定的优先关系递减
2. 堆中最优先的元素必须位于二叉树的根结点里，O\(1\)时间就能得到
3. 位于树中不同路径上的元素，这里不关心其顺序关系

用堆作为优先队列，可以直接得到堆中的最优先元素，O\(1\)时间，需要解决两个问题：

* 如何实现插入元素的操作：向堆中加入一个新元素，必须能通过操作，得到一个包含了所有原元素和刚加入的新元素的堆
* 如何实现弹出元素的操作：从堆中弹出最小元素后，必须能把剩余元素重新做成堆。

### 二叉树定义

第三方第三方

### 二叉树遍历

沙发斯蒂芬

##### 递归实现

舒服舒服

#### 非递归实现

沙发斯蒂芬

### 构建二叉树

### 哈夫曼树

扩充二叉树的外部路径长度，即根到其外部结点的路径长度之和：$$E = \sum_{i=1}^{m}l_i$$，其中m是扩充二叉树中外部结点的个数，$$l_i$$是从根到外部结点$$i$$的路径长度。

###### 带权扩充二叉树的外部路径及长度

给扩充二叉树的每个外部结点标一个数值，称为该结点的权，表示与该叶有关的某种性质。进而定义带权扩充二叉树的外部路径长度为：$$WPL = \sum_{i=1}^mw_il_i$$，其中$$w_i$$是外部结点$$i$$的权。

**哈夫曼树：**设实数集$$W=\{ {w_0,w_1,\ldots,w_{m-1}}\}$$，$$T$$是棵扩充二叉树，某m个外部结点分别以$$w_i (i=1,2,\ldots,n-1)$$为权，而且$$T$$的带权外部路径长度为$$WPL$$在所有这样的扩充二叉树中达到最小，则称$$T$$为数据集$$W$$的最优二叉树或者哈夫曼树。

