

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
3. 将一个 sp 作为函数的返回值（根本原因是向函数调用者返回了一个 sp 的拷贝）；

以上情况都会使与其关联的计数器递增。



什么时候递减呢？

1. 对 sp 赋予一个新的值；
2. 局部 sp 离开它的作用域；



当 sp 计数器变为 0 ，它机会自动释放自己管理的对象



```c++
class Foo {
    ...
};

shared_ptr<Foo> func1(T arg) {
    return make_shared<Foo>(arg);
}

void use_func1(T arg) {
    shared_ptr<Foo> p = func1(arg);  // 使用 p
}                                    // p 离开其作用域，自动释放它指向的内存
```

上述例子中，释放内存的过程如下：

1. p 为局部变量，离开作用域被销毁；
2. 销毁 p 时，递减其引用计数并检查递减后是否为 0；
3. 因为 p 时唯一引用 func1 返回的内存对象，所以引用计数递减为 0 ；
4. p 指向的内存对象被释放

如果引用计数不递减为 0 ，则内存对象也不会被释放：

```c++
void use_func1(T arg) {
    shared_ptr<Foo> p = func1(arg); // p 引用计数为 1
    return p;                       // p 引用计数为 2，因为将 sp 作为返回值
}                                   // p 离开作用域被销毁，但它指向的内存不会被释放
```