

> `make_shared()`

最安全的的分配和使用动态内存的方法。定义在头文件 **<memory>** 中。功能如下：

1. 在动态内存中***分配***一个对象
2. ***初始化***这个对象
3. ***返回***指向此对象的 shared_ptr



```c++
#include <memory>
#include <string>

shared_ptr<int> sp1 = make_shared<int>(42);

shared_ptr<string> sp2 = make_shared<string>(10,'9');

shared_ptr<int> sp3 = make_shared<int>();     // 不传递任何参数，就会进行值初始化

auto sp4 = make_shared<vector<string>>();     // 使用 auto 来定义 shared_ptr 对象，指向动态分配空的 vector<string>
```



> `shared_ptr` 的引用计数

进行拷贝或赋值时，每个 sp 都会记录有多少个其他 sp 指向相同的动态内存对象。例如：

```c++
auto sp1 = make_shared<int>(30);  // 此时 sp1 指向的对象只有 sp1 一个引用者
```



通过拷贝来获取另一个指向相同动态内存对象的引用者：

```c++
auto sp2(sp1);    // 此时 sp2 与 sp1 指向相同内存对象，此对象有两个引用者
```



```c++
#include <iostream>
#include <memory>

int main()
{
    auto p1 = std::make_shared<int>(30);
    std::cout<<"p1 count: "<<p1.use_count()<<std::endl;
    auto p2(p1);
    std::cout<<"p2 count: "<<p1.use_count()<<std::endl;
    std::cout<<"p1 count: "<<p1.use_count()<<std::endl;

    std::cout<<*p1<<std::endl;  // p1 解引用，打印内存对象的值
    std::cout<<*p2<<std::endl;  // p2 解引用，打印内存对象的值

    return 0;
}

```

运行结果：
<img src="https://raw.githubusercontent.com/huibazdy/TyporaPicture/main/image-20240326165504348.png" alt="image-20240326165504348" style="zoom: 50%;" />



每个 sp 都有一个与之关联的计数器，称为引用计数。无论何时拷贝一个 sp ，计数器都会递增：

1. 用一个 sp 初始化另一个 sp；
2. 将一个 sp 作为参数传递给一个函数；
3. 将一个 sp 作为函数的返回值；

以上情况都会使与其关联的计数器递增。



什么时候递减呢？

1. 对 sp 赋予一个新的值；
2. 局部 sp 离开它的作用域；



当 sp 计数器变为 0 ，它机会自动释放自己管理的对象