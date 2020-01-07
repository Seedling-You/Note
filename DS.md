# DS

###Sort


|            | 平均复杂度       | 最优复杂度   | 最坏复杂度        | 辅助空间    | 稳定性   |
| -------------- | ---------------- | ------------ | ----------------- | ----------- | -------- |
| Bubble Sort    | $O(n^2)$         | $O(n)$       | $O(n^2)$          | $O(1)$      | Stable   |
| Selection Sort | $O(n^2)$         | $O(n^2)$     | $O(n^2)$          | $O(1)$      | Unstable |
| Insertion Sort | $O(n^2)$         | $O(n)$       | $O(n^2)$          | $O(1)$      | Stable   |
| Shell Sort     | $O(n^{7\over6})$ | $O(n)$       | $O(n^{4\over 3})$ | $O(1)$      | Unstable |
| Heap Sort      | $O(n\log n)$     | $O(n\log n)$ | $O(n\log n)$      | $O(1)$      | Unstable |
| Merge Sort     | $O(n\log n)$     | $O(n\log n)$ | $O(n\log n)$      | $O(n)$      | Stable   |
| Quick Sort     | $O(n\log n)$     | $O(n\log n)$ | $O(n^2)$          | $O(\log n)$ | Unstable |
| Bucket Sort    | $O(n+{n^2\over k}+k)$         | $O(n)$ | $O(n^2)$ | $O(k+n)$ | Stable   |

通过交换相邻元素的排序算法需要$\Omega(n^2)$

Quick Sort 的辅助空间是递归额外使用的栈空间。

对于归并排序的总体复杂度有：
$$
T(N)=2T(N/2)+N
$$
求解后:
$$
T(N) = N+N\log N   =O(N\log N)
$$
我们总共需要的Merge Times 是$O(\log N)$, 每次Merge的时间开销大概是$O(\log N)$



### 杂项

斐波那契数列：递归：$O(2^n)$   迭代：$O(n)$, 算法：二叉树叶子数就是运行时间，等价于求解$T(n)=T(n-1)+T(n-2)$

### Tree

Nodes  = Degree + 1

### Hash Table

Hash Table Find的平均长度

| 处理办法          | 查找成功                                 | 查找失败                                   | 插入 |
| ----------------- | ---------------------------------------- | ------------------------------------------ | ----------------- |
| Separate Chaining | $1+{\lambda \over 2}$ |$\lambda + e^{-\lambda}$| 与失败相同 |
| Linear Probing    | ${1\over 2}{(1+{1\over {(1-\lambda)}})}$                                         |   ${1\over 2}{(1+{1\over {(1-\lambda)^2}})}$                                           | 与失败相同 |
| Quadratic Probing | $-{1\over \lambda}\ln(1-\lambda)$ | $1\over {1-\lambda}$ | 与失败相同 |
| Double Hashing    | $-{1\over \lambda}\ln(1-\lambda)$ | $1\over {1-\lambda}$ | 失败相同 |

Hash表的平均查找与插入时间复杂度为$O(1) $，但真正的复杂度取决于他的冲突解决方法，最坏复杂度为$ O(n)$

查找失败总是比查找成功的平均长度长

**定理**：如果hash table的长度是质数，且表至少有一半是空的，那么使用Quadratic probing 总是能插入一个新的元素。

如果这个素数的形式是4k+3，且使用probing方法是$F(i)=\pm i^2$，那么整个哈希表都可以被探测到。

$F(i)=\pm i^2$的含义是每次探测先加再减

### 程序填空题

**2015-2016秋冬期末**

![image-20200107231121880](D:\Note\DS.assets\image-20200107231121880.png)

![image-20200107231137601](D:\Note\DS.assets\image-20200107231137601.png)

![image-20200107231152382](D:\Note\DS.assets\image-20200107231152382.png)



### 函数题

**2015-2016秋冬期末**

![image-20200107231210292](D:\Note\DS.assets\image-20200107231210292.png)

![image-20200107231222800](D:\Note\DS.assets\image-20200107231222800.png)



![image-20200107231233167](D:\Note\DS.assets\image-20200107231233167.png)

不想写了，写了几遍都看错，看成写判断平衡二叉树，艹。

**2016-2017秋冬期末**



![image-20200107231418988](D:\Note\DS.assets\image-20200107231418988.png)

![image-20200107231429247](D:\Note\DS.assets\image-20200107231429247.png)

**AC代码**

~~~c
#define MAXN 128

int dfs(Tree T, int X, int *Stack, int *Sp);

int LCA(Tree T, int u, int v) {
    int stack1[MAXN];
    int stack2[MAXN];
    int sp1 = -1;
    int sp2 = -1;
    int f1 = dfs(T, u, stack1, &sp1);
    int f2 = dfs(T, v, stack2, &sp2);
    if (f1 * f2 == 0) {
        return ERROR;
    }
    int min = (sp1 - sp2 < 0) ? sp1 : sp2;
    for (int i = 0; i <min+1; ++i) {
        if (stack1[i]!=stack2[i])
        {
            return stack1[i-1];
        }
    }
    return stack1[min];


}

int dfs(Tree T, int X, int *Stack, int *Sp) {
    Tree cur = T;
    while (1) {
        if (cur == NULL) {
            return 0;
        }
        Stack[++*Sp] = cur->Key;
        if (cur->Key > X) {
            cur = cur->Left;
        } else if (cur->Key < X) {
            cur = cur->Right;
        } else {
            return 1;
        }
    }

}
~~~

