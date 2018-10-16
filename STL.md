# STL与泛型编程

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