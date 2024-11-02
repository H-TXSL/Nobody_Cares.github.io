# 从零开始的STL生活
> 参考[cppreference](https://zh.cppreference.com/w/%E9%A6%96%E9%A1%B5)
# 目录
> - 序列
> [array](#array)
> [vector](#vector)
> [迭代器图示](#迭代器图示)
## array
> 头文件 `#include <array>`
***
> - 成员函数
>   - 成员访问
> [at 带越界访问检查](#arr1)
> [operator[] 访问指定元素, 无边界检查](#arr2)
> [front 访问第一个元素](#arr3)
> [back 访问最后一个元素](#arr4)
> [data 直接访问底层连续存储](#arr5)
>   - 迭代器
> [迭代器](#arr6)
>   - 容量
> [empty 检查容器是否为空](#arr7)
> [size 返回元素数](#arr8)
> [max_size 返回可容纳的最大元素数](#arr9)
>   - 操作
> [fill 以指定值填充容器](#arr10)
> [swap 交换内容](#arr11)
> - 非成员函数
> [get(std::array) 访问array的一个元素](#arr12)
> [std::swap(std::array) 特化std::swap算法](#arr13)
> [std::to_array 从内建数组创建std::array对象](#arr14)
> - 辅助类
> [std::tuple_size\<std::array>](#arr15)
> [std::tuple_element\<std::array>](#arr16)
***
- 成员访问
<a name="arr1"></a>
at 带越界访问检查
```c++
std::array<int, 6> arr{1, 2, 3, 4, 5, 6};
// 设置元素
arr.at(1) = 10;
// 访问元素
std::cout << arr.at(1) << std::endl; // 输出 10
// 越界则抛出 std::out_of_range 类型的异常
 try {
    arr.at(10) = 100;
  } catch (const std::out_of_range& ex) {
    std::cout << ex.what() << std::endl; 
  }
```
<a name="arr2"></a>
operator[] 访问指定元素, 无边界检查
```c++
std::array<int, 6> arr{1, 2, 3, 4, 5, 6};
// 设置元素
arr[1] = 10;
// 访问元素
std::cout << arr[1] << std::endl; // 输出 10
```

<a name="arr3"></a>
front 访问第一个元素
```c++
std::array<int, 6> arr{1, 2, 3, 4, 5, 6};
// 访问第一个元素
std::cout << arr.front() << std::endl; // 输出 1
```

<a name="arr4"></a>
back 访问最后一个元素
```c++
std::array<int, 6> arr{1, 2, 3, 4, 5, 6};
// 访问最后一个元素
std::cout << arr.back() << std::endl; // 输出 6
```

<a name="arr5"></a>
data 直接访问底层连续存储
```c++
std::array<int, 5> arr{1, 2, 3, 4, 5};
// 返回一个指向底层连续存储的指针
// 使得范围[data(), data() + size()]始终为有效范围
  int* p = arr.data();
  for (int i = 0; i < arr.size(); i++)
  {
    std::cout << *(p + i) << " ";
  }
  std::cout << std::endl;
```
- 迭代器
<a name="arr6"></a>
begin 指向起始位置的迭代器 
end 指向末元素后一个位置的迭代器
rbegin 指向末元素的迭代器
rend 指向头元素前一个位置的迭代器
> cbegin cend crbegin crend 为常量迭代器
```c++
  std::array<int, 5> arr{1, 2, 3, 4, 5};
  // 正向迭代器
  for (auto it = arr.begin(); it != arr.end(); it++)
  {
    std::cout << *it << " ";
    // 1 2 3 4 5 
  }
  std::cout << std::endl;
  // 反向迭代器
  for (auto it = arr.rend() - 1; it != arr.rbegin() - 1; it--)
  {
    std::cout << *it << " ";
    // 1 2 3 4 5 
  }
  std::cout << std::endl;
```
- 容量
<a name="arr7"></a>
empty 检查容器是否为空
```c++
  std::array<int, 5> arr{1, 2, 3, 4, 5};
  若容器为空则为 true，否则为 false
  std::cout << std::boolalpha << "arr.empty() : " << arr.empty() << std::endl;
  // arr.empty() : false
```
<a name="arr8"></a>
size 返回元素数
```c++
  std::array<int, 5> arr{1, 2, 3, 4, 5};
  std::cout << "arr.size() : " << arr.size() << std::endl;
  // arr.size() : 5
```
<a name="arr9"></a>
max_size 返回可容纳的最大元素数
```c++
  std::array<int, 5> arr{1, 2, 3, 4, 5};
  // 因为每个 std::array<T, N> 都是固定大小容器，故 max_size 返回的值等于 N（亦为 size() 所返回的值）。
  std::cout << "arr.max_size() : " << arr.max_size() << std::endl;
  // arr.max_size() : 5
```
- 操作
<a name="arr10"></a>
fill 以指定值填充容器
```c++
  std::array<int, 5> arr{1, 2, 3, 4, 5};
  arr.fill(10);
  for (auto it = arr.begin(); it!= arr.end(); it++)
  {
    std::cout << *it << " ";
    // 10 10 10 10 10
  }
  std::cout << std::endl;
```
<a name="arr11"></a>
swap 交换内容
```c++
  std::array<int, 5> arr1{1, 2, 3, 4, 5};
  std::array<int, 5> arr2{10, 20, 30, 40, 50};
  arr1.swap(arr2);
  for (auto it = arr1.begin(); it!= arr1.end(); it++)
  {
    std::cout << *it << " ";
    // 10 20 30 40 50
  }
  std::cout << std::endl;
  for (auto it = arr2.begin(); it!= arr2.end(); it++)
  {
    std::cout << *it << " ";
    // 1 2 3 4 5
  }
  std::cout << std::endl;
```
- 非成员函数
<a name="arr12"></a>
get(std::array) 访问array的一个元素
```c++
  std::array<int, 5> arr{1, 2, 3, 4, 5};
  // 设置值
  // get返回值为引用
  std::get<0>(arr) = 10;
  // 访问值
  std::cout << std::get<0>(arr) << std::endl; // 10
```
<a name="arr13"></a>
std::swap(std::array) 特化std::swap算法
```c++
  std::array<int, 5> arr1{1, 2, 3, 4, 5};
  std::array<int, 5> arr2{10, 20, 30, 40, 50};
  std::swap(arr1, arr2);
  for (auto it = arr1.begin(); it!= arr1.end(); it++)
  {
    std::cout << *it << " ";
    // 10 20 30 40 50
  }
  std::cout << std::endl;
  for (auto it = arr2.begin(); it!= arr2.end(); it++)
  {
    std::cout << *it << " ";
    // 1 2 3 4 5
  }
  std::cout << std::endl;
```
<a name="arr14"></a>
to_array 从内建数组创建std::array对象
`C++20支持`
- 辅助类
<a name="arr15"></a>
std::tuple_size\<std::array> 提供作为编译时常量表达式访问 std::array 中元素数量的方法
<a name="arr16"></a>
std::tuple_element\<std::array> 使用 tuple 式接口，提供 array 元素类型的编译时索引访问