# C++笔记
        本笔记《C++ Primer Plus》为主要书籍，若不解之处，可直接阅读对应的章节。两者间若有冲突，除非特别说明，否则以书中知识为准。读者若发现错误，欢迎指出，多谢。
        本笔记旨在帮忙已熟悉C++的基础上，回忆C++不常用知识点。如 if-else C++常用编程语句等，则不予说明。  
        本笔记适合已了解C++或熟悉C的程序员阅读。  

## 基础知识
1. 命名空间

    + 代码中可以直接使用cout
     ```c++
        #include <iostream> 
        using namespace std
      ```
      
    + 直接使用std::cout
    + ```c++
         using std::cout
      ```
      代码中可以直接使用cout
    + #include <iostream.h>

2. 基本输入输出
   ```c++
   #include <iostream> //包含了命名空间std
   using std::cout
   using std::cin
   using std::endl
   ```

3. 原C库头文件需要加上c字符开头，例如：
   ```c++
   #include <cmath>
   ```

4. 符号常量
   ```c++
   #include <climits>
   ```
   climits中定义了各种基本类型的符号常量取值范围。例如：INT_MAX表示2147483647

5. 初始化
   ```c++
   int variable = 5;
   int variable(5);
   int variable{5};
   int variable = {5};
   int variable[5] {1, 2, 3, 4, 5} //c++11
   ```

6. wchar_t ：宽字符类型，表示扩展字符集（Unicode）。
   ```c++
   wchar_t ch0 = L'p';            // 长度随系统而变。
   char16_t ch1 = u'q';           // 16bits
   char32_t ch2 = U'\U0000222B';  // 32bits
   ```

7. const 限定符
   ```c++
   int Mo1 = 12;
   const int Mo2 = 12;                // const data
   const int *Mo3 = &Mo1;             // const data, non-const pointer  
   int * const Mo4 = &Mo1;            // non-const data, const pointer
   const int * const Mo5 = &Mo1;      // const data, const pointer
   ```

8.  强制类型转换
   
9.  auto：将变量的类型设置成与初始值一样。
    ```c++
    auto n = 100;     // n is int
    auto x = 1.5;     // x is double
    auto y = 1.5f;    // y is float
    ```

10. 不可变类型
    ```c++
    char *ch1 = "12345";
    string ch2 = "12345";
    ```
    
11. 指针
    ```c++
    int *va1;
    double *va2;
    val++; //地址加上sizeof(int)
    va2++; //地址加上sizeof(double)
    // sizeof(val) 等于 sizeof(va2) 等于当前系统的地址总线位数/8。
    ```

12. new 与 delete
    ```c++
    int *va1 = new int; // 指向int变量
    int *vaArray = new int[10]; // 指向int数组变量。
    delete va1;
    delete [] vaArray;
    ```

13. 逗号运算符。
    ```c++
    int i = 0;
    int j = 0;
    int k = (i = 20, j = 2 * i); // k = 40
    ```
    注：先运行前面的表达式，再运行后面的表达式，最后后面的表达式结果为整个逗号运算表达式的值。

14. for循环， C++11
    ```c++
    double prices[5] = {4.1, 2.3, 5.6, 2.4, 5.5};
    for (double x : prices)
    {

    }

    for (double &x : prices)
        x = x * 0.9;
    
    for (int x : {1, 2, 3, 4, 5})
    {

    }
    ```

15. 内联函数 inline
    ```c++
    inline void function() {};
    ```

16. 默认参数
    ```c++
    void function(int a, int b = 0, int c = 1) {}; //从右向左添加默认值。
    //调用时，可忽略设置了默认值的参数。
    function(av1, av2);
    ```
    注：与函数重载的冲突，若定义以下重载函数，编译将不予编译通过。
    ```c++
    void function(int a, int b) {};
    ```
    注：两者间存在二义性。通常的做法是，若需要使用默认值，则不重载函数，以免导致二义性，或者影响代码的可读性（即使存在C++编译可以通过例子）。

