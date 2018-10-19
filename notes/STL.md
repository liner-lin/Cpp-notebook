# STL与泛型编程

## STL通用算法
+ sort(iterator begin, iterator end) : 对象必须重载operator<()函数。
+ for_each()
    ```c++
    for (vector<Review>::iterator pr = books.begin(); pr != books.end(); pr++)
        ShowReview(*pr);

    //等同于：
    for_each(books.begin(), books.end(), ShowReview);
    ```
+ random_shuffle(iterator begin, iterator end) : 随机排序。

## 模板类vector ：动态内存分配
```c++
template <class T, class Allocator = allocator<T>>
class vector {
    ...
};
```
+ 构造函数：vector<T>(const int size);

+ 成员函数：
    - size()
    - swap()
    - begin()
    - end()
    - push_back()
    - erase(iterator begin, iterator end) : 删除区间[begin， end)的元素。
    - insert(iterator location, iterator begin, iterator end)

+ 迭代器：vector<T>::iterator it; 

## 泛型编程
        面向算法编程，而不关注数据结构。迭代器使得面向算法编程成为可能。

## 容器的基本特征
+ X::iterator
+ X::value_type    ：    T
+ X u
+ X()
+ X u(a)
+ X u = a
+ r = a
+ a.begin()
+ a.end()
+ a.size()
+ a.swap(b)
+ a == b
+ a != b
  
## 序列的基本特征

    元素按待定顺序排序，两个遍历，顺序一致。

+ X a(n, t)  : n个t值的序列
+ X(n, t)
+ X a(i, j)  : 初始化区间[i, j)，i, j为X同类型的序列容器的迭代器。
+ X(i, j)
+ a.insert(p, t)  : 将t插入到p的前面
+ a.insert(p, n, t)
+ a.insert(p, i, j)
+ a.erase(p)
+ a.erase(p, q)
+ a.clear()
+ T& a.front()   :  *a.begin()
+ T& a.back() : *--a.end()
+ a.push_front(t):a.insert(a.begin(), t)
+ a.push_back(t):a.insert(a.end, t)
+ a.pop_front(t):a.erase(a.begin())
+ a.pop_back(t):a.erase(--a.end())
+ T& a[n]:*(a.begin()+n)
+ T& a.at(n):*(a.begin()+n)

## STL七种序列容器
+ deque ：双向队列
+ list ： 双向链表，可反转。
    - void merge(list<T, Alloc>& x)：两个链表必须已排序，合并后，x为空。
    - void remove(const T& val)
    - void sort()
    - void splice(iterator pos, list<T, Alloc> x)
    - void unique()：将连续相同的元素压缩为单个元素。（注连续）
+ queue
    - bool empty() const
    - size_type size() const
    - T& front()
    - T& back()
    - void push(const T& x)
    - void pop()
+ priority_queue：优先队列，需要再构造函数中，传进一个函数对象。
+ stack
    - bool empty() const
    - size_type size() const
    - T& top()
    - void push(const T& x)
    - void pop()
+ vector ：矢量
    - rbegin()和rend() : 支持反向遍历元素。
+ forward_list：单向链表，C++11增加。
+ array：C++11增加，非STL标准
  
## STL四种关联容器 : 底层是树结构
+ set
+ multiset
+ map
+ multimap

## 无序关联容器（C++11)：哈希表
+ unordered_set
+ unordered_multiset
+ unordered_map
+ unordered_multimap

## 函数对象
重载了()运算符的对象。

+ for_each() :
  ```c++
  template<class InputIterator, class Function>
  Function for_each(InputIterator first, InputIterator last, Function f);
  ```
  每个迭代器都重载了for_each()。

## initialize_list : C++11初始化列表
```c++
std::vector<int> val{1, 2, 3, 4};
```