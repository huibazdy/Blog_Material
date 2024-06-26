# vptr & vtbl

首先引入三个类之间的继承关系：

* **基类 A**

    ```c++
    class A
    {
    public:
        virtual void vf1();
        virtual void vf2();
        void f1();
        void f2();
    private:
        int v1;
        int v2;
    };

* **B 继承 A**

    ```c++
    class B : public A
    {
    public:
                             // 默认继承虚函数 A::vf2()
        virtual void vf1();  // A::vf1() 重写为 B::vf1()
                             // 默认继承成员函数 A::f1()
        void f2();           // 成员函数 A::f2() 重写为 B::f2()
    private:
                             // 默认继承 A::v1
                             // 默认继承 A::v2
        int v1;              // B 新增数据成员 B::v3
    };
    ```

    * B 依旧有 4 个成员函数
    * B 有 3 个数据成员
    * B 中的 f2( ) 与 A 中同名 

* **C 继承 B**

    ```c++
    class C : public B
    {
    public:
                            // 默认继承 B::vf2() 即 A::vf2()
        virtual void vf1(); // B::vf1() 重写为 C::vf1()
                            // 默认继承 B::f1() 即 A::f1()
        void f2();          // B::f2() 重写为 C::f2()
    private:
                            // 默认继承 A::v1（从 B 间接继承）
                            // 默认继承 A::v2（从 B 间接继承）
                            // 默认继承 B::v1
        int v1;             // 新增 C::v1
        int v2;             // 新增 C::v2
    };
    ```
    
    

【例】指向对象的指针调用虚函数

```c++
C* p = new C;  //实例化一个 C 对象，让指针 p 指向它

```

> 父类有虚函数，子类一定有虚函数



> 只要类中有虚函数，其对象中就存在一个指向虚表（vtbl）的指针 vptr

虚指针（vptr）大小为 4 字节（32位机器）。也就是说，类对象大小就是数据成员所占空间加上 4 个字节。



> vtbl 中存放的都是函数指针，指向的是类涉及到的虚函数





> 动态绑定发生的条件，即虚机制

1. 利用指针调用
2. 调用的是虚函数
3. 向上（父类）转型

* “动态”体现在指针类型（具体指向继承体系的哪个类）来决定具体执行哪个虚函数，而不是像静态绑定那样已知被调用函数的地址。



> 关于继承与派生需要知道的基础知识

1. 派生类必须在其内部对所有需要重新定义的虚函数进行声明，需要在这样的函数之前加上**`virtual`**关键字或在形参列表后加上**`override`**关键字。
2. 基类将成员函数分为两类，一类是希望派生类进行重写（或覆盖）的函数，称为***虚函数***；另一类是希望派生类直接继承而不要进行改变的函数。
3. 基类的析构函数一般都声明为虚函数。
4. 根据引用或指针所绑定对象类型的不同，决定执行基类的函数版本还是执行某个派生类函数版本的机制称为***动态绑定***。可以理解为声明为 virtual 的函数，才有可能发生动态绑定（因为同名、重写）。

