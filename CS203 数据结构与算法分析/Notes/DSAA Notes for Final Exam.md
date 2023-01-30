# DSAA Notes for Final Exam

## Lecture 1 DSAA Introduction

### 重点提示

1. 算法距离：扑克排序（选择排序），理解与应用。
2. 算法思想：分而治之（猜数字），理解与应用。
3. 算法设计：迭代和递归的概念与应用，理解与应用。

### 算法 (Algorithm)

定义好的一系列步骤，用来处理可计算的问题。

- 正确性（correct output）
- 原子性（basic steps）
- 有限性（finite time）

#### Example 1: 选择排序算法（Selection Sort Algorithm）

- Input：一个含有 $n$ 个数字的数组（array） $A$。
- Output：升序（ascending order）排序后的数组 $A'$。

伪代码（pseudocode）如下：

```cpp
for (int i = 1; i <= n - 1) {
    k = i;
    for (int j = i + 1; j <= n; j++) 
        if (a[k] > a[j]) k = j;
    swap(a[i], a[k]);
}
```

​	Hint：降序（descending order）

#### Example 2: 分治算法（Divide-and-conquer Strategy）

猜数字 $X \in [1, 20]$，设当前可能区间 $[l, r]$，每次猜 $m = \left[\frac{ l + r}{ 2}\right]$，若：

- $m$ is correct，则查找成功。
- $m$ is too low，则 $l = m + 1$。
- $m$ is too large，则 $r = m - 1$。

上述算法的核心思想就是将区间分治为 $[l, m - 1], m, [m + 1, r]$ 三段。

根据提供的大小信息，可以在较少次数的判断后找到答案。

### 数据结构（Data Structures）

组织数据对象的形式，用来高效使用数据。

- 集合 Set、数组 Array、链表 Linked List、栈 Stack、队列 Queue
- 哈希表 Hash Table、堆 Heap、树 Tree ...

### 算法设计

#### 增量 / 迭代（Incremental / Iteration Technique）

依据当前的结果，尝试构建更大的结果，通常使用循环实现。

example：已经完成了 $A[1, ... i - 1]$ 的排序，增加一个元素 $A[i]$ 使得 $A[1, ..., i]$ 有序。

####  递归（Recursive Technique）

将当前的问题，尝试变成更小的子问题，通常采用自我调用的函数实现。

example：将 $A[i, ... , n]$ 的排序问题，通过找最小值放到 $A[i]$，转化成 $A[i + 1, ..., n]$ 的排序问题。

## Lecture 2 Algorithm Analysis  

### 重点提示

1. 算法分析：复杂度分析、正确性分析，理解与应用。
2. 查找算法（顺序查找、二分查找）的理解与应用。
3. 渐进表示法：大 O 表示法、大 Ω 表示法 、大 Θ 表示法，理解与应用。
4. 程序的时空复杂度，理解与应用。
5. 解决递归程序时间复杂度利器：主定理，了解与计算。

### 算法分析

#### 复杂度分析（Cost Analysis）

- Hint：在 $CS203$ 课程中，如果没有特别说，算法分析即为复杂度分析。

我们以如何实现有序数组$A[1, ... , n]$中的查找算法为例，进行程序复杂度分析：

##### 方法 1：顺序查找算法

```cpp
int i = 1;
do {
    if (A[i] == t) return true;
    i = i + 1;
} while (i <= n);
return false
```

在最坏输入的情况下，顺序查找算法需要的计算次数为 $4n + 1$ 次。

所以，此算法的最差时间（Worst-Case Running Time）是 $f(n) = 4n + 1$。

##### 方法 2：二分查找算法

```cpp
left = 1, right = n;
do {
    mid = (left + right) / 2;
    if (t == A[mid]) return true;
    else if (t < A[mid]) right = mid - 1;
    else left = mid + 1;
} while (left <= right);
return false;
```

最坏输入的情况下，二分查找需要的计算次数为 $2 + 9h$ 次，其中 $h$ 为 $2 - 7$ 行循环执行次数。

容易证明，第 $i$ 次循环时，剩余的元素最多是 $\frac{n}{2^i}$ 个，所以总次数为 $\frac{n}{2^{i}} < 1$ 得到 $h > \log_2 n$。

也就是说，当第 $h = \log_2 n + 1$ 次后，二分查找循环一定执行完毕。

