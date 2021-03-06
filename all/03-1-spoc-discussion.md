# lec5 SPOC思考题


NOTICE
- 有"w3l1"标记的题是助教要提交到学堂在线上的。
- 有"w3l1"和"spoc"标记的题是要求拿清华学分的同学要在实体课上完成，并按时提交到学生对应的git repo上。
- 有"hard"标记的题有一定难度，鼓励实现。
- 有"easy"标记的题很容易实现，鼓励实现。
- 有"midd"标记的题是一般水平，鼓励实现。


## 个人思考题
---

请简要分析最优匹配，最差匹配，最先匹配，buddy systemm分配算法的优势和劣势，并尝试提出一种更有效的连续内存分配算法 (w3l1)
```
最优匹配：可以利用小碎片，但会产生更小的碎片，导致回收困难
最差匹配：可以抑制外碎片的产生，但是可能导致大块内存分配失败，且回收内存时性能不佳
最先匹配：回收内存时比较快，但是分配内存时性能会下降，而且容易产生外碎片
buddy system:　分配内存速度快，没有外碎片，但是会产生内碎片
可以预分配一系列不同大小的内存，每次申请内存时从预分配的内存块中以最优匹配分配
```
```
  + 采分点：说明四种算法的优点和缺点
  - 答案没有涉及如下3点；（0分）
  - 正确描述了二种分配算法的优势和劣势（1分）
  - 正确描述了四种分配算法的优势和劣势（2分）
  - 除上述两点外，进一步描述了一种更有效的分配算法（3分）
 ```
- [x]  

>  

## 小组思考题

请参考ucore lab2代码，采用`struct pmm_manager` 根据你的`学号 mod 4`的结果值，选择四种（0:最优匹配，1:最差匹配，2:最先匹配，3:buddy systemm）分配算法中的一种或多种，在应用程序层面(可以 用python,ruby,C++，C，LISP等高语言)来实现，给出你的设思路，并给出测试用例。 (spoc)
```
SIZE = 20

class Node:
    start = 0
    size = 2 ** SIZE
    no = 1
    
    def __init__(self, st, sz, n):
        self.start = st
        self.size = sz
        self.no = n

free = []
used = []
def log(x):
    n, k = 0, 1
    while (k < x):
        n += 1
        k += k
    return n

def min(x, y):
    if (x < y):
        return x
    else:
        return y

def malloc(size):
    n = log(size)
    k = n
    while (k <= SIZE and len(free[k]) == 0):
        k += 1
    if (k > SIZE):
        return None

    node = free[k][0]
    free[k] = free[k][1:]
    while (k > n):
        free[k - 1].append(Node(node.start, node.size / 2, node.no * 2))
        node = Node(node.start + node.size / 2, node.size / 2, node.no * 2 + 1)
        k -= 1
    used[n].append(node)
    print 'allocating [', node.start, ',', node.size, ']'
    return node

def mfree(node):
    print 'freeing [', node.start, ',', node.size, ']'
    n = log(node.size)
    used[n].remove(node)
    while True:
        pair = None
        for x in free[n]:
            if (x.no == node.no ^ 1):
                pair = x
                break
        if (pair == None):
            break
        free[n].remove(pair)
        node.start = min(node.start, pair.start)
        node.size *= 2
        node.no /= 2
        n += 1
    free[n].append(node)

def print_alloc():
    print 'printing free memory blocks'
    for i in xrange(0, 21):
        for x in free[i]:
            print '[', x.start, ',', x.size, ']'
    print

for i in xrange(0, 21):
    free.append([])
    used.append([])
free[SIZE].append(Node(0, 2**SIZE, 1))
x = malloc(123)
print_alloc()
y = malloc(1432)
print_alloc()
z = malloc(24320)
print_alloc()
mfree(y)
print_alloc()
mfree(x)
print_alloc()
mfree(z)
print_alloc()
```


```
如何表示空闲块？ 如何表示空闲块列表？ 
[(start0, size0),(start1,size1)...]
在一次malloc后，如果根据某种顺序查找符合malloc要求的空闲块？如何把一个空闲块改变成另外一个空闲块，或消除这个空闲块？如何更新空闲块列表？
在一次free后，如何把已使用块转变成空闲块，并按照某种顺序（起始地址，块大小）插入到空闲块列表中？考虑需要合并相邻空闲块，形成更大的空闲块？
如果考虑地址对齐（比如按照4字节对齐），应该如何设计？
如果考虑空闲/使用块列表组织中有部分元数据，比如表示链接信息，如何给malloc返回有效可用的空闲块地址而不破坏
元数据信息？
伙伴分配器的一个极简实现
http://coolshell.cn/tag/buddy
```

--- 

## 扩展思考题

阅读[slab分配算法](http://en.wikipedia.org/wiki/Slab_allocation)，尝试在应用程序中实现slab分配算法，给出设计方案和测试用例。

## “连续内存分配”与视频相关的课堂练习

### 5.1 计算机体系结构和内存层次
MMU的工作机理？
 通过查找页表中的页表项将虚拟地址转换为物理地址
- [x]  

>  http://en.wikipedia.org/wiki/Memory_management_unit

L1和L2高速缓存有什么区别？
L1缓存在CPU内部，速度和CPU一样；L2缓存在CPU外部，但一般和CPU集成在一起，速度比L1慢，但仍比内存快
- [x]  

>  http://superuser.com/questions/196143/where-exactly-l1-l2-and-l3-caches-located-in-computer
>  Where exactly L1, L2 and L3 Caches located in computer?

>  http://en.wikipedia.org/wiki/CPU_cache
>  CPU cache

### 5.2 地址空间和地址生成
编译、链接和加载的过程了解？

- [x]  

>  

动态链接如何使用？

- [x]  

>  


### 5.3 连续内存分配
什么是内碎片、外碎片？

- [x]  

>  

为什么最先匹配会越用越慢？

- [x]  

>  

为什么最差匹配会的外碎片少？

- [x]  

>  

在几种算法中分区释放后的合并处理如何做？

- [x]  

>  

### 5.4 碎片整理
一个处于等待状态的进程被对换到外存（对换等待状态）后，等待事件出现了。操作系统需要如何响应？

- [x]  

>  

### 5.5 伙伴系统
伙伴系统的空闲块如何组织？

- [x]  

>  

伙伴系统的内存分配流程？

- [x]  

>  

伙伴系统的内存回收流程？

- [x]  

>  

struct list_entry是如何把数据元素组织成链表的？

- [x]  

>  



