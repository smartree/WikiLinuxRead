从C99开始允许 empty macro  arguments：

```
#define FUN(x, y) return (x) < (y) ? (x) : (y);

FUN(1, 2) // OK: return (1) < (2) ? (1) : (2);
FUN(1, ) // OK: return (1) < ( ) ? (1) : ( );
FUN(, 2) // OK: return ( ) < (2) ? ( ) : (2);
```

macro arguments以`,`隔开，只要不传任何东西进参数，就为 empty argument。对于 empty argument，macro 的展开都是为空的。
上面例子从语法来看是合法的，能够通过预处理 (`g++ -E`)，但是通过不了编译，因为 macro 展开后的语法不正确。

但这仅仅是对于 macro，对 function 来说就没效了。

下次看到类似`Func(a, );`这样的代码就不会疑惑了。

References: https://gcc.gnu.org/onlinedocs/cpp/Macro-Arguments.html