最坏输入的情况下，二分查找需要的计算次数为 $2 + 9(\log_2 n+ 1)$ 次。

所以，此算法的最差时间（Worst-Case Running Time）是 $g(n) = 9 \log_2 n + 11$ 次。

##### 	分析

我们认为，算法 2 优于算法 1，这是因为输入很大时（当 $n$ 很大时），后者远远快于前者。

当输入很大时，常数因子不影响算法最差时间的增长速度。 

#### 正确性分析（Correctness Analysis）

使用数学方法表明，算法可以覆盖所有情况，输出正确结果，它在任何数据上都是成立的。

### 大 O 表示法

设 $f(n), g(n)$ 表示两个关于 $n$ 的函数，我们称 $f(n)$ 渐进（asymptotically）增长不快于 $g(n)$：

- 存在常数 $c_1 > 0$ 使得 $f(n) \leq c_1 \cdot g(n)$ 对于 $n \geq c_2$ 恒成立。

 记作：$f(n) = O(g(n))$。

#### 程序的时空复杂度

我们通常使用程序在最坏输入情况下的大 O 表示法来描述算法的时间复杂度。

上面的例子中，顺序查找算法的时间复杂度为 $f(n) = O(n)$，二分查找算法的时间复杂度为 $g(n) = O(\log_2 n)$。

程序的空间复杂度分析，与时间复杂度分析同理，通常使用程序在最坏输入情况下的大 O 表示法来描述算法的空间复杂度。

### 大 Ω 表示法 

设 $f(n), g(n)$ 表示两个关于 $n$ 的函数，我们称 $f(n)$ 渐进（asymptotically）增长不慢于 $g(n)$：

- 存在常数 $c_1 > 0$ 使得 $f(n) \geq c_1 \cdot g(n)$ 对于 $n \geq c_2$ 恒成立。

 记作：$f(n) = Ω (g(n))$。

### 大 Θ 表示法 

设 $f(n), g(n)$ 表示两个关于 $n$ 的函数，我们称 $f(n)$ 渐进（asymptotically）增长等于于 $g(n)$：

- $f(n) = O(g(n))$ 并且 $f(n) = Ω (g(n))$

 记作：$f(n) = Θ  (g(n))$。

### 主定理（Master Theorem）

递归方程 $T(n) = aT(\frac{n}{b}) + O(n^c)$，计算 $T(n)$ 的渐进复杂度。

- 当 $\log_b a < c$：$T(n) = O(n^c)$
- 当 $\log_b a = c$：$T(n) = O(n^c \log n)$
- 当 $\log_b a > c$：$T(n) = O(n^{\log_b a})$

## Lecture 3 Sorting Algorithms

### 重点提示

1. 选择排序、插入排序、冒泡排序、归并排序、快速排序的理解与应用。
2. 计数排序、基数排序、桶排序的了解。
3. 排序算法的稳定性分析。

### 选择排序（Selection Sort）

每次选择剩余数字中最小的一个，并将其放置到当前已经排序的数字的最右侧。

```cpp
for (int i = 1; i <= n - 1; i++) {
    int k = i;
    for (int j = i + 1; j <= n; j++)
        if (a[k] > a[j]) k = j;
    swap(a[i], a[k]);
}
```

时间复杂度：$O(n^2)$

### 插入排序（Insertion Sort）

考虑先已经排序好的数字序列中插入一个新数字。首先将待插入数字放置在已经排序的数字列最右侧，向左交换至正确位置。

```cpp
for (int i = 1; i <= n; i++) {
	for (int j = i; j >= 2; j--) {
		if (a[j] < a[j - 1]) 
            swap(a[j], a[j - 1]);
	    else 
            break;     
    }
}
```

时间复杂度：$O(n^2)$

### 冒泡排序（Bubble Sort）

每次考虑数字序列中相邻的每一对，若次序错误交换次序，直到有序。

```cpp
for (int i = 1; i <= n - 1; i++) {
    for (int j = 2; j <= n; j++) {
        if (a[j] < a[j - 1])
            swap(a[j], a[j - 1]);
    }
}
```

时间复杂度：$O(n^2)$

### 归并排序（Merge Sort）

使用分而治之的思想，每次将区间平均分成两部分，进行排序后归并。

