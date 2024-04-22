# decltype

> 其实我们已经习惯了编译器隐式进行类型推导，例如在模板（泛型）函数中：

```c++
template <typename T>
void foo(T val) {
    std::cout<<val<<std::endl;
}

int main()
{
    foo(4.32);  // 编译器帮忙隐式推导参数类型
    return 0;
}
```



从 C++11 开始，支持用户主动要求编译器进行类型推导，主要是通过 auto 与 decltype 两个关键字来实现的。



* auto 用推导变量类型
* decltype 用于推导表达式结果的类型



【例】

```c++
int a = 1;
double b = 1.4;
decltype(a+b) c = a + b;
```