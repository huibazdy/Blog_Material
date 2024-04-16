# 友元

> 通过 `friend` 使类的非公有成员能被其他类或函数访问

1. 友元声明只能出现在类定义的内部；
2. 最好在类定义开始或结束前集中声明友元；
3. 友元函数需要再类外进行一次声明；
4. 友元的声明与类本身的声明放在同一头文件中（目的是为了友元对类的用户可见）；
5. 友元函数也可以是其他类的成员函数；
6. 友元函数能定义在类的内部（这样的函数是隐式内联的）；



> 通过两个互相关联的类 `Screen` 与 `Window_mgr` 来展示友元特性

* Screen 类

  1. 窗口内容
  2. 屏幕高
  3. 屏幕宽
  4. 光标位置

  ```c++
  class Screen
  {
  public:
      typedef std::string::size_type pos;
      
      Screen() = default;      // 默认构造函数，因为有自定义构造函数，所以此函数是必需的
      Screen(pos h, pos w, char c):height(h),width(w),contents(h*w,c) {} // 自定义构造函数
      
      char get() const {return contents[cursor];}  //读取光标处字符，定义在类内自动内联（隐式内联）
      
      inline char get(pos h,pos w) const; // 显式内联
      
      Screen &move(pos row, pos column);  // 能在之后设为内联
  private:
      pos cursor = 0;  // 光标位置
      pos height = 0;  // 窗高
      pos width = 0;   // 窗宽
      std::string contents;  // 显示的字符串内容
  };

移动光标（外部声明为inline）：

```c++
inline Screen &Screen::move(pos row, pos column)
{
    pos r = row * width;    //计算行的位置
    cursor = r + column;    //在行内将光标移动到指定的列
    return *this;           //以左值形式返回对象
}
```

读取光标处字符（类内显式声明为 inline）：

```c++
char Screen::get(pos row, pos column) const
{
    pos r = row * width;     //计算行位置
    return contents[r + c];  //返回给定字符
}
```