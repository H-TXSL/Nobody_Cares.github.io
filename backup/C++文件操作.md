+ 所需头文件`#include <fstream>`

> 包含 fstream 类, ifstream 类, ofstream 类.  
fstream 读写
>
> ifstream 读
>
> ofstream 写
>



## 打开文件,没有此文件,则创建并打开
函数原型 `void open(const char* filename, ios_base::openmode mode);`

filename 文件名	mode 打开模式

> 常见的打开模式
>
> std::ios::in：以只读模式打开文件。
>
> std::ios::out：以只写模式打开文件。如果文件不存在，它将被创建。如果文件已存在，其内容将被清空。
>
> std::ios::app：以追加模式打开文件。数据将被写入到文件的末尾。
>
> std::ios::ate：打开文件并定位到文件末尾。
>
> std::ios::binary：以二进制模式打开文件。
>
> std::ios::trunc：如果文件已存在，其内容将被清空。
>

+ 组合模式打开文件

`myfile.open("test.txt", std::ios::in | std::ios::out | std::ios::binary);`

表示以读写二进制模式打开文件。

+ 打开模式的顺序对文件的影响

```cpp
// 在没有test.txt文件时, 
// std::ios::out会创建文件
// std::ios::in 会尝试打开一个已存在的文件

// 先指定out 后指定 in, 文件不存在时,会先创建后打开
myfile.open("test.txt", std::ios::out | std::ios::in);
// 先指定in 后指定out, 文件不存在时, 会失败
myfile2.open("test.txt", std::ios::in | std::ios::out);
// 则myfile2.is_open()返回 false
```

## 关闭文件 `myfile.close();`


## 写入操作
```cpp
    // 按行写入
    myfile << "Hello, World!" << std::endl;

    // 按字符方式写入
    char mychar = 65;
    // 写入A到Z
    while (mychar <= 90)
    {
      myfile.put(mychar);
      mychar++;
    }
    myfile << std::endl;

    char mychar2[] = "Hello, World!";
    // 写入字符串到文件
    // write(字符数组指针, 字符数)
    myfile.write(mychar2, std::strlen(mychar2));
    // string类型转const char*
    std::string mychar2 = "Hello, World!";
    myfile.write(mychar2.c_str(), mychar2.size());
    myfile << std::endl;
```

## 读取文件
```cpp
    std::fstream myfile2("test.txt", std::ios::in);
    // 逐行读取
    std::string line;
    while (std::getline(myfile2, line))
    {
      std::cout << line << std::endl;
    }


    std::string mystring;
    // 类型为 char 时,按字符读取
    // 类型为 string 时,按单词读取, 以空格为分隔符, 不读取空格和换行符
    while (myfile2 >> mystring)
    {
      std::cout << mystring << std::endl;
    }

    
    char mychar3;
    // 按字符读取, 读取空格和换行符
    while (myfile2.get(mychar3))
    {
      std::cout << mychar3 << std::endl;
    }


    // 以二进制读取文件 read 函数
    // read函数原型:
    // std::istream& read(char* s, std::streamsize n);
    std::fstream myfile3("test.txt", std::ios::in | std::ios::binary);
    // 检查是否成功打开文件
    if(!myfile3.is_open()) {
      std::cerr << "无法打开文件: " << std::strerror(errno) << std::endl;
      return 1;
    }
    // 获取文件大小
    myfile3.seekg(0, std::ios::end);
    // 返回从文件开始到当前读指针所在位置的字节数
    std::streampos fileSize = myfile3.tellg();
    // 检查文件是否为空
    if(fileSize == 0) {
      std::cerr << "文件为空" << std::endl;
      return 1;
    }
    // 重置读指针到文件开始位置
    myfile3.seekg(0, std::ios::beg);
    // 输入文件大小
    std::cout << "文件大小: " << fileSize << " 字节" << std::endl;
    // 定义缓冲区大小
    const int bufferSize = 1024;
    char buffer[bufferSize];
    // 逐块读取文件内容
    // 使用 eof() 函数检查是否到达文件末尾
    while (!myfile3.eof())
    {
      // 读取数据到缓冲区
      // 读取的字节数可能小于缓冲区大小, 因此需要使用 gcount() 获取实际读取的字节数
      myfile3.read(buffer, bufferSize);
      // 计算实际读取的字节数
      std::streamsize bytesRead = myfile3.gcount();
      // 输出缓冲区内容
      // std::cout.write(buffer, bytesRead);
      // 输出缓冲区内容
      for (int i = 0; i < bytesRead; i++)
      {
        // 以 16 进制输出
        // static_cast<int>(buffer[i]) 将 char 类型转换为 int 类型
        std::cout <<  std::hex <<  static_cast<int>(buffer[i]) << " ";
      }
      // 检查是否到达文件末尾
      if (myfile3.eof())
      {
        break;
      }
    }
    std::cout << std::endl;
```



## 文件指针
1. seekg 和 seekp
+ seekg 和 seekp 函数用于定位输入和输出文件指针的位置.
+ seekg(offset, origin) : 将输入文件指针移动到距离 origin 处后 offset 个字节的位置
+ seekp(offset, origin) : 将输出文件指针移动到距离 origin 处后offset 个字节的位置
+ std::ios::beg 表示相对于文件开头, std::ios::cur 相对于当前位置, std::ios::end 相对于文件末尾
+ 偏移量 offset 可正可负

