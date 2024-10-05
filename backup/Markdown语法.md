# Markdown语言
+ 提示: 适用与Github上的Markdown文本编辑
+ 在Github中的Markdown编辑器中,可以使用以下三种不同的语法在代码块中创建图表关系图：mermaid、geoJSON 和 topoJSON、ASCII STL.
[关于图表关系图请在此处查询](https://docs.github.com/zh/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams)
+ 在Github中的Markdown编辑器中支持LaTeX语法显示数学表达式.
[关于LaTeX语法请在此处查询](https://docs.github.com/zh/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
## 标题
- 创建标题
- 最大6个层次结构的标题
```Markdown
# 标题一
## 标题二
### 标题三
......
###### 标题六
```
# 标题一
## 标题二
### 标题三
......
###### 标题六
***
<a id="set1"></a>

## 设置文本样式
| 语法 | 例子 | 输出 | 
| :--: | :--: | :--: |
| ** **或者__ __ | `**粗体**` | **粗体** |
| * *或者_ _ | `*斜体*` | *斜体* |
| ~~ ~~ | `~~删除线~~` | ~~删除线~~ |
| ** ** 和 * * | `**粗体*斜体*字**` | **粗体*斜体*字**(粗体嵌套斜体) |
| * * 和 ** ** | `*斜体**粗体**字*` | *斜体**粗体**字*(斜体嵌套粗体) |
| *** *** | `***全部粗体加斜体***` | ***全部粗体加斜体*** |
| `<sub> </sub>` | 这是一个`<sub>下标</sub>` | 这是一个<sub>下标</sub> |
| `<sup> </sup>` | 这是一个`<sup>上标</sup>` | 这是一个<sup>上标</sup> |
## 引用文字
- 引用的文本是缩进的,会具有不同字体颜色
```Markdown
这是一个引用文本
> 这是一个引用文本
>> 多重引用
>>> ...
```
这是一个引用文本
> 这是一个引用文本
>> 多重引用
>>> ....
## 引用代码
- 用多个反引号可以区分嵌套的代码 -> 在隔离代码块中显示三个反引号,用四个反引号包裹
1. 单行引用 -> 由单个反引号连接首尾
```Markdown
这是一个`单行引用`.
```
这是一个`单行引用`.
2. 多行引用 -> 由三个反引号连接首尾
- 可以在代码块中增添语言标识符以启用语法高亮
````Markdown
以下为多行引用:
```c++
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello World!"<<endl;
    return 0;
}
```
````
以下为多行引用:

```c++
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello World!"<<endl;
    return 0;
}
```
## 链接
- 链接的文本是蓝色的,可以点击跳转
```Markdown
// 内联式链接 -> [链接文本](链接地址)
[个人博客](https://h-txsl.github.io/Nobody_Cares.github.io/)
// 引用式链接 -> [链接文本][链接标识符]
// 在文档结尾处添加链接标识符
// 链接标识符可以是任意字符串
[个人博客][blog]

[blog]: https://h-txsl.github.io/Nobody_Cares.github.io/
```
[个人博客](https://h-txsl.github.io/Nobody_Cares.github.io/)
[个人博客][blog]
## Markdown文档内部跳转
```Markdown
// 标题跳转
// 跳转至设置文本样式
[设置文本样式](#设置文本样式)

// 自定义锚点跳转
// 使用HTML的锚点标签<a>和id属性来实现文档内部跳转
<a id="自定义标识"></a>
// 跳转至设置文本样式

[自定义锚点跳转](#set1)

// 由于在设置文本样式处设置了锚点,所以可以直接跳转
// <a id="set1"></a>
```
[设置文本样式](#设置文本样式)
[自定义锚点跳转](#set1)
- 图片链接
>通过添加 ! 并 将 alt 文本用 [ ] 括起来，可显示图像。 替换文字是等效于图像中信息的短文本。 然后将图像的链接用括号 () 括起来。
>
```Markdown
![头像](https://avatars.githubusercontent.com/u/110390930?u=e650bc80688d9b64f5c5dd69d6cf9e822186493e&v=4)
```
![头像](https://avatars.githubusercontent.com/u/110390930?u=e650bc80688d9b64f5c5dd69d6cf9e822186493e&v=4)

## 列表
- 无序列表
```Markdown
// 无序列表使用-或+或*作为列表标记
- 列表项一

// 有序列表使用数字和.作为列表标记
1. 列表项一
2. 列表项二
3. 列表项三
// 列表可以嵌套

// 任务列表
- [x] 已完成任务
- [ ] 未完成任务

```
- 列表项一
1. 列表项一
2. 列表项二
3. 列表项三  
- [x] 已完成任务
- [ ] 未完成任务

## 脚注
- 脚注是对文本的补充说明
>Markdown 中脚注的位置不会影响该脚注的呈现位置。 您可以在引用脚注后立即写脚注，脚注仍将呈现在 Markdown 的底部

```Markdown
这是一段文本[^1]
[^1]: 这是一段脚注
```
这是一段文本[^1]
## 表格
- 表格两端的管道是可选的
```Markdown
// 使用|来分隔列
// 使用:来设置对齐方式
| 左对齐 | 居中对齐 | 右对齐 |
| :-- | :--: | --: |
| 表头一 | 表头二 | 表头三 |
| 内容一 | 内容二 | 内容三三三 |
| 内 | 内容五五五五五 | 内容六六六六 |
```
| 左对齐 | 居中对齐 | 右对齐 |
| :-- | :--: | --: |
| 表头一 | 表头二 | 表头三 |
| 内容一 | 内容二 | 内容三三三 |
| 内 | 内容五五五五五 | 内容六六六六 |
## 警报信息
- 在 GitHub 上，它们以独特的颜色和图标显示，以指示内容的显著性
- 警报无法嵌套在其他元素中
```Markdown
> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.
```
以下为呈现的警报:
> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.
## 创建折叠信息
- 折叠信息可以折叠显示
- 注意空格的使用
````Markdown
<details>
<summary>折叠信息</summary>

这是一段折叠信息

```c++
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello World!"
    return 0;
}
```

</details>
````
<details>
<summary>折叠信息</summary>

这是一段折叠信息

```c++
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello World!"
    return 0;
}
```

</details>

> [!CAUTION]
> 此适用于GitHub的Markdown语法文档不完整
> 更多的语法请参考[官方文档](https://docs.github.com/zh/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

[blog]: https://h-txsl.github.io/Nobody_Cares.github.io/
[^1]: 这是一段脚注