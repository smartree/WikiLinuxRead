问题：

为什么能够以`by-value`方式返回`unique_ptr` 而不用显式使用`std::move`? 看下面例子：

```cpp
std::unique_ptr<int> ptr() {
    std::unique_ptr<int> p(new int(3));
    return p;  //  Why doesn't this require explicit move using std::move?
} 

std::unique_ptr<int> a = ptr();  // Why doesn't this require std::move? 
```

我们知道`unique_ptr`是不能复制的（copy constructor被deleted），按照通常理解：当函数返回值时候，compiler会创建一个临时对象用于保存函数返回值，然后使用这个临时对象初始化给`a`。
可是`unique_ptr`是不能复制的，那么临时对象无法成功创建，为什么能够成功编译呢？

原因是：compiler会优先使用move constructor创建临时对象。

C++ standard 12.8有提到：

> When the criteria for elision of a copy/move operation are met, but not for an exception-declaration, and the object to be copied is designated by an lvalue, or when the expression in a return statement is a (possibly parenthesized) id-expression that names an object with automatic storage duration declared in the body or parameter-declaration-clause of the innermost enclosing function or lambda-expression, overload resolution to select the constructor for the copy is first performed as if the object were designated by an rvalue.

> If the first overload resolution fails or was not performed, or if the type of the first parameter of the selected constructor is not an rvalue reference to the object’s type (possibly cv-qualified), overload resolution is performed again, considering the object as an lvalue.

下面是standard里提供的例子：

```
class Thing {
    public:
     Thing();
     ~Thing();
      Thing(Thing&&);
    private:
     Thing(const Thing&);
};
Thing f(bool b) {
   Thing t;
   if (b)
     throw t; // OK: Thing(Thing&&) used (or elided) to throw t
    return t; // OK: Thing(Thing&&) used (or elided) to return t
}
Thing t2 = f(false)；
```

对于上面例子，左值`p`会被先被当成右值处理；换句话说，会先使用move constructor；如果不成功，再使用copy constructor。这样做的目的是减少不必要的copy开销 (copy elision)。

但是事实上，这里连move constructor也不会调用，因为有[`RVO`](https://en.wikipedia.org/wiki/Return_value_optimization), compiler直接在`ptr()`函数中直接对`a`进行构造了；这也是C++ standard 12.8 31允许的，就算copy/move constructor有side effect。但RVO不同compiler实现不一样，程序行为不应该依赖constructor调用的次数。

查看下面的例子：

```cpp
class Foo {
  public:
    Foo() = default;
    Foo(const Foo& f) {
      cout << "copy ctor\n";
    }
    Foo(Foo&& f) {
      cout << "move ctor\n";
    }
};
Foo f0() {
   Foo t;
   return t1; // RVO
}

Foo f(1bool first) {
   Foo t1, t2;
   if (first) return t1; // no RVO, will call move constructor
   return t2;
} 

Foo f1(bool first) {
   Foo t1, t2;
   return first? t1 : t2; // no RVO, will call copy constructor.
}

int main() {
   f0();
   f1(true);
   f2(true);
}
```