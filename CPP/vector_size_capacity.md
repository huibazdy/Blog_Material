> **理解 std::vector 的 size 与 capacity**

* size：指的是 vector 中存储元素的数量
* capacity：指的是 vector 存储元素的能力，即存储元素数量上限



> **初始化**

* **默认初始化**

  ```c++
  vector<int> v1;            // capacity 为 0，size 为 0
  ```

  默认初始化的 vector 不包含任何元素，capacity 与 size 均为 0。

* **值初始化**

  ```c++
  vector<int> v2(3);         // capacity 为 3，size 为 3，v2=[0,0,0]
  ```

* **列表初始化**

  ```c++
  vector<int> v3{1,2,3,4};   // capacity 为 4，size 为 4, v3=[1,2,3,4]
  vector<int> v4={1,2,3,4};
  ```



> **基本操作**

* **插入**

  ```c++
  v3.push_back(5);           // capacity 为 8，size 为 5, v3=[1,2,3,4,5]
  ```

  因为存在内存对齐，扩容后 capacity 从 4 变为 8，capacity 扩容为之前 size 大小的两倍

* **删除**

  ```c++
  v4.pop_back();             // capacity 为 4，size 为 3, v4=[1,2,3]



> **修改容器大小（size）**

* **`resize(n)`**

  调整容器大小为 n 个元素，若 n 小于 size ，则抛弃多出的元素；若 n 大于 size 则需对添加的元素进行值初始化。注意，改大 size 超过原来的 capacity 相当于间接修改 capacity 为 n 。

  ```c++
  vector<int> v{1,2,3,4};   // capacity 为 4，size 为 4, v=[1,2,3,4] 
  v.resize(3);              // capacity 为 4，size 为 3, v=[1,2,3]
  v.resize(5);              // capacity 为 6，size 为 5, v=[1,2,3,0,0]
  ```

* **`resize(n,t)`**

  调整容器大小为 n 个元素，任何添加元素都初始化为 t 。

  ```c++
  vector<int> v{1,2,3,4};   // capacity 为 4，size 为 4, v=[1,2,3,4]
  v.resize(5,0);            // capacity 为 8，size 为 5, v=[1,2,3,4,0]



> **修改容器容量（capacity）**

* **`reserve(n)`**

  分配至少能存储 n 个元素的内存空间，可能更大。注意，只有当 n 大于当前 capacity 时调用该函数才会改变容量。

  ```c++
  vector<int> v(4);        // capacity 为 4，size 为 4, v=[0,0,0,0]
  v.reserve(3);            // capacity 为 4，size 为 4, v=[0,0,0,0]
  v.reserve(5);            // capacity 为 5，size 为 4, v=[0,0,0,0]
  ```

  如果只是单纯地使用 push_back 会无谓地翻倍 capacity，利用 reserve 增长实际需要增加的内存空间再调用 push_back 能更高效灵活地实现增长。

* **`shrink_to_fit()`**

  将 capacity 减小为和 size 相同，达到释放冗余内存的效果。

  ```c++
  vector<int> v{1,2,3,4};  // capacity 为 4，size 为 4, v=[1,2,3,4]
  v.resize(6);             // capacity 为 8，size 为 6, v=[1,2,3,4,0,0]
  v.shrink_to_fit();       // capacity 为 6，size 为 6, v=[1,2,3,4,0,0]