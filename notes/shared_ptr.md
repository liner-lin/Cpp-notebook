# 智能指针

       智能指针又名指针引用计数器，通过对指针引用计数，从而管理动态内存的方法，避免了内存泄漏等问题，也让程序员申请内存后，无需过多地关注关注内存的释放情况。  
       在头文件memory中，位于命令空间std。

## auto_ptr

## unique_ptr

## shared_ptr
```c++
shared_ptr<string> str1(new string());
```

## weak_ptr

## 区别

   + auto_ptr和unique_ptr，只能有一个智能指针是有效的，即拥有对象的所有权，auto_ptr可通过赋值运算符转移所有权，而unique_ptr不允许。
   ```c++
   auto_ptr<string> p1(new string("1234"));
   auto_ptr<string> p2;
   p2 = p1; //p1将为nullptr。
   ```
   + shared_ptr通过引用计数方式。