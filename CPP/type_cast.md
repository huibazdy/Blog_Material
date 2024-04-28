

> C++ 目前提供了四种类型转换

* static_cast
* dynamic_cast
* const_cast
* reinterpret_cast



> 过去的类型转换与现在的类型转长啥样

* 过去

  `(type) expression`

* 现在

  `static_cast<type> expression`



【例】将一个 int 值转为 double 值

* C风格

  ```c
  int a, b;
  double res = ((double)a) / b;
  ```

* C++  风格

  ```c++
  int a, b
  double res = static_cast<double>a / b;