# vector_insert_delete

### 插入

> **C++11 针对顺序容器引入了三个新的成员函数**

* emplace_front（对应之前的 push_front）
* emplace（对应之前的 insert）
* emplace_back（对应之前的 push_back）



> **默认从容器头部插入**

* **`push_front`**
* **`emplace_front`**（c++11）



> **默认从容器末尾插入**

* **`push_back`**
* **`emplace_back`**（c++11）



> **从容器指定位置插入**

* **`insert`**

* **`emplace`**（c++11）

  1. 函数原型

     ```c++
     template< class... Args >
     iterator emplace( const_iterator pos, Args&&... args );
     // 参数 pos：在该位置（迭代器）前插入元素
     // 参数 args：



> **插入后的 size 如果超过了 capacity 会发生什么？**



> **拷贝还是构造？**

* emplace 是构造
* push_back 是拷贝
* insert 是拷贝

```c++
class A
{
public:
    A(std::string str) : s(str) {std::cout<<"构造"<<std::endl;}
    A(const A& obj) : s(obj.s) {std::cout<<"拷贝构造"<<std::endl;}
    A(A&& obj) : s(std::move(obj.s)) {std::cout<<"移动构造"<<std::endl;}
    
    A& operator=(const A& obj)
    {
        s = obj.s;
        std::cout<<"拷贝赋值运算符"<<std::endl;
        return *this;
    }
    
    A& operator=(A&& obj)
    {
        s = std::move(obj.s);
        std::cout<<"移动赋值运算符"<<std::endl;
        return &this;
    }
private:
    std::string s;
};

int main()
{
    std::vector<A> container;
    
    return 0;
}
```



### 删除

* erase
* pop_back
* 