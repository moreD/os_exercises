# 文件系统(lec 21) spoc 思考题

## 个人思考题
### 文件系统和文件 
 1. 文件系统的功能是什么？

>  负责数据持久保存，功能是数据存储和访问

>  具体功能：文件分配、文件管理、数据可靠和安全

 1. 什么是文件？

>  文件系统中具有符号名的基本数据单位。

### 文件描述符
 1. 打开文件时，文件系统要维护哪些信息？

>  文件指针、打开文件计数、访问权限、文件位置和数据缓存

 1. 文件系统的基本数据访问单位是什么？这对文件系统有什么影响？
 1. 文件的索引访问有什么特点？如何优化索引访问的速度？

### 目录、文件别名和文件系统种类
 1. 什么是目录？

>  由文件索引项组成的特殊文件。

 1. 目录的组织结构是什么样的？

>  树结构、有向图

 1. 目录操作有哪些种类？
 1. 什么是文件别名？软链接和硬链接有什么区别？
 1. 路径遍历的流程是什么样的？如何优化路径遍历？
 1. 什么是文件挂载？
 1. 为什么会存在大量的文件类型？

### 虚拟文件系统 
 1. 虚拟文件系统的功能是什么？

>  对上对下的接口、高效访问实现

 1. 文件卷控制块、文件控制块和目录项的相互关系是什么？
 1. 可以把文件控制块放到目录项中吗？这样做有什么优缺点？


### 文件缓存和打开文件
 1. 文件缓存和页缓存有什么区别和联系？
 1. 为什么要同时维护进程的打开文件表和操作系统的打开文件表？这两个打开文件表有什么区别和联系？为什么没有线程的打开文件表？
 
### 文件分配
 1. 文件分配的三种方式是如何组织文件数据块的？各有什么特征？
 1. UFS多级索引分配是如何组织文件数据块的位置信息的？

### 空闲空间管理和冗余磁盘阵列RAID
 1. 硬盘空闲空间组织和文件分配有什么异同？
 1. RAID-0、1、4和5分别是如何组织磁盘数据块的？各有什么特征？

## 小组思考题
 1. (spoc)完成Simple File System的功能，支持应用程序的一般文件操作。具体帮助和要求信息请看[sfs-homework](https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab8/sfs-homework.md)
```
[Here](https://github.com/moreD/ucore_lab/blob/master/related_info/lab8/sfs-homework.py)
```

 1. (spoc)FAT、UFS、YAFFS、NTFS这几种文件系统中选一种，分析它的文件卷结构、目录结构、文件分配方式，以及它的变种。
  wikipedia上的文件系统列表参考
  - http://en.wikipedia.org/wiki/List_of_file_systems
  - http://en.wikipedia.org/wiki/File_system
  - http://en.wikipedia.org/wiki/List_of_file_systems

  请同学们依据自己的选择，在下面链接处回复分析结果。
  - [https://piazza.com/class/i5j09fnsl7k5x0?cid=416 FAT文件系统分析]
  - [https://piazza.com/class/i5j09fnsl7k5x0?cid=417 NTFS文件系统分析]
  - [https://piazza.com/class/i5j09fnsl7k5x0?cid=418 UFS文件系统分析]
  - [https://piazza.com/class/i5j09fnsl7k5x0?cid=419 ZFS文件系统分析]
  - [https://piazza.com/class/i5j09fnsl7k5x0?cid=420 YAFFS文件系统分析]