```cpp
#include<iostream>
#include<fstream>

int main()
{
    std::fstream myfile;
    myfile.open("test.txt", std::ios::out | std::ios::in);
    myfile << "Hello World !" << std::endl;
    myfile.seekg(2, std::ios::beg);
    char mychar;
    while (myfile.get(mychar))
    {
        std::cout << mychar;
        // 输出 llo World !
    }
    myfile.close();
    return 0;
}
```

2. tellg()
+ tellg() 返回从文件开始到当前读指针所在位置的字节数
+ 返回类型 std::streampos



## 测试代码
```cpp
#include <iostream>
#include <fstream>
#include <cerrno>
#include <cstring>
#include <locale>
#include <string>

int main()
{
  std::fstream myfile;
  myfile.open("test.txt", std::ios::out);

  if (myfile.is_open()) {
    // 文件成功打开，可以进行读写操作
    // 写入数据到文件
    myfile << "Hello, World!" << std::endl;
    // 按行写入
    myfile << "Hello, World!" << std::endl;

    // 按字符方式写入
    char mychar = 65;
    // 写入A到Z
    while (mychar <= 90)
    {
      myfile.put(mychar);
      mychar++;
    }
    myfile << std::endl;

    // char mychar2[] = "Hello, World!";
    // // 写入字符串到文件
    // myfile.write(mychar2, std::strlen(mychar2));
    std::string mychar2 = "你好世界!";
    myfile.write(mychar2.c_str(), mychar2.size());
    myfile << std::endl;

  
    std::fstream myfile2("test.txt", std::ios::in);
    // // 逐行读取
    // std::string line;
    // while (std::getline(myfile2, line))
    // {
    //   std::cout << line << std::endl;
    // }


    // std::string mystring;
    // // 类型为 char 时,按字符读取
    // // 类型为 string 时,按单词读取, 以空格为分隔符, 不读取空格和换行符
    // while (myfile2 >> mystring)
    // {
    //   std::cout << mystring << std::endl;
    // }

    
    // char mychar3;
    // // 按字符读取, 读取空格和换行符
    // while (myfile2.get(mychar3))
    // {
    //   std::cout << mychar3 << std::endl;
    // }

    // 以二进制读取文件 read 函数
    // read函数原型:
    // std::istream& read(char* s, std::streamsize n);
    std::fstream myfile3("test.txt", std::ios::in | std::ios::binary);
    // 检查是否成功打开文件
    if(!myfile3.is_open()) {
      std::cerr << "无法打开文件: " << std::strerror(errno) << std::endl;
      return 1;
    }
    // 获取文件大小
    myfile3.seekg(0, std::ios::end);
    // 返回从文件开始到当前读指针所在位置的字节数
    std::streampos fileSize = myfile3.tellg();
    // 检查文件是否为空
    if(fileSize == 0) {
      std::cerr << "文件为空" << std::endl;
      return 1;
    }
    // 重置读指针到文件开始位置
    myfile3.seekg(0, std::ios::beg);
    // 输入文件大小
    std::cout << "文件大小: " << fileSize << " 字节" << std::endl;
    // 定义缓冲区大小
    const int bufferSize = 1024;
    char buffer[bufferSize];
    // 逐块读取文件内容
    // 使用 eof() 函数检查是否到达文件末尾
    while (!myfile3.eof())
    {
      // 读取数据到缓冲区
      // 读取的字节数可能小于缓冲区大小, 因此需要使用 gcount() 获取实际读取的字节数
      myfile3.read(buffer, bufferSize);
      // 计算实际读取的字节数
      std::streamsize bytesRead = myfile3.gcount();
      // 输出缓冲区内容
      // std::cout.write(buffer, bytesRead);
      // 输出缓冲区内容
      for (int i = 0; i < bytesRead; i++)
      {
        // 以 16 进制输出
        // static_cast<int>(buffer[i]) 将 char 类型转换为 int 类型
        std::cout <<  std::hex <<  static_cast<int>(buffer[i]) << " ";
      }
      // 检查是否到达文件末尾
      if (myfile3.eof())
      {
        break;
      }
    }
    std::cout << std::endl;



    std::cout << "文件成功打开" << std::endl;
  } else {
    // 文件打开失败，可能是因为文件不存在或没有权限
    std::cerr << "无法打开文件: " << std::strerror(errno) << std::endl;
  }
  // 关闭文件
  myfile.close();
  return 0;
}
```

```cpp
#include<iostream>
#include<fstream>
// ofstream 写入
// ifstream 读取,不能创建文件
// fstream 写入读取
int main() {
    char data[100];

    // 以写模式打开文件
    std::ofstream outfile;
    outfile.open("afile.dat");
    std::cout << "writing file" << std::endl;
    std::cout << "name: ";
    std::cin.getline(data, 100);

    // 向文件写入
    outfile << data << std::endl;
    std::cout << "age: ";
    std::cin >> data;
    // 刷新输入流缓冲区
    std::cin.ignore();

    // 再次向文件写入
     outfile << data << std::endl;
    // 关闭文件
    outfile.close();
    // 以读模式打开文件
    std::ifstream infile;
    infile.open("afile.dat");
    std::cout << "Reading file" << std::endl;
    infile >> data;

    // 向屏幕写入数据
    std::cout << data << std::endl;
    // 再次从文件读取数据,并显示
    infile >> data;
    std::cout << data << std::endl;
    // 关闭文件
    infile.close();
    return 0;
}
```