17. 函数重载
    ```c++
    void fc1(int a, int c);
    void fc1(double a, int b);
    ```
    注：函数特征标以函数参数的类型排序。编译使用参数类型与函数重新组合的形式生成具体的函数名，例如：
    ```c++
    void fc1_int_int(int, int);
    void fc1_double_int(double, int);
    ```
    注：函数特征标与参数变量名、返回类型无关。

18. 函数模板
    ```c++
    template <class T>
    void function(T, T);

    // C++98后使用关键字typename
    template <typename T>
    void function(T, T);
    ```

19. 同文件管理
    ```c++
    #ifndef COORDIN_H_
    #define COORDIN_H_
    ···
    #endif
    ```

20. 存储连续性：变量声明周期，与生命周期。
    + 自动存储持续性：函数中定义的变量；以大括号为生命周期。
    + 静态存储持续性：
       - static修饰变量；整个程序运行周期。
       - thread_local，与所属线程一样长。
    + 动态存储持续性：new, malloc

21. 常理表达式
    ```c++
    const int i = 3; //是
    const int j = i + 1; //是
    const int k = function(i); //不是
    ```
    注：常用表达式使用宏替换预处理，在编译初始就完成，不占用内存空间，非常量表达式仅表面变量初始化后，不再能被修改，但需要在运行过程中才能初始化，故需要占用内存空间。

22. constexpr C++11
    + C++11允许声明constexpr类型来由编译器检验变量的值是否是一个常量表达式。声明为constexpr的必须是一个常量，并且只能用常量或者常量表达式来初始化。
    ```c++
    constexpr int i = 3;
    constexpr int j = i+1;
    constexpr int k = f(); //只有f()是一个constexpr函数时k才是一个常量表达式
    ```
    + 一般来说，若果一旦认定变量是一个常量表达式，那就把它声明为constexpr类型。尽管指针和引用都可以定义为constexpr，但是他们的初始值却受到了严格的限制。一个constexpr指针的初始值必须是nullptr或者0，或者是存储某个固定地址的对象。函数体中定义的变量并非存放在固定地址中，因此constexpr指针不可以指向这样的变量。相反的，对于所有函数体之外的对象地址是固定不变的，可以用constexpr来定义；必须明确一点，在constexpr声明中，如果定义了一个指针，限定符号constexpr仅仅对指针有效，与指针所指对象无关。

    ```c++
    const int *p = nullptr;  //p是一个指向整型常量的指针（pointer to const）
    constexpr int *p1 = nullptr; //p1是一个常量指针(const pointer)
    ```

23. 命名空间namespace与using
    命名空间可嵌套，使用如下：
    ```c++
    namespace space1 {
        double function(double n);
    }

    namespace space2 {
        double function(double n);
    }
    ```
    往某个命名空间中添加元素的方式（可在其他源文件中）：
    ```c++
    namespace space1 {
        double function(double n, int b);
    }
    ```
    注：两者间不会冲突，使用如下：
    ```c++
    double va1 = 1.0l;
    space1::function(va1);
    space2::function(va1);
    ```
    或者：
    ```c++
    using space1::function;
    function(va1);

    //错误用例：
    using space1::function;
    using space2::function; //出现冲突。
    ```
    另一种用法，将整个命名空间添加到当前命名空间中：
    ```c++
    using namespae space1；
    ```
    注：以上语句若不在某个命名空间中，则将整个space1命名空间添加到全局命名空间中。全局命名空间有且只有一个，所以不推荐。

24. 枚举类型
    ```c++
    enum egg {Small};
    enum t_shirt{Small};  //将出现冲突。

    //C++11
    enum class egg{Small};
    enum class t_shirt{Small};

    //使用
    egg::Small;
    ```

25. 空指针 C++11: nullptr

26. 定位new运算符
    ```c++
    char *buffer = new char[1024];
    Class_name *va1 = new (buffer) Class_name;
    Class_name *va2 = new (buffer + sizeof(Class_name)) Class_name;
    ...
    delete va2;
    delete va1;
    delete buffer;
    ```
    注：
      + va1、va2将分别在buffer、buffer + sizeof(Class_name)的内存地址上分配内存空间，所以第二个需要加上sizeof(Class_name)，即内存起始地址是由程序员控制的。
      + 应该先删除缓存buffer上new的对象，再删除缓存。