```cpp
void MergeSort(int l, int r) {
    if (l == r) return;
    int mid = (l + r) / 2;
    MergeSort(l, mid);
    MergeSort(mid + 1, r);
    int p = l, q = mid + 1;
    for (int i = l; i <= r; i++)
        if ((q > r) || (p <= mid && a[p] <= a[q])) {
            t[i] = a[p];
            p = p + 1;
        } else {
            t[i] = a[q];
            q = q + 1;
        }
    for (int i = l; i <= r; i++)
    	a[i] = t[i];
}
```

时间复杂度：$T(n) = 2 T(\frac{n}{2}) + O(n) = O(n \log_2 n)$。

#### Trick：求逆序对

逆序对：$a_i > a_j$ 并且 $i < j$ 的数对 $(i, j)$。

使用归并排序可以快速求数组中的逆序对个数。

```cpp
int invPairNum = 0;
void MergeSort(int l, int r) {
    if (l == r) return;
    int mid = (l + r) / 2;
    MergeSort(l, mid);
    MergeSort(mid + 1, r);
    int p = l, q = mid + 1;
    for (int i = l; i <= r; i++)
        if ((q > r) || (p <= mid && a[p] <= a[q])) {
            t[i] = a[p];
            p = p + 1;
        } else {
            t[i] = a[q];
            q = q + 1;
            invPairNum += mid - p + 1;
        }
    for (int i = l; i <= r; i++)
    	a[i] = t[i];
}
```

归并排序将数组分成左区间和右区间分别排序，再进行合并。合并时，若右区间中选取一个数字时，则所有左区间中未选取的数字和该数字构成逆序对。

时间复杂度：$T(n) = 2 T(\frac{n}{2}) + O(n) = O(n \log_2 n)$。

### 快速排序（Quick Sort）

#### 随机算法（Randomized Algorithm）

函数 `random(x, y)` 表示在闭区间 $[x, y]$ 中等概率的选取一个整数，并返回。

在 CS203 课程中大多算法都是具有确定性（deterministic）的，无需进行随机化。

但一些算法可以是随机化的，并且效果更好，如快速排序算法。

#### 快速排序

随机在数组中选择一个元素 $p$，称之为主元（pivot）。

将数组中小于 $p$ 的数字放在 $p$ 的左边，大于等于 $p$ 的数字放在 $p$ 的右边。

递归地排序 $p$ 左侧的所有元素，递归地排序 $p$ 右侧的所有元素。

```cpp
void QuickSort(int l, int r) {
	int pos = random(l, r), val = a[pos];
	int p = l, q = r;
	for (int i = l; i <= r; i++)
		if (i != pos) {
			if (a[i] < val) {
				t[p] = a[i];
				p = p + 1;
			}
			else {
				t[q] = a[i];
				q = q - 1;
			}
		}
	t[p] = val;
	for (int i = l; i <= r; i++)
		a[i] = t[i];
	if (l <= p - 1) QuickSort(l, p - 1);
	if (p + 1 <= r) QuickSort(p + 1, r);
}
```

快速排序的最差时间复杂度为：$O(n^2)$，但是期望时间复杂度为 $O(n \log_2 n)$。

设 $X$ 为快速排序的比较次数，则快速排序的时间复杂度为$O(n + X)$，

下面证明：$E(X) = O(n \log_2 n)$：设 $e_i$ 为 $A$ 中第 $i$ 小的数字，考虑 $e_i, e_j (i \ne j)$，我们计算快速排序中将 $e_i, e_j$ 比较的期望。考虑数组中排名为 $i,j$ 之间的数字，在 $e_i, e_j$ 被选择作为主元之前被选中作为主元，此时 $e_i, e_j$ 将不会被比较。反之，$e_i, e_j$ 将被比较，概率为：$\frac{2}{j - i + 1}$。所以比较的期望次数为：$E(X) = \sum\limits_{i,j} \frac{2}{j - i + 1} = O(n \log_2 n)$。

Hint：调和级数(Harmonic series) $O(1 + \frac{1}{2} + ... + \frac{1}{n}) = O(\log_2 n)$。

相较于归并排序，快速排序虽然没有理论上的优势，但实际使用中常数较小。

### 计数排序（Counting Sort）

输入数据的数据范围为$S$，则可以使用时间复杂度为$O(|S| + n)$，空间复杂度为$O(|S|)$的计数排序。

