# 选择排序

---

沙发看电视就废了



双方都是对方

双方都

```py
def select_sort(alist):
    """选择排序
       不稳定
       时间复杂度：O(N*N)
    """
    n = len(alist)
    print(alist)
    for j in range(n - 1):
        for i in range(j + 1, n):
            if alist[j] > alist[i]:
                alist[j], alist[i] = alist[i], alist[j]

    print(alist)


if __name__ == '__main__':
    alist = [26, 20, 12, 40, 93, 54, 77,20, 31, 44, 55, 226]
    select_sort(alist)
```



