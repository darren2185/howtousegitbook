 

# 冒泡排序

---

第三方士大夫

双方都 

第三方士大夫

```py
def bubble(alist):
    n = len(alist)
    for j in range(n-1):
        for i in range(n-1-j):
            if alist[i] > alist[i + 1]:
                alist[i], alist[i + 1] = alist[i+1], alist[i]


if __name__ == '__main__':
    li = [54, 26, 93, 17, 77, 31, 44, 55, 20]
    bubble(li)
    print(li)
```



