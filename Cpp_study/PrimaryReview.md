# 数据类型

## 类型修饰符

如：
* <u>signed
* unsigned </u>
* short
* long

> *注意*:一般要使用两组进行修饰时**符号修饰**要在**长度修饰**==前面==，但颠倒也不影响含义。
> eg: 
> `unsigned long int`

* 小补充：

使用头文件中标准库函数`#include <limits>`求*数据类型最大最小值*

```c++
#include <iostream>
#include <limits>
using namespace std;
int main()
{
    cout << "Hello World!\n";
    cout << "int的字节数：" << sizeof(int) << endl;
    
    cout << "int的最大值：" << (numeric_limits<int>::max)() << endl;
    cout << "int的最小值：" << (numeric_limits<int>::min)();

}

```
***
## 枚举类型
* 定义形式：

> *enum* **枚举名**{ 
     标识符[=整型常数], 
     标识符[=整型常数], 
... 
    标识符[=整型常数]
} **枚举变量**;
    
* **实例**

```c++
#include <iostream>
using namespace std;

int main(){
    enum days{one, two, three}day;
    day = one;
    switch(day){
        case one:
            cout << "one" << endl;
            break;
        case two:
            cout << "two" << endl;
            break;
        default:
            cout << "three" << endl;
            break;
    }
    return 0;
}

```
***

# 变量作用域
* **变量重名情况**

>在函数内，**局部变量**的值会==覆盖==**全局变量**的值。

* **类作用域**

```c++
#include <iostream>

class MyClass {
public:
    static int class_var;  // 类作用域变量
};

int MyClass::class_var = 30;

int main() {
    std::cout << "类变量: " << MyClass::class_var << std::endl;
    return 0;
}
```

> MyClass 类中声明了一个名为 class_var 的类作用域变量。可以使用类名和作用域解析运算符<mark>::</mark>来访问这个变量。
***
# 常量
> *注意*：把**常量**定义为==大写字母==形式，是一个很好的编程实践。
***


# 类型限定符
  *用于在定义变量或函数时**改变**它们的<u>默认行为</u>的关键字。*

  * static

> 用于定义静态变量，表示该变量的**作用域**仅限于==当前文件或当前函数==内，不会被其他文件或函数访问。**static** 关键字使局部变量存储在==程序生命周期内都存在==

```c++
void example_function() {
    static int count = 0; // static 关键字使变量 count 存储在程序生命周期内都存在
    count++;
}
```

***

# 存储类

> 存储类定义 C++ 程序中**变量/函数**的*范围（可见性）和生命周期*。