### 基数排序（Radix Sort）

将输入数据分成 $k$ 个数位，从低位到高位分别使用桶排序。

时间复杂度为 $O(nk)$。

### 桶排序（Bucket Sort）

将输入的数组放置在有限个桶里，每个桶再递归进行排序。

时间复杂度为 $O(n + c), c = n(\log n - \log m)$，$m$ 是桶的个数。 

### 排序算法的稳定性

当数组中存在两个不同位置但值相等的数时，使用排序算法使得数字有序，并且这两个数的相对位置较排序前一样，则称该排序算法是“稳定”的。

- 常见稳定排序算法冒泡排序：冒泡排序、插入排序、归并排序、基数排序、计数排序、桶排序。
- 常见不稳定排序算法冒泡排序：堆排序、快速排序、希尔排序、选择排序。

## Lecture 4 Linked List

### 重点提示

1. 链表的定义与构建。
2. 链表的递归遍历、迭代遍历。
3. 链表的基本操作：插入、删除、查找、修改。
4. 链表各项操作的时间复杂度分析。

### 链表定义

#### 概念

有首指针，以链式节点存储的数据结构叫做链表。

![image-20230118040941047](https://raw.githubusercontent.com/Maystern/picbed/main/image-20230118040941047.png)

每个节点的构成为：项（item）、链（link），后者指向下一个节点。

特别地，链表的最后一个节点的链指向`NULL`。

#### 性质

- 链表没有固定长度，可以增加或者减少节点个数。
- 不能执行随机访问（random access），只能按顺序遍历元素。
- 与数组相比需要占更多的空间（链也需要占据空间）
- 链表则可以使用非连续内存（Not Compact）。

### 链表操作

#### 赋值操作

1. 指针 $q$ 被 $p$ 赋值：$q \leftarrow p$：

<img src="https://raw.githubusercontent.com/Maystern/picbed/main/image-20230118041722165.png" alt="image-20230118041722165" style="zoom:50%;" />

2. 指针 $q$ 被 $p$ 所指向的节点赋值：$q \leftarrow \text{next of }p$：

<img src="https://raw.githubusercontent.com/Maystern/picbed/main/image-20230118041918029.png" alt="image-20230118041918029" style="zoom: 50%;" />

3. 指针 $p$ 被 $p$ 所指向的节点赋值：$p \leftarrow \text{next of }p$：

<img src="https://raw.githubusercontent.com/Maystern/picbed/main/image-20230118041958665.png" alt="image-20230118041958665" style="zoom:50%;" />

4. $q$ 所指向的节点被 $p$ 赋值：

   情况 1：$p, q$ 不在同一链表上。

   <img src="https://raw.githubusercontent.com/Maystern/picbed/main/image-20230118042203059.png" alt="image-20230118042203059" style="zoom:50%;" />

​			情况 2：$p, q$ 在同一链表上。

<img src="https://raw.githubusercontent.com/Maystern/picbed/main/image-20230118042316725.png" alt="image-20230118042316725" style="zoom:50%;" />

5. $q$ 所指向的节点被 $p$ 所指向的节点赋值：

​				情况 1：$p, q$ 不在同一链表上。

<img src="https://raw.githubusercontent.com/Maystern/picbed/main/image-20230118042359122.png" alt="image-20230118042359122" style="zoom:50%;" />

​				情况 2：$p, q$ 在同一链表上。

<img src="https://raw.githubusercontent.com/Maystern/picbed/main/image-20230118042428795.png" alt="image-20230118042428795" style="zoom:50%;" />

​	以上操作：时间复杂度：$O(1)$，空间复杂度：$O(1)$。

#### 遍历操作（Traverse）

##### 递归遍历（Recursion）

```cpp
void traverse(node *A) {
    if (A == NULL) return;
    else {
        cout << (A -> value) << '\n';
        traverse(A -> next);
    }
}
```

时间复杂度：$O(n)$，空间复杂度：$O(1)$。

##### 迭代遍历（Iteration）

```cpp
void traverse(node *A) {
    node *trav = A;
    while (trav != NULL) {
        cout << (trav -> value) << '\n';
        trav = trav -> next;
    }
}
```

时间复杂度：$O(n)$，空间复杂度：$O(1)$。

#### 插入操作（Insert）

```cpp
node* insert(node *A, node *x, int pos) {
    int cnt = 0; node *p = A;
    while (pos - 1 > cnt) {
        p = p -> next;
        cnt = cnt + 1;
    }
    node *tmp = p -> next;
    p -> next = x;
    x -> next = tmp;
    return A;
}
```

时间复杂度：$O(n)$，空间复杂度：$O(1)$。

#### 删除操作（Delete）

```cpp
node* delete(node *A, int pos) {
    int cnt = 0; node *p = A;
    while (pos - 1 > cnt) {
        p = p -> next;
        cnt = cnt + 1;
    }
    p -> next = (p -> next) -> next;
    return A;
}
```

时间复杂度：$O(n)$，空间复杂度：$O(1)$。

#### 查找操作（Find）

```cpp
bool find(node *A, int val) {
    node *p = A;
    while (p != NULL) {
        if (x == p -> value) 
            return true;
       	p = p -> next;
    }
    return false;
}
```

时间复杂度：$O(n)$，空间复杂度：$O(1)$。

#### 修改操作（Update）

```cpp
node* update(node *A, int x, int y) {
    node *p = A;
    while (p != NULL) {
        if (x == p -> value) 
            p -> value = y;
       	p = p -> next;
    }
    return A;
}
```

时间复杂度：$O(n)$，空间复杂度：$O(1)$。

## Lecture 9 Graph

### 概念（Concepts）

#### 无向图（Undirected Graph）

无向图是 可以表示为集合对$(V, E)$，其中 $V$ 表示点集，$E$ 表示边集。其中边是指无序点对 $\{u, v\}$，表示从顶点 $u$ 与顶点 $v$ 之间的无向边。节点（node）也被叫做顶点（vertex）。

#### 有向图（Directed Graph）

无向图是 可以表示为集合对$(V, E)$，其中 $V$ 表示点集，$E$ 表示边集。其中边是指无序点对 $\{u, v\}$，表示从顶点 $u$ 到顶点 $v$ 的一条有向边。节点（node）也被叫做顶点（vertex）。

有向边 $\{u, v\}$  是 $u$ 的出边（outgoing edge），是 $v$ 的入边（incoming edge）。并且 $v$ 是 $u$ 的出边邻居（out-neighbor），$u$ 是 $v$ 的入边邻居（in-neighbor）。

#### 路径（Path）

设 $G = (V,E)$，图 $G$ 中的路径指的是节点序列$(v_1,v_2, ..., v_k)$，对于所有$i \in [1, k - 1]$, $v_i, v_{i + 1}$ 之间都有连边。

#### 环（Cycle）

设 $G = (V,E)$，图 $G$ 中的环指的是一条首尾节点相同的路径。

#### 度（Degree）

无向图中，节点 $u$ 的度指的是与 $u$ 直接相连，边的条数。

有向图中，节点 $u$ 的入度指的是 $u$ 的入边条数，节点 $u$ 的出度指的是 $u$ 的出边条数。

#### 连通图（Connected Graph）

设 $G = (V,E)$，图 $G$ 是连通的，当且仅当任意节点$u, v$，都有 $u$ 到 $v$ 的路径。

#### 树（Tree）与森林（Forest）

树指的是连通无向无环图，森林指的是一些列不相交的树。

Hint：树是特殊的森林。

#### 表示法（Representation）

##### 邻接表（Adjacency List）

对于每一个节点，使用一个链表，存储其直接相邻的节点。

空间复杂度：$O(|V| + |E|)$。

##### 邻接矩阵（Adjacency Matrix）

 构建一个 $|V| \times |V|$ 的二维数表，若 $v_i, v_j$ 之间有连边，则将矩阵 $(i,j)$ 位置置为 $1$，否则置为 $0$。

空间复杂度：$O(|V|^2)$。

### 最短路径（Shortest Path）

设 $G = (V,E)$，图 $G$ 中的路径指的是节点序列$(v_1,v_2, ..., v_k)$，对于所有$i \in [1, k - 1]$, $v_i, v_{i + 1}$ 之间都有连边，该路径的长度为 $k - 1$。

图的最短路径问题就是对于给定的 $(u,v)$ 找到最短路径。

### 单元最短路径（Single Source Shortest Path，SSSP）

