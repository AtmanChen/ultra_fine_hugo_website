+++
title = "C++ 中的自定义类型转换"
description = "这篇博客的内容基本上是 C++ Crash Course 中 User-Defined Type Converstions 的翻译"
tags = [
"C++"
]
date = "2019-10-25"
categories = [
"Code"
]
image = "cpp_type_cast.png"
+++

为什么需要类型转换？比如你可能需要求一组整数的平均值，但这个结果可能不是整数。

## 自定义类型转换

我们可以提供自定义的转换函数。在你进行显式和隐式转换时，编译器就能通过它们知道你是怎样自定义这个类型转换的。

```c++
struct MyType {
    operator destination-type() const {
        // return 返回一个 destination-type 的值
    }
}
```

下面是一个实例:

**Example 1 :**

```c++
struct ReadOnlyValue {

    ReadOnlyValue(const int intValue, const std::string stringValue) : intVal{ intValue }, strVal{ stringValue } {};

    operator int() const {
        return intVal;
    }

    operator std::string() const {
        return strVal;
    }
private:
    const int intVal;
    const std::string strVal;
}
```

operator int 函数定义了将 ReadOnlyValue 类型的变量转换为 int 类型时转换后的值，而且可以返回任何你需要的值。比如这里我们返回了属性 intVal，如果你愿意，也可以返回 intVal * 10。

下面是调用 cast 时的情况:

**Example 2 :**

```c++
int main() {
    ReadOnlyValue r{ 99, "I love c++" };
    auto intCast = r + 1; // 这时 r 被隐式转换为 int 类型，intCast 的值为100
    auto intCast2 = static_cast<int>(r) + 1; // 这时 r 被显式转换为 int 类型，intCast' 的值为100
    auto strCast = static_cast<std::string>(r); // 这时 r 被显式转换为 std::string 类型，strCast 的值为 "I love c++"
}
```

这种自定义转换类型的目的就是消除转换结果中可能发出的歧义或者误差。


## Reference

*[C++ Crash Course Book](https://lospi.net/c/c++/programming/developing/software/2019/07/28/cpp-crash-course.html)*