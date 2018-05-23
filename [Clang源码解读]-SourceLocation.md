我们做Clang开发，特别是要对代码进行增删改，都不可避免地会跟`SourceLocation`打交代。每一个token或者AST的节点像`Decl`, `Expression`, 都有类似`getLocation`, `getLocStart`, `getLocEnd`的函数，用于获取该AST节点在代码中的位置。如果想获取对应AST节点的代码，配合着使用`SourceManager`和`Lexer`就能容易的获取到。

SourceLocation提供了dump函数，输出类似`source.cc:<line_number>:<column_number>`易于阅读的信息。

SourceLocation内部是一个32bit`integer`的offset，非常轻量级，拷贝的代价很少，在Clang代码中按值传递。所以SourceLocation可以简单理解成指字符串(这个字符串就是代码)中的offset，指向某个字符。

SourceLocation有一个`getLocWithOffset`函数，这个函数用于移动当前的offset，并返回对应的SourceLocation。用来获取相对于SourceLocation的前面或者后面的SourceLocation。

Clang里有`SourceRange`, `CharSourceRange`的数据结构表示代码里的一个范围(Begin, End)。 CharSourceRange分为两个类型:

1. TokenRange，是基于Token的范围。这种类型下的End是指向最后一个token的开始位置，实际范围会包括最后一个token的长度（`lexer::MeasureTokenLength`）。
2. CharRange, 是基于Char的范围。这种类型下的End指向最后一个char的位置，实际范围是Begin和End所代表的范围

我们使用`Lexer::getSourceText`接口获取某个CharSourceRange的代码块。不过值得注意的是如果是CharRange，最后的End的是不包括，即获取的范围是[begin, end):

```cpp
vector<Token> toks = ParseSource("int a;");
// tok[0]: int
// tok[1]: a
// tok[2]: ;
SourceRange Range(toks[0].getLocation(), toks[2].getLocEnd());
bool Invalid = false;
// Get "int a"
Lexer::getSourceText(CharSourceRange::getCharRange(Range), SourceMgr, &Invalid);
// Get "int a;"
Lexer::getSourceText(CharSourceRange::getCharRange(SourceRange(toks[0].getLocation(), toks[2].getLocation()().getLocWithOffset(1))),
SourceMgr, &Invalid);
// Get "int a;"
Lexer::getSourceText(CharSourceRange::getTokenRange(Range), SourceMgr, &Invalid);
```

如果是宏定义怎么处理？`SourceManager`提供了相应的接口：

```cpp
vector<Token> toks = ParseSource(
  "#define X(x) x\n"
  "X(int a;)");

// Line 2, column 1, 宏展开的位置
toks[0].getLocation();
// Begin: line 2, column 1
// End：Line 2, column 9
// 获取宏展开的位置 
SourceRange MacroRange = SourceMgr.getExpansionRange(toks[0].getLocation());

// 获取token[0] int在macro的位置：Line 2, column 3
SourceLocation SpellingLocBegin = SourceMgr.getSpellingLoc(toks[0].getLocation());

// Line 2, column 6
SourceLocation SpellingLocBegin = SourceMgr.getSpellingLoc(toks[0].getLocation());
```

// Change