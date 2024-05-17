# 类与面向对象
## 抽象类和接口的区别
- *抽象类*中的==方法可以在其中实现==，而***接口***不能将方法实现
- 一个类可以实现==多个接口==
- 接口==不能存在**静态方法**==
# java的类
## String类
1. **split()方法**
- 语法
> split(String regex,int limit);
> **参数**
> - regex -- 正则表达式分隔符
> - limit -- 分割的份数

**注意：**
- `.`、`$`、`|`、`*`等转义字符必须得加`\\`
- 多个分隔符，用`|`作为连字符
- 当**分割符**位于==开始==或==结尾==时，仍将字符串分成两半，如`.java`,当用"."为分隔符时，将其拆分为==空字符串`""`和java==

**eg:**
```java
public class Test {
    public static void main(String args[]) {
        String str = new String("Welcome-to-Runoob");
 
        System.out.println("- 分隔符返回值 :" );
        for (String retval: str.split("-")){
            System.out.println(retval);
        }
 
        System.out.println("");
        System.out.println("- 分隔符设置分割份数返回值 :" );
        for (String retval: str.split("-", 2)){
            System.out.println(retval);
        }
 
        System.out.println("");
        String str2 = new String("www.runoob.com");
        System.out.println("转义字符返回值 :" );
        for (String retval: str2.split("\\.", 3)){
            System.out.println(retval);
        }
 
        System.out.println("");
        String str3 = new String("acount=? and uu =? or n=?");
        System.out.println("多个分隔符返回值 :" );
        for (String retval: str3.split("and|or")){
            System.out.println(retval);
        }
    }
}

/*- 分隔符返回值 :
Welcome
to
Runoob

- 分隔符设置分割份数返回值 :
Welcome
to-Runoob

转义字符返回值 :
www
runoob
com

多个分隔符返回值 :
acount=? 
 uu =? 
 n=?
*/
```

2. **trim()方法**
*用于删除字符串头尾空白符*
- 语法：
> trim();

- 无参数

***返回一个删除空白符的字符串***

**eg:**
```java
public class Test {
    public static void main(String args[]) {
        String Str = new String("    www.runoob.com    ");
        System.out.print("原始值 :" );
        System.out.println( Str );

        System.out.print("删除头尾空白 :" );
        System.out.println( Str.trim() );
    }
}

```

---
## StringBuffer类
- 初始化
> StringBuffer stringBuffer = new StringBuffer();
> StringBuffer stringBuffer = new StringBuffer("Hello World!");

- **StringBuffer对象和String对象互转**
==错误方式==：
> StringBuffer s = "abc";  //**赋值类型不匹配**
> StringBuffer s = (StringBuffer)"abc";  //**不存在继承关系，无法进行强转**

==正确方式：==
> String string1 = "Hello World!";
StringBuffer stringBuffer = new StringBuffer(string1);  //**String转换为StringBuffer**
String string2 = stringBuffer.toString();  //**StringBuffer转换为String**

- **函数方法**
1. append()函数
```java
StringBuffer stringBuffer = new StringBuffer("Hello");
stringBuffer.append("World!");
System.out.println(stringBuffer);

```

2. reverse()函数
```java
StringBuffer stringBuffer = new StringBuffer("abc");
System.out.println(stringBuffer.reverse());

```

## 包装类
- **装箱和拆箱**
![Alt text](image.png)

![Alt text](image-1.png)

- **将包装类转换成其他数据类型**
```java
Integer i = new Integer(100);
//转换成double类型
double d = i.doubleValue();
System.out.println("d的值：" + d);
//转换成float类型
float f = i.floatValue();
System.out.println("f的值" + f);

```
- **如何将基本数据类型转换成字符串**
![Alt text](image-2.png)

- **如何将字符串转换成基本数据类型**
![Alt text](image-3.png)

## 常用类
### Object类
> **它是所有类的父类，如果一个类没有使用extends关键字明确标识继承另外一个类，那么这个类就默认继承 Object 类。**

1. toString()方法
- eg:
```java
package educoder;
public class TestToStringDemo2 {
    public static void main(String[] args) {
        Person p = new Person();
        System.out.println(p);
    }
}
class Person extends Object {
    String name = "张三";
    int age = 18;
    // 复写Object类中的toString()方法
    public String toString() {
        return "我是:" + this.name + ",今年:" + this.age + "岁";
    }
}
```

2. equals()方法
- ***如果不重写该方法，那么比对的是对象的地址内存***
- eg
```java
package educoder;
public class test {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.name = "jack";
        Dog dog1 = new Dog();
        dog1.name = "jack";
        System.out.println(dog);
        System.out.println(dog1);
        if (dog.equals(dog1)) {
            System.out.println("两个对象是相同的");
        } else {
            System.out.println("两个对象是不相同的");
        }
    }
}
class Animal {
}
class Dog extends Animal {
    int age = 20;
    String name = "rose";
    public String toString() {
        return "Dog [age=" + age + ", name=" + name + "]";
    }
    /* getClass() 得到的是一个类对象 */
    @Override
    public boolean equals(Object obj) {
        if (this == obj)// 两个对象的引用是否相同，如果相同，说明两个对象就是同一个
            return true;
        if (obj == null)// 如果比较对象为空，不需要比较，肯定不相等
            return false;
        if (getClass() != obj.getClass())// 比较两个对象的类型是否相同，如果不同，肯定不相同
            return false;
        Dog other = (Dog) obj;// 转化成相同类型后，判断属性值是否相同
        if (name == null) {
            if (other.name != null)
                return false;
        } else if (!name.equals(other.name))
            return false;
        return true;
    }
}

```

### ArrayList类
- 语法格式：

`import java.util.ArrayList; // 引入 ArrayList 类`
`ArrayList<E> objectName =new ArrayList<E>();　 // 初始化`

- 方法：
1. 添加元素（add()方法）
- eg:
```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        System.out.println(sites);
    }
}

/*输出结果为：
[Google, Runoob, Taobao, Weibo]*/
```
2. 访问元素（get()方法）
- eg:
```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        System.out.println(sites.get(1));  // 访问第二个元素
    }
}
```

3. 修改元素（set()方法）
- eg:
```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        sites.set(2, "Wiki"); // 第一个参数为索引位置，第二个为要修改的值
        System.out.println(sites);
    }
}
```

4. 删除元素

