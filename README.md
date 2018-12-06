# 数据结构与算法
# 为什么学习数据结构与算法

# 如何学习——抓重点

### 数据结构同算法的关系

数据结构与算法相辅相成，数据结构为算法服务的，算法要在特定的数据结构之上，两者无法孤立。

数据结构是静态的，是数据组织、存储的一种方式。

### 重点

* **时间及空间复杂度分析**
* 数据结构：堆、栈、数组、链表、队列、散列表、二叉树、跳表、图、Trie树
* 算法：递归、排序、二分查找、搜索、哈希算法、贪心算法、分治算法、回溯算法、动态规则、字符串匹配算法

### 学习方法

* **学习来历，自身特点，适合解决的问题及实际的应用场景**
* **适度刷题，边学边练**
* 多思考，多互动
* 打怪升级法，设定小目标，多发朋友圈，让大家监督
* 知识需要沉淀，不要试图一下子掌握所有，要反复迭代，不断沉淀
* 不要只抓住一点，一直看，耗费太多时间，先整体过一遍，有个整体的印象，再细看。

# 复杂度分析

### 是什么

时间复杂度分析包括**时间复杂度**和**空间复杂度**

**时间复杂度**:随着数据规模n的增大，执行方法所消耗的时间的函数。

**空间复杂度**：随着数据规模n的增大，执行方法所占用的空间的函数关系式。

复杂度分析：是一种粗略的分析，主要看的是趋势，**渐进复杂度分析**

### 为什么

* 事后统计虽然准确，受限制太多，不一定具备环境
* 测试结果十分依赖测试环境，同电脑配置紧密相关
* 测试结果受数据规模影响很大，不同的量级的n,执行结果可能完全不一样

### 大O复杂度表示法

* unit_time 每行代码执行的时间
* 忽略常量，低阶、系数忽略，n无限大时对增长趋势的变化影响很小，可以忽略不记
* 只关注代码执行次数最多的几行代码即可，对增长影响最大
* **加法法则**: 总复杂度等于两级最大的那段代码的复杂度
* **乘法法则：**嵌套代码的复杂度为嵌套内外代码复杂度的乘积
* 如果受多个参数影响 m,n，因为m,n的大小关系不确定，O（m+n）

### O(1)

```:zap:
 int i = 8;
 int j = 6;
 int sum = i + j;
```

代码执行时间不随n增大，不管多少行代码，复杂度都是O(1)

### O(n)

```:zzz:
int sum_1 = 0;
int p = 1;
for (; p < n; ++p) {
	sum_1 = sum_1 + p;       // n
}
```

* t表示unit_time
* 前两行2t,循环部分2nt
* 假设t是固定的，fn(2+2n),n增加很大时，常量和系数影响可以忽略，所以是 O(n)

### O(n<sup>2</sup>)

```:new_zealand:
int cal(int n) {
   int ret = 0; 
   int i = 1;
   for (; i < n; ++i) {
     ret = ret + f(i);      O(n) 
   } 
 } 
 
 int f(int n) {        //O(n)
  int sum = 0;
  int i = 1;
  for (; i < n; ++i) {
    sum = sum + i;
  } 
  return sum;
 }
```

* 外层O(n)
* 外层每执行一次，内层就执行n次  O(n)
* 总共执行n<sup>2</sup>次
* 嵌套循环 乘法法则 O(n<sup>2</sup>)=T1(n)*T2(n)

### O(logn)  O(nlogn)

```:zero:
 i=1;
 while (i <= n)  {
   i = i * 2;
 }
```

求循环执行多少次,根据高中数学，i 1 2 4 8...，所以是求下图中的x

![0对数计算](imgs\0对数计算.jpg)2<sup>x</sup>=n,所以执行次数x=log<sub>2</sub>n,所以时间复杂度是O(log<sub>2</sub>n) 
找规律，再看下面代码

```c#
 i=1;
 while (i <= n)  {
   i = i * 3;
 }
```