27. explicit：可以使用explicit修饰构造函数，关闭隐式转换。
    
28. for循环
    ```c++
    for (auto x : books)   //auto 自动适配类型
        ShowReview(x);
    
    for (auto &x : books)   //使用引用，可以修改books
        ShowReview(x);
    ```

## 类
1. 构造与析构函数
    ```c++
    class Stock 
    {
    public:
        Stock() {va1 = 0;}
        Stock(int x):va1(x){}
        ~Stock(){}
    private:
        int va1;        
    }
    ```
    注：构造函数要么没有定义（隐式构造函数），要么显示定义默认构造函数，否则默认构造函数将不可用。

2. this指针: 对this指针的修饰。
   + 如果我们设计一个成员函数时，不想让其修改成员变量，那么就应该将this指针定义为底层指针。c++定义的方式就是在函数签名后面加上const，即
   ```c++
   void func（const A& a, int b, const int* c, int* d）const;
   ```
   + 显然，上述成员函数中，a为const引用传递，不可以改变原值；b为值传递；c为const指针传递，不可改变原值；d为输出参数，可以改变原值。而该函数为const成员函数，不可以修改成员变量值。
   + 以下是const成员函数注意的几点：
      - const对象只能访问const成员函数,而非const对象可以访问任意的成员函数,包括const成员函数。
      - const对象的成员变量不可以修改。
      - mutable修饰的成员变量，在任何情况下都可以修改。也就是说，const成员函数也可以修改mutable修饰的成员变量。c++不好的地方就是mutable和friendly这样的特性，很乱。
      - const成员函数可以访问const成员变量和非const成员变量，但不能修改任何变量。
      - const成员函数只是用于非静态成员函数，不能用于静态成员函数。
      - const成员函数的const修饰不仅在函数声明中要加（包括内联函数），在类外定义出也要加。
      - 作为一种良好的编程风格，在声明一个成员函数时，若该成员函数并不对数据成员进行修改操作，应尽可能将该成员函数声明为const 成员函数。
   + const成员函数指的是不能修改this.成员变量。

3. 运算符重载
    ```c++
    class Time
    {
    public:
        Time();
        Time operator+(const Time &t) const;
    private:
        ...
    };

    Time Time::operator+(const Time &t) const
    {
        Time sum;
        ...
        return sum;
    }
    ```

4. 友元函数
    ```c++
    class Time
    {
    public:
        Time();
        Time operator+(const Time &t) const;
        Time operator*(const double x) const;
        friend Time operator*(const double x);
    private:
        ...
    };

    Time Time::operator+(const Time &t) const
    {
        Time sum;
        ...
        return sum;
    }

    Time Time::operator*(const double x) const
    {
        operator*(x, this);  //建议如此编写。
    }

    Time operator*(const double x)  //不需要域操作符::
    {
        Time result;
        ...
        return sum;
    }
    ```
    注：
    + 运算符重载将左边的操作数作为调用对象，即
        ```c++
        Time va1, va2;
        Time va3 = va1 + va2; 
        //等价于：
        Time va3 = va1.operator+(va2);
        ```
    + 友元函数不是成员函数，但和成员函数一样可以修改成员变量。
        ```c++
        Time va1;
        Time va2 = va1 * 0.3;  // 等价于：Time va2 = va1.operator*(0.3);
        Time va2 = 0.3 * va1;  // 等价于：Time va2 = operator*(0.3, va1);
        ```
    + 如上所示，乘法运算发重载需要编写友元和成员函数重载。
    + 不能使用友元重载的运算发：=, [], ->, () 原因：等于号认为左侧操作数没有进行函数重载，会根据C++规则，调用左侧操作数的构造函数。

5. 友元类

6. 友元成员函数
   
