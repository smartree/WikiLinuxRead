# {}-list Initialization

list-initialization (`{}`) is a new form introduced in C++11, which can be used to initialize variables, including build-in types and user-defined types (classes).

## Initialize build-in type variables with default values 

Most build-in types have a default value (`int` => 0, `bool` => false, `<pointer>` => nullptr).

The benefit of using `{}`-list is that narrowing is not allowed.

```cp
int a; // uninitialized.
int a {}; // a = 0;
int b {1}; // b = 1;
float c {a}; // Error: narrowing is not allowed
```


## Initialize class variables:

This can be divided into two subcases:

* Initialization without constructors

```cpp
struct A { int a; }; // An aggregate class
A object; // member a is uninitialized
A object {}; // default initialization: a = 0
A object {1}; // aggregate initialization: a = 1
```
   
* Initialization with constructors

The list-initialization will call the corresponding constructor to construct the object.
Aggregate initialization is not available in this case because classes with user-provided constructors are not aggregates.

```cpp
struct A {
   A(int);
   A();
};

A object {}; // Call default ctor A()
A object {1}; // Call A(1)
```

Things will be more complicated if the class has initializer-list constructor (a constructor that takes a single argument of `std::initializer_list`). The `{}-list` will be used as the argument in the initializer-list constructor.

If a class has serval constructors (default, initializer-list), the selected constructor follows two rules below:

1. Prefer default constructor if either a default constructor or an initializer-list constructor can be invoked.
2. Prefer initializer-list constructor if either a default constructor or an "ordinary" constructor can be invoked.

Rule 1 states that unlike non-empty `{}`-list, zero-element `{}`-list is a special case, which will be handled by a default constructor if present. This is reasonable -- because we use `{}`-list to initialize build-in type variables to default value, the same to classes.

```cpp
struct A {
  A();
  A(int);
  A(std::initializer_list<T>);
};

A object (); // default ctor
A object {}; // default ctor
A object ({}); // initializer-list ctor
A object {1}; // initializer-list ctor, not A(1)
A object {1, 2}; // initializer-list ctor

struct B {
  B(std::initializer_list<T>);
};

B object; // Error, no default ctor
B object {}; // initializer-list ctor as default ctor is not defined.
B object ({}); // initializer-list ctor
B obejct {1, 2}; // initializer-list ctor
```

## References

* The C++ Programming language, chapter 6.3.5, 11.3, 17.3