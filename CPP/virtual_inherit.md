# 虚继承



> 使用虚继承之前



```c++
#include <iostream>
using namespace std;

class BaseL1 {     // 对象大小为 4 字节，因为只有一个数据成员，所以无需对齐
private:
    int m_data1;
};

class BaseL2A : public BaseL1 {   // 对象大小为 4 + 4 = 8 字节
private:
    int m_data2;
};

class BaseL2B : public BaseL1 {   // 对象大小为 4 + 4 = 8 字节
private:
    int m_data3;
};

class BaseL3 : public BaseL2A, public BaseL2B {   // 对象大小为 8 + 8 + 4 = 20 字节
private:
    int m_data4;
};

int main()
{
    BaseL3 a;
    cout<<sizeof(a)<<endl;   // 输出结果为 20
    return 0;
}
```



> 使用虚继承之后



```c++
#include <iostream>
using namespace std;

class BaseL1 {
private:
    int m_data1;
};

class BaseL2A : public  virtual BaseL1 {   // 虚继承，将 BaseL1 定义为 BaseL2A 的虚基类，对象大小为 8 字节
private:
    int m_data2;
};

class BaseL2B : public virtual BaseL1 {   // 虚继承，将 BaseL1 定义为 BaseL2B 的虚基类，对象大小为 8 字节
private:
    int m_data3;
};

class BaseL3 : public BaseL2A, public BaseL2B {   // 共享虚基类的同一份子对象实例，对象大小为 4 + 4 + 4 + 4 = 16
private:
    int m_data4;
};

int main()
{
    BaseL3 a;
    cout<<sizeof(a)<<endl;  
    return 0;
}
```

输出结果为：40