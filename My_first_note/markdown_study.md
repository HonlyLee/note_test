# Markdown语法的学习
## 一、文字修饰类
*文字* 
**文字**
***文字***
<u>文字</u>
==文字==
==*文字*==
***
>一对”*“号是倾斜，两对是加粗，三对是倾斜加粗`<u></u>`，两对=号是高亮

## 二、注释类语法
* **解释框**
> 如同这个用'>'符号

* **单行代码框**

`cout << "hello world";`
>用一对反单引号``括起来即可

* **多行代码框**

```c++
#include <iostream>
int main()
{
   std::cout << "nb" << endl;

    return 0;
}

```

*使用三个反引号括起即可*

## **三、分隔符及列表**
**分隔符**
***
>如上使用三个*号就有分割线

**列表**
* 收到撒啊

1. 目录
   * 社保卡
2. 呵呵呵

>一个*号（后面要跟一个空格）代表无序列表，数字+.是有序列表，列表之间使用Tab键可嵌套

## **四、跳转链接类**
比如说我这段话[^1]

[^1]:就是我想说的东西

>[]号中再加上\^号再加个标识符，具体注释用\[\^**标识符**]:==解释语句==

## **五、链接（图片链接）**

* **普通链接**

这是一个链接[点我](www.baidu.com)

或者<https://www.google.com>

[链接][标识]

[标识]:https://www.runoob.com/markdown/md-link.html

><u>语法为：==[链接名]后面直接跟(链接地址)==</u>或者  ==<链接地址>== 直接显示网址链接

---
* ==链接地址可为文件中***标题链接***==

eg:请参照[标题一](#一文字修饰类)
即可跳转到标题

>只用将括号中的地址换为 ==#+*标题名*==（不论几级标题）



* **图片链接**
![图片](/photos/99.png)
> 语法为 ==！+[] (图片地址)==


##**六、其他**
* 关于==关键字==的显示可用<code><mark>\<code></mark>标签和<mark>\\</mark></code>配合使用
高亮还能用标签\<mark>表示
<code>==\<code>== 标签和 ==\\==</code>