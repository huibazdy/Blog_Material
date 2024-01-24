# 虚函数

## 形参一致

派生类中覆盖某个继承的基类虚函数，其参数类型必须与被它覆盖的虚函数完全一致。

基类：

```c++
class A {
public:
    virtual void f1(int) const;
    virtual void f2(int,double);
};
```

派生类：

```c++
class B : public A {
public:
    void f1(int) const override;  // 正确，覆盖的函数和虚函数形参一致
    void f2(double) override;     // 错误，覆盖的函数和虚函数形参不一致
    void f2(double);              // 正确，编译器认定为独立函数 f2 
};
```

注意第三种情况，如果意图覆盖却没有保持形参一致，编译器就检查不出来错误了。所以 C++11 标准才会规定意图覆盖虚函数的情况下后面加上 **override** 关键字。



## 关于 final

当一个类中的虚函数被关键字`final`修饰时，说明这个虚函数不能在其派生类中被重写，否则会报错。

```c++
class Base     // 基类 Base
{
public:
    virtual void f1(int) final;
};

class Derived1 : public Base  // 派生类 Derived1
{
public:
    void f1(int) override;  // 编译器报错，因为在其基类中的虚函数被声明为 final，不能被覆盖
};
```

问题来了，基类中声明为 virtual 就是希望它的派生类中被重写，为什么又添加 final 不允许派生类重写呢？