## static 存储类
>- 使用 static 修饰局部变量可以在函数调用之间保持局部变量的值。
>- static 修饰符也可以应用于全局变量。当 static 修饰**全局变量**时，会使变量的**作用域**限制在声明它的<u>文件内</u>。
> - 当 static 用在**类数据成员**上时，会导致仅有一个该成员的<u>副本</u>被==类的所有对象共享==。详细说明[点这](#类的静态成员)

## extern 存储类
> - 当有多个文件且定义了一个可以在其他文件中使用的全局变量或函数时，可以在其他文件中使用 extern 来得到已定义的变量或函数的引用。可以这么理解，==extern 是用来在<u>另一个文件中</u>**声明**一个*全局变量或函数*==。
> - extern 修饰符通常用于当有两个或**多个文件**==共享==**相同的**<u>全局变量或函数</u>的时候

**实例**
- 第一个文件:`main.cpp`

```c++
#include <iostream>
 
int count ;
extern void write_extern();
 
int main()
{
   count = 5;
   write_extern();
}
```
- 第二个文件：`support.cpp`

```c++
#include <iostream>
 
extern int count;
 
void write_extern(void)
{
   std::cout << "Count is " << count << std::endl;
}
```

## mutable存储类

>mutable 说明符仅适用于**类的对象**，它允许对象的成员替代常量。也就是说，mutable 成员可以通过 ==const 成员函数==*修改*。

具体解释和实例[点这](#const修饰成员函数)

***
# 运算符

## 三目运算符

> 条件？ 语句1 ：语句2

**实例**：
```c++
#include <stdio.h>
	int main(void) {
	int a, b;
	scanf("%d", &a);
	b = (a > 0) ? 1 : 0;
	printf("%d\n%d", a, b);
}
```

## 移位运算符

```a = b >> 2;```->*右移两位*
***


# 函数

## 引用调用

> 注意函数定义时参数写成`类型 &形参名`，函数进行调用时，直接写成`function(a)`就行。

```c++
#include <iostream>
using namespace std;
 
// 函数声明
void swap(int &x, int &y);
 
int main ()
{
   // 局部变量声明
   int a = 100;
   int b = 200;
 
   cout << "交换前，a 的值：" << a << endl;
   cout << "交换前，b 的值：" << b << endl;
 
   /* 调用函数来交换值 */
   swap(a, b);
 
   cout << "交换后，a 的值：" << a << endl;
   cout << "交换后，b 的值：" << b << endl;
 
   return 0;
}
 
// 函数定义
void swap(int &x, int &y)
{
   int temp;
   temp = x; /* 保存地址 x 的值 */
   x = y;    /* 把 y 赋值给 x */
   y = temp; /* 把 x 赋值给 y  */
  
   return;
}

```

## 参数的默认值
>可以为参数列表中后边的每一个参数指定默认值。当调用函数时，如果实际**参数的值留空**，则*使用这个默认值。*


***
# 常用数学运算
## 内置数学函数
> **注意**以下函数必须加头文件==cmath==

1.*三角函数类*
- sin();cos();tan();

2.*对数指数类*
- log();
> 返回值的**自然对数**

- pow(a,b);
> 返回a^b

3.*平方根类*
- hypot(x,y);

>返回x^2 + y^2 的平方根（勾股）

- sqrt();
> 返回参数的平方根


4.*绝对值类*
- abs();

> 返回整数的绝对值

- fabs();

> 返回浮点数的绝对值

- floor();

> 返回一个**小于等于**参数的**最大整数**

## 随机数
> 生成随机数之前必须**先调用 srand() 函数**。实例中使用了 **time() 函数**来获取系统时间的*秒数*，通过调用**rand() 函数**来生成随机数
>>**注意：** 要加头文件==ctime==和==cstdlib==

```c++
#include <iostream>
#include <ctime>
#include <cstdlib>
 
using namespace std;
 
int main ()
{
   int i,j;
 
   // 设置种子
   srand( (unsigned)time( NULL ) );
 
   /* 生成 10 个随机数 */
   for( i = 0; i < 10; i++ )
   {
      // 生成实际的随机数
      j= rand();
      cout <<"随机数： " << j << endl;
   }
 
   return 0;
}

```

***

# 数组&字符串的小区别

- 若字符串像这样定义：`char a[] = "abcd";`则要输出该字符串只需`cout << a;`即可。
- 而数组如`int a[] = {1,2,3};`则不能这么输出

> tips:**数组名**指向的是一个==指针常量==，其值不能改变，但能进行变换。
>>如：`int arr[];`
`cout << *(arr+1);`

<u>*字符串操作及输入可以参考以下链接：*</u>

<https://www.runoob.com/cplusplus/cpp-strings.html>

***
# 指针和引用（&）的区别

> - **不存在空引用**。引用必须连接到一块合法的内存。
> - ==一旦引用被初始化为一个对象，就不能被指向到另一个对象==。指针可以在任何时候指向到另一个对象。
> - 引用必须在创建时被初始化。指针可以在任何时间被初始化。

***

## 引用和常量引用
- 常量引用：顾名思义就是在引用前加const,`const int& a = ...`
</br>
- **注意区别**：
1. **非常量**引用的**初始值**必须为==左值==。

> 如：`int a = 1;int &b = a; //例一  `是**正确**；
> 但`int &a = 1;  //例二  `是**错误**。
> **但是**，非常量引用==能更改值==。接例一：`b = 3;`
>> 而且它只能用==非常量的左值==进行初始化


2.**常量**引用的初始值可以为==变量，常量以及非左值==
> 如： `const int &a = 1;  //例三 这是合法的对于const引用`
> `const int a = 2; const int &b = a;//例四 也是合法的`
> 但是**常量引用**==不能更改值==，接例四：`b = 3;// 非法`是**错误**的

上面的知识可以与**类函数**的**参数传递**相联系，如[拷贝构造](#拷贝构造函数)，[运算符的重载中的输入输出](#运算符的重载)
# 类&对象

## 构造函数的初始化列表

```c++
C::C( double a, double b, double c): X(a), Y(b), Z(c)
{
  ....
}

```

## 拷贝构造函数

> 注意：如果类带有==指针变量==，并有==动态内存分配==，则它必须有一个**拷贝构造函数**。

* 最常见的形式：
```c++
classname (const classname &obj) {
   // 构造函数的主体
}
/*obj 是一个对象引用，该对象是用于初始化另一个对象的。*/
```
- **调用拷贝构造函数的情况**：

1. 一个对象以值传递的方式*传入函数体*
2. 一个对象以值传递的方式从*函数返回*
3. 一个对象需要通过*另外一个对象进行初始化*。


## 友元函数

类的友元函数是**定义在类外部**，但==有权访问==类的所有私有<u>（private）</u>成员和保护<u>（protected）</u>成员。
> 友元可以是一个函数，该函数被称为友元函数；*友元*也**可以是一个类**，该类被称为友元类，在这种情况下，**整个类及其所有成员都是友元**。

* 用法：如果要使函数为一个类的友元，**需要在该类中声明该函数**，并在前面使用关键字 ==friend==(友元类同理)

**eg**:
```c++
#include <iostream>
 
using namespace std;
 
class Box
{
   double width;
public:
   friend void printWidth( Box box );
   void setWidth( double wid );
};
 
// 成员函数定义
void Box::setWidth( double wid )
{
    width = wid;
}
 
// 请注意：printWidth() 不是任何类的成员函数
void printWidth( Box box )
{
   /* 因为 printWidth() 是 Box 的友元，它可以直接访问该类的任何成员 */
   cout << "Width of box : " << box.width <<endl;
}
 
// 程序的主函数
int main( )
{
   Box box;
 
   // 使用成员函数设置宽度
   box.setWidth(10.0);
   
   // 使用友元函数输出宽度
   printWidth( box );
 
   return 0;
}
```

## this指针
> - 当一个*对象*的**成员函数**==被调用时==，编译器会隐式地传递该==对象的地址==作为 this 指针。
> - *友元函数*==没有 this 指针==，**因为友元不是类的成员**，只有成员函数才有 this 指针。

## 类的静态成员
1. 静态成员

我们==不能==把静态成员的初始化放置在**类的定义中**，但是可以**在类的外部通过使用范围解析运算符 :: 来重新声明静态变量**从而对它进行==初始化==

**eg**:
```c++
#include <iostream>
 
using namespace std;
 
class Box
{
   public:
      static int objectCount;
      // 构造函数定义
      Box(double l=2.0, double b=2.0, double h=2.0)
      {
         cout <<"Constructor called." << endl;
         length = l;
         breadth = b;
         height = h;
         // 每次创建对象时增加 1
         objectCount++;
      }
      double Volume()
      {
         return length * breadth * height;
      }
      static int getCount()
      {
         return objectCount;
      }
   private:
      double length;     // 长度
      double breadth;    // 宽度
      double height;     // 高度
};
 
// 初始化类 Box 的静态成员
int Box::objectCount = 0;
 
int main(void)
{
  
   // 在创建对象之前输出对象的总数
   cout << "Inital Stage Count: " << Box::getCount() << endl;
 
   Box Box1(3.3, 1.2, 1.5);    // 声明 box1
   Box Box2(8.5, 6.0, 2.0);    // 声明 box2
 
   // 在创建对象之后输出对象的总数
   cout << "Final Stage Count: " << Box::getCount() << endl;
 
   return 0;
}
```

2. 静态成员函数

- 如果把函数成员声明为静态的，就可以把函数与类的任何特定对象独立开来。
- 静态成员函数即使在类对象不存在的情况下也能被调用，==静态函数只要使用类名加范围解析运算符 :: 就可以访问==。

- 静态成员函数只能访问静态成员数据、其他静态成员函数和类外部的其他函数。没有this指针

***

## const修饰成员函数

> 在类成员函数后加**const**，表示在成员函数中保证==不会修改==调用对象的==成员变量==

- **要点**：
1. 如果成员变量有**mutable**修饰，则可无视const，函数内可修改该值
2. 加了`const`的函数**只能调用“const函数”**；一般函数则都可调用是（非）const函数。
3. **const对象**调用的函数规则与2.类似


# 继承
- **语法**：

`class derived-class: access-specifier base-class
`
> 如果**未使用**访问修饰符 access-specifier，则==默认为 private==。

- **注意**：

一个派生类继承了所有的基类方法，*但下列情况除外*：

* 基类的**构造**函数、**析构**函数和**拷贝**构造函数。
* 基类的**重载运算符**。
* 基类的**友元函数**。

尽管不能在派生类**函数体**中直接使用基类的构造函数，但是能在**派生类**的构造函数==参数列表中==**使用基类构造函数赋值**

如：</br>
```c++
#include <iostream>
 
using namespace std;
 
// 基类
class Shape 
{
   public:
      Shape(int w,int h)
      {
        width=w;
        height=h;
      }
   protected:
      int width;
      int height;
};
 
// 派生类
class Rectangle: public Shape
{
   public:
      Rectangle(int a,int b):Shape(a,b)
      {
        
      }
};
```
***

# 运算符的重载
直接看例子：
1. "i++和++i"的重载：
>**前缀形式**重载调用 Check ==operator ++ ()==，**后缀形式**重载调用 ==operator ++ (int)== 注意，**int** 在 括号内是为了向编译器说明这是一个==后缀形式==，而不是表示整数。

```c++
#include <iostream>
using namespace std;
 
class Check
{
  private:
    int i;
  public:
    Check(): i(0) {  }
    Check operator ++ ()
    {
        Check temp;
        temp.i = ++i;
        return temp;
    }
 
    // 括号中插入 int 表示后缀
    Check operator ++ (int)
    {
        Check temp;
        temp.i = i++;
        return temp;
    }
 
    void Display()
    { cout << "i = "<< i <<endl; }
};
 
int main()
{
    Check obj, obj1;    
    obj.Display(); 
    obj1.Display();
 
    // 调用运算符函数，然后将 obj 的值赋给 obj1
    obj1 = ++obj;
    obj.Display();
    obj1.Display();
 
    // 将 obj 赋值给 obj1, 然后再调用运算符函数
    obj1 = obj++;
    obj.Display();
    obj1.Display();
 
    return 0;
}
```
2. 输入输出运算符的重载

> **注意**：在重载**输出流运算符**时，可以==使用const Value &d==作为参数的原因是，**输出操作符不会修改被输出的对象的值**。因此，可以将参数声明为const引用，允许传递const Value类型的对象，以及非const Value类型的对象。
> 然而，重载**输入流运算符**时情况稍有不同。输入操作符的目的是将输入的数据存储到对象中，即修改对象。因此，参数必须是非常量引用==Value &d==，以**确保可以直接对参数进行修改**。
>> 特别的，我们需要把输入输出运算符重载函数声明为**类的友元函数**，这样我们==就能不用创建对象而直接调用函数==。

```c++
#include <iostream>
using namespace std;
 
class Distance
{
   private:
      int feet;             // 0 到无穷
      int inches;           // 0 到 12
   public:
      // 所需的构造函数
      Distance(){
         feet = 0;
         inches = 0;
      }
      Distance(int f, int i){
         feet = f;
         inches = i;
      }
      friend ostream &operator<<( ostream &output, 
                                       const Distance &D )
      { 
         output << "F : " << D.feet << " I : " << D.inches;
         return output;            
      }
 
      friend istream &operator>>( istream  &input, Distance &D )
      { 
         input >> D.feet >> D.inches;
         return input;            
      }
};
int main()
{
   Distance D1(11, 10), D2(5, 11), D3;
 
   cout << "Enter the value of object : " << endl;
   cin >> D3;
   cout << "First Distance : " << D1 << endl;
   cout << "Second Distance :" << D2 << endl;
   cout << "Third Distance :" << D3 << endl;
 
 
   return 0;
}
```

**补充**：
> 如果运算符有**连续**的操作（如连加：a = a+b+c...）,则函数返回值类型为相应类型的==引用==（即**调用者本身**或**输入输出流本身**），可参考上面的输入输出，否则返回值类型一般不为引用