3 9 27   3<sup>x</sup>=n,所以执行次数x=log<sub>3</sub>n,
因为log<sub>3</sub>n = log<sub>3</sub>2 * log<sub>2</sub>n,忽略系数，所以时间复杂度为O(logn),执行若外层嵌套，执行n次，则为O(nlogn)

**不同复杂度随n变化的增长趋势**

![0_增长趋势对比图](imgs\0_增长趋势对比图.png)

### 查找或插入算法

```c#
// n 表示数组 array 的长度
int find(int[] array, int n, int x) {
  int i = 0;
  int pos = -1;
  for (; i < n; ++i) {
    if (array[i] == x) {
       pos = i;
       break;
    }
  }
  return pos;
}
```

### 最好时间复杂度

因为查找或插入同所在位置有很大关系，最好的情况就是第一个元素就是要查找的元素/插入的位置匹配

### 最坏时间复杂度

都遍历完数组才发现元素，或仍然没有发现，此时就是最坏时间复杂度

### 平均时间复杂度

分析所有可能的情况，n+1中，n(0,n-1及不再数组中)，每种情况的查询次数相加后除以n+1

![1_平均时间复杂度](imgs\1_平均时间复杂度.png)

再分析每种情况出现的概率，最后得出的就是平均时间复杂度。在数组中，不在数组中各1/2，出现在每个位置的概率是相同的，所以出现在每个位置的概率是 1/2n,不出现的概率是1/2,最终平均时间复杂度为O(n)

![2_平均时间复杂度](imgs\2_平均时间复杂度.png)

### 均摊时间复杂度

```c#
 // array 表示一个长度为 n 的数组
 // 代码中的 array.length 就等于 n
 int[] array = new int[n];
 int count = 0;
 
 void insert(int val) {
    if (count == array.length) {
       int sum = 0;
       for (int i = 0; i < array.length; ++i) {
          sum = sum + array[i];
       }
       array[0] = sum;
       count = 1;
    }

    array[count] = val;
    ++count;
 }
```

像数组中插入数据，有空闲位置，就直接插入O(1)，只有当count==array.length 没有空闲位置才遍历数组，O(n)

普遍复杂度都相同，只有极个别的情况下复杂度不同

出现n中情况的频率非常有规律

摊还分析法：将极端情况，分摊到普通情况下，由此计算出的时间复杂度就是均摊时间复杂度。

### 时间复杂度作业

```c#
// 全局变量，大小为 10 的数组 array，长度 len，下标 i。
int array[] = new int[10]; 
int len = 10;
int i = 0;

// 往数组中添加一个元素
void add(int element) {
   if (i >= len) { // 数组空间不够了
     // 重新申请一个 2 倍大小的数组空间
     int new_array[] = new int[len*2];
     // 把原来 array 数组中的数据依次 copy 到 new_array
     for (int j = 0; j < len; ++j) {
       new_array[j] = array[j];
     }
     // new_array 复制给 array，array 现在大小就是 2 倍 len 了
     array = new_array;
     len = 2 * len;
   }
   // 将 element 放到下标为 i 的位置，下标 i 加一
   array[i] = element;
   ++i;
}
```

* 最好时间复杂度，i<len   直接赋值，O(1)
* 最坏时间复杂度，i>=len  循环遍历arr  O(n)
* 平均时间复杂度，判断i最可能是多少 ，共0~n-1和大于n 中情况，也就是共n+1种情况。每种情况出现的概率都是一样的，所以 1\*(1/n+1)+2\*(1/n+1)+...+n\*(1/n+1)=1  所以平均时间复杂度为O(1)
* 均摊时间复杂度，前面都是O(1),最后一个是O(n),均摊到每一个，所以最终均摊时间复杂度为O(1)

# 算法书籍

* 数据结构 邓俊辉 edx 学堂在线上有视频
* 算法导论  麻省理工公开课

### 入门

