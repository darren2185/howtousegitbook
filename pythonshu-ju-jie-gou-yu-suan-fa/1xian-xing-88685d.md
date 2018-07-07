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

表中元素顺序存放在一片足够大的连续存储区里，首元素存入存储区的开始位置，其余元素依次顺序存放。元素之间的逻辑顺序关系通过元素在存储区里的物理位置表示