7. const, static和static const
   + const定义的常量在函数执行之后其空间会被释放，而static定义的静态常量在函数执行后不会被释放其空间。
   + static 表示的是静态的。类的静态成员函数，成员变量是和类相关的，不是和类的具体对象相关，即使没有具体的对象，也能调用类的静态成员函数，成员变量。一般的静态函数几乎就是一个全局函数，只不过它的作用域限于包含它的文件中。
   + 在c++中，static静态成员变量不能在类内部初始化。 
        ```c++
        class STATICTEST 
        {
        private:
            static int n;    
        }

        int STATICTEST::n = 3;
        ```
   + 在c++中，const常量成员变量也不能在类定义处初始化，只能通过构造函数初始化列表进行，并且必须有构造函数。
   + const数据成员只在某个对象生存期内是常量，而对于整个类而言却是可变的。因为类可以创建多个对象，不同的对象其const数据成员的值可以不同。所以不能在类声明中初始化const数据成员，因为类的对象未被创建时，编译器不知道const 数据成员的值是什么。
   + const数据成员的初始化只能在类的构造函数的初始化表中进行。要想建立在整个类中都恒定的常量，应该用类中的枚举常量来实现，或者static const。

8. 类型转换
    ```c++
    class Test 
    {
    public:
        Test(int a, double b = 0);
        Test(double x);
        Test(float x, int b);
    }

    Test t = 19.6; //调用了Test(double x);  隐式转换
    Test(19.6); 
    Test(19.6f);  //非法，
    Test(10);     //合法，
    ```
    注：只能接受一个参数的构造函数，除非后面的参数提供了默认值。  
    explicit：可以使用explicit修饰构造函数，关闭隐式转换。

9. 转换函数
    ```c++
    //operator double();
    class Test 
    {
    public:
        Test(int a, double b = 0);
        Test(double x);
        Test(float x, int b);
        operator double() const;
    }

    Test t = 19.6; //调用了Test(double x);
    Test(19.6); 
    Test(19.6f);  //非法，
    Test(10);     //合法
    double x = double(x);
    double y = (double)x;
    ```
    注：由于double(x)使用的位置（上下文）不同，所以不会被误认为是double类的构造函数。

10. 转换函数与友元造成的混乱
    ```c++

    class Test 
    {
    public:
        Test(int a, double b = 0);
        Test(double x);
        Test(float x, int b);
        operator double() const;
        Test operator+(const Test &t) const;
        friend Test operator+(const double x, const Test &t);
    }

    Test t = 19.6;
    Test t2 = 0.3 + t;  // 0.3将自动转换为Test类型，再调用运算符重载成员函数，而不是调用友元。
    ```

11. 特殊成员函数，未定义编译器提供
    + 默认构造函数：Class_name();
    + 默认析构函数：~Class_name();
    + 复制构造函数：Class_name(Class_name &);
    + 赋值运算符：Class_name & operator=(const Class_name &);
    + sdf
    注：赋值运算符可能会调用复制运算符，先提供对象的副本。

12. 构造函数中的new，应与析构函数中的delete配对。  
    注：所有构造函数都应与析构函数中的delete配对，因为析构函数只有一个。

13. 多态与虚函数virtual  
    + 只有使用virtual修饰的函数，即虚函数，可实现多态。即根据对象具体的类型，调用对应的函数。
    + 当对父类函数进行重载时，将导致父类函数不可见。

14. protected关键字：子类可见。

15. 私有继承：基类公共成员和保护成员都将成为派生类的私有成员。
16. 保护继承：基类公共成员和保护成员都将成为派生类的保护成员。

17. 虚拟继承：解决多重继承的问题。  
    例如：O继承A和B， A，B继承C，如果C中有变量成员c，则O中将继承两份。虚拟继承将解决改问题，只继承一份c变量成员。

18. 友元类
    ```c++
    class TV
    {
    public:
        friend class Remote;

    private:
        int state;
    };

    class Remote
    {
    public:
        void set_state(TV &t) {t.state = 0;}
    };
    ```
    注：声明某类为友元，则该类可直接访问私有数据。（也可将某个类的成员函数声明为友元函数。）