* 《大话数据结构》 2天看完？！
* 《算法图解》有意思

### 面试

* 《剑只offer》 常见面试题
* 《编程珠玑》 豆瓣9分  海里数据
* 《编程之美》 Google ,Facebook大公司

### 经典大部头

* 《算法导论》
* 《算法》

### 殿堂级

* 《计算机程序设计艺术》

### 闲暇阅读

* 《算法帝国》优先
* 《数学之美》
* 《算法之美》

# 数组

### 是什么

数组是一种**线性表**数据结构，它用**一组连续的内存空间**，来存储一组具有**相同类型**的数据。

#### 线性表

数据排成一条线一样的结构，每个线性表上的数据只有向前和向后两个方向。

常见的线性表结构：数组、链表、队列、栈、

![3线性表结构](imgs\3线性表结构.png)

####  非线性表结构

常见的非线性表结构：二叉树、堆、图

![4非线性表结构](imgs\4非线性表结构.png)

#### 连续的内存空间和相同的数据类型

连续的内存空间，和相同的数据类型，每个元素所占空间大小相同，数组空间存放位置连续，所以，数组元素的的**内存地址是可以计算的**，所以数组有一个“杀手锏”的特性：**按照下标随机访问**，

有利就有弊，插入或者删除时，为了保证存储空间的连续性，需要做大量的数据搬移工作。

数组存储空间示意图：

一个 int[] a=new int[10], 假设首地址 base_address=1000,int每个元素占4个字节。

 ![](imgs\5_数组存储空间示意图.png)

数组的寻址公式为：

```c#
a[i]_address = base_address + i * data_type_size
```

### 数组和链表的区别

链表适合作插入、删除，时间复杂度O(1)

数组支持随机访问，根据下标随机访问的时间复杂度是O(1) ，但是遍历的时间复杂度是O(n),二分法的时间复杂度是O(logn)。

### 数组低效的“插入”和“删除”

插入操作：

最好时间复杂度：在末尾插入，O(1)

最坏时间复杂度：在第0个位置插入，O(n)

平均时间复杂度：(1+2+3...n)/n=O(n)

**解决** 

如果只要求在K位置插入元素，而数组中存储的结构并没有任何规律，则可以将第K个位置的元素赋值到末尾，然后将a[k]=newValue，这样时间复杂度就降为了O(1)

删除操作：

同插入类似：

最好时间复杂度：在末尾删除，O(1)

最坏事件复杂度：在第0个位置删除，O(n)

平均时间复杂度：(1+2+...n)/n=O(n)

**解决**

如果会有多次删除操作，不要每次都执行，可以将要删除的元素**标记为已删除**，最后集中删除，这样可以大大减少数据搬移次数。JAVA中JVM标记清除垃圾回收算法的核心思想就是先标记，到一定时间后，统一删除。

### 容器(ArrayList) VS 数组（Array）

ArrayList:

* 支持动态扩容，当空间不足时，自动增长1.5倍。但是扩容，涉及内存申请和数据搬移，比较耗时，如果能确定大小，还是要事先指定好。
* 无法存储基本类型，ArrayList存储的都是对象，Integer,Long，但是包装（Autoboxing）和拆封（Unboxing）都会消耗性能。
* 适合做业务开发，省时省力，损耗一丢丢性能，不会影响系统整体的性能。

Array:

* 适合存储简单的数据类型 int  string
* 适合做底层开发

### 数组下标为什么从0开始

从0开始，则寻址公式

```c#
a[k]_address = base_address + k * type_size
```

从1开始，寻址公式如下：

```c#
a[k]_address = base_address + (k-1)*type_size
```

还有就是沿用C的习惯。

### 二维数组寻址公式

二维数组也是线性排列的，m行n列的数组，计算是第多少个元素即可，行号*总列数+当前的列号即可。

```C#
int[][] a=new int[m][n]
a[i][j]=base_address+(i*n+j)*data_typeSize 
```

