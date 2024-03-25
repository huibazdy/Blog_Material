# RAII

> RAII

**RAII** 的全称是**资源获取即初始化**（**Resource Acquisition Is Initialization，RAII**）。**Bjarne** 称它为使用局部对象来管理资源的技术。因为局部对象存储在栈中，所以其生命周期由操作系统管理，无需人为介入。它的提出是防止程序员忘记销毁资源而导致的资源浪费或内存泄漏等问题。



> RAII 实现步骤

1. 设计一个类封装资源（内存、文件、socket、锁等）
2. 构造函数中初始化资源（申请内存、打开文件、申请锁等）
3. 析构函数中销毁资源（释放内存、关闭文件、释放锁等）
4. 使用该类对象，在希望用到的作用域内声明即可，如：函数开始处或作为类的成员变量



> RAII 实现文件句柄封装

```c++
#include<iostream>
#include<fstream>

class File
{
public:
    //构造函数
    File(const char* filename):m_handle(std::ifstream(filename)) {}
    //析构函数
    ~File() {
        if(m_handle.is_open()) {
            std::cout<<"File is closed."<<std::endl;
            m_handle.close(); // 关闭文件，释放句柄
        }
    }
    // 获取文件句柄的函数
    std::ifstream& getHandle() {
        return m_handle;
    }
private:
    std::ifstream m_handle;   // 文件句柄
};

int main()
{
    File file1("111.txt");
    if(file1.getHandle().is_open()) {
        std::cout<<"File is opened."<<std::endl;
    }
    else
        std::cout<<"Failed to open the file. "<<std::endl;
    return 0;
}
```



> RAII 实现 mutex 锁的封装

包装 mutex 在多线程场景安全锁定和解锁互斥量，实现线程同步。



```c++
#include <iostream>
#include <mutex>
#include <thread>


```







## 参考资料

1. [C++ RAII 思想](https://csguide.cn/cpp/memory/raii_in_cpp.html#%E7%A4%BA%E4%BE%8B)