## IO
1. 基本输入输出
   ```c++
   #include <iostream>
   using std::cin
   using std::cout
   using std::endl

   cin >> variable; //已空格、tab、换行等为结束符。
   // 注：当variable为int类型变量时，换行符扔在输入流缓存区中，需要get()读取丢弃。
   cin.getline(charArray0, charLen); //读取一行，已换行为结束符读取size_t个字符，读取并丢弃换行字符。

   cin.get(charArray1, charLen); //不读取换行符，下一次读取需要读取丢弃换行符。
   cin.get();  //读取丢弃输入流中的换行符
   cin.get(charArray2, charLen); //读取第二行

   cin.get(charArray1, charLen).get().get(charArray2, charLen);  //等同上。
   // 注：以上函数get()读取到空行，与其他函数读取到超出charLen的行时，将设置失效位，阻断后面的输入。超出时，超出部分扔在输入流缓冲区中。

   cin.eof();  //eofbit
   cin.fail(); //failbit or eofbit

   ```

## 三、字符串
1. string : 不可变类型
   ```c++
   #include <string>
   using namespace std;
   string str1 = "123";
   string str2{"456"};
   string str3 = str1 + str2; // "123456"
   str3 += str1;  //"123456123"
   str1 = str2;   //同引用
   ```
   注：string类型本身属于不可变类型，+ 或者 += 等操作都是通过创建新的string对象，并给其赋值实现的。

   常用操作：
   ```c++
   string.size();

   ```
2. cctype ：从C中继承而来的库。
   ```c++
   #include <cctype>
   isalpha(ch); //是否字母
   isspace(ch);
   ispunct(ch); //是否标点符号
   isdigits(ch); //是否数字
   isalnum(ch); //字母或数字
   iscntrl(ch); 
   isgraph(ch); //空格之外的打印字符
   islower(ch);
   isupper(ch);
   isprint(ch); //包括空格的打印字符
   isxdigit(ch); //十六进制数字
   tolower(ch);
   toupper(ch);

## 数组类
1. vector
   ```c++
   #include <vector>
   using namespace std;
   vector<typeName> vt(n_elem); // 分配在动态内存区中，n_elem可以为变量。
   ```
2. array ：固定长度
   ```c++
   //C++11
   #include <array>
   using namespace std;
   array<typeName, n_elem> arr; // 分配在栈上，n_elem不能为变量。
   arr[index]; //不对下标进行检测。
   arr.at(index); //检测下标，抛出异常。
   ```

## 异常
```c++
throw class_name();

try {

} catch (calss_name e) {

}
```
1. 栈解退
2. 基类exception
3. C++库stdexcept中定义的异常类：
    + logic_error
    + runtime_error
    + domain_error
    + invalid_argument
    + length_error
    + out_of_bounds
    + range_error
    + overflow_error
    + underflow_error
4. bad_alloc和异常new  
   注：new失败将抛出bad_alloc异常。
5. 异常规范 （C++11弃用）
    ```c++
    void func() throw(out_of_bounds)
    {

    }
    ```
    注：函数中抛出的异常必须和规范匹配，否则则为意外异常。
6. 设置意外异常/未捕获异常处理函数
    头文件exception中的声明：
    ```c++
    typedef void (*terminate_handler)();
    terminate_handler set_terminate(terminate_handler f) throw(); //C++98
    terminate_handler set_terminate(terminate_handler f) noexcept; //C++11
    void terminate();  //C++98
    void terminate() noexcept; //C++11

## RTTI
1. dynamic_cast：是否可以安全地将对象的地址赋值给特定类型的指针，是则返回改地址，否则返回空指针。
   ```c++
   Superb *pm = dynamic_cast<Superb *>(pg);
   ```
2. typeid运算符和type_info类
   ```c++
   typeid(Superb) == typeid(pg);
   ```
3. const_cast  
   用于const类型间的转换。
4. static_cast  
   用于向上（基类），或向下（派生类）类型的转换
5. reinterpret_cast
   
