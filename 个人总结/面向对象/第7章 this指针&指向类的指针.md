# 第七章 this指针&指向类的指针

## 7.1 this指针

在 C++ 中，**this** 指针是一个特殊的指针，它指向当前对象的实例。

在 C++ 中，每一个对象都能通过 **this** 指针来访问自己的地址。

**this**是一个隐藏的指针，可以在类的成员函数中使用，它可以用来指向调用对象。

当一个对象的成员函数被调用时，编译器会隐式地传递该对象的地址作为 this 指针。

友元函数没有 **this** 指针，因为友元不是类的成员，只有成员函数才有 **this** 指针。

下面的实例有助于更好地理解 this 指针的概念：

```cpp
#include <iostream>
using namespace std;

class MyClass
{
private:
    int value; // 私有成员变量

public:
    void setValue(int value) // 公有成员函数
    {
        this->value = value; // 通过this指针访问私有成员变量
    }

    void printValue() // 打印私有成员变量
    {
        cout << "Value: " << this->value << endl;
    }
};

int main()
{
    MyClass obj; // 创建对象
    obj.setValue(42); // 设置值
    obj.printValue(); // 打印值
}
```

实例解析：

- 以上实例中，我们定义了一个名为 MyClass 的类，它有一个私有成员变量 value。

- 类中的 setValue() 函数用于设置 value的 值，而 printValue() 函数用于打印 value 的值。

- 在 setValue() 函数中，我们使用 this 指针来引用当前对象的成员变量 value，并将传入的值赋给它，这样可以明确地告诉编译器我们想要访问当前对象的成员变量，而不是函数参数或局部变量。

- 在 printValue() 函数中，我们同样使用 this 指针来引用当前对象的成员变量 value，并将其打印出来。

- 在 main() 函数中，我们创建了一个 MyClass 的对象 obj，然后使用 setValue() 函数设置 value 的值为 42，并通过 printValue() 函数打印出来。

- 通过使用 this 指针，我们可以在成员函数中访问当前对象的成员变量，即使它们与函数参数或局部变量同名，这样可以避免命名冲突，并确保我们访问的是正确的变量。

更多实例：

```cpp
#include <iostream>

using namespace std;

class Box
{
public:
    // 构造函数定义
    Box(double l = 2.0, double b = 2.0, double h = 2.0)
    {
        cout <<"调用构造函数。" << endl;
        length = l;
        breadth = b;
        height = h;
    }
    double Volume() // 体积计算函数
    {
        return length * breadth * height;
    }
    int compare(Box box) // this指针指向当前对象，box参数指向另一个Box对象
    {
        return this->Volume() > box.Volume();
    }
private:
    double length;     // 宽度
    double breadth;    // 长度
    double height;     // 高度
};

int main(void)
{
    Box Box1(3.3, 1.2, 1.5);    // 声明 box1
    Box Box2(8.5, 6.0, 2.0);    // 声明 box2

    if(Box1.compare(Box2))
    {
        cout << "Box2 的体积比 Box1 小" <<endl;
    }
    else
    {
        cout << "Box2 的体积大于或等于 Box1" <<endl;
    }
    return 0;
}
```

## 7.2 指向类的指针

一个指向 C++ 类的指针与指向结构的指针类似，访问指向类的指针的成员，需要使用成员访问运算符 **->**，就像访问指向结构的指针一样。与所有的指针一样，必须在使用指针之前，对指针进行初始化。

在 C++ 中，指向类的指针指向一个类的对象，与普通的指针相似，指向类的指针可以用于访问对象的成员变量和成员函数。

### 7.2.1 声明和初始化指向类的指针

```cpp
#include <iostream>
using namespace std;
class MyClass {
public:
    int data; // 成员变量

    void display() // 成员函数
    {
        cout << "Data: " << data << endl;
    }
};

int main() {
    // 创建类对象
    MyClass obj;
    obj.data = 42; // 给成员变量赋值

    // 声明和初始化指向类的指针
    MyClass *ptr = &obj;

    // 通过指针访问成员变量
    cout << "Data via pointer: " << ptr->data << endl;

    // 通过指针调用成员函数
    ptr->display();
}
```

### 7.2.2 动态分配内存

指向类的指针还可以用于动态分配内存，创建类的对象

```cpp
#include <iostream>
using namespace std;
class MyClass
{
public:
    int data;

    void display() const {
        cout << "Data: " << data << endl;
    }
};

int main() {

    // 动态分配内存创建类对象
    auto *ptr = new MyClass;

    // 通过指针设置成员变量的值
    ptr->data = 42;

    // 通过指针调用成员函数
    ptr->display();

    // 释放动态分配的内存
    delete ptr;
}
```

### 7.2.3 指向类的指针作为函数参数

```cpp
#include <iostream>
using namespace std;
class MyClass
{
public:
    int data;

    void display()
    {
        cout << "Data: " << data << endl;
    }
};

// 函数接受指向类的指针作为参数
void processObject(MyClass *ptr)
{
    ptr->display();
}

int main() {
    MyClass obj; // 创建类的对象
    obj.data = 42; // 设置数据成员的值

    // 将指向类的指针传递给函数
    processObject(&obj);
}
```

## 7.3 综合实例

```cpp

```
