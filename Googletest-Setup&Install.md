## Compile and Install

1. Download source code .zip package: https://code.google.com/p/googletest/
2. Unzip, and complie:
```
unzip gtest*.zip
cd 
./configure
make
```
3. *Install Step* Copy header files and libs into system directories:
```
sudo cp -a include/gtest /usr/include
sudo cp -a lib/.libs /usr/lib/
// UPdate the cahce of linker
sudo ldconfig -v 
```

## How to use in your program

The following is sample code:
```
// main.cpp
#include <gtest/gtest.h>

int Foo(int a, int b) {
  if (a == 0 || b == 0)
    throw "don't do that";
  int c = a % b;
  if (c == 0)
    return b;
  return Foo(b, c);
}

TEST(FooTest, HandleNoneZeroInput) {
  EXPECT_EQ(2, Foo(4, 10));
  EXPECT_EQ(6, Foo(30, 18));
}

// Optional
// We can ignore main fucntion witch explicit -lgtest_main 
int main(int argc, char* argv[]) {
  testing::InitGoogleTest(&argc, argv);
  return RUN_ALL_TESTS();
}
```

Compile with commands:
```
g++ -o main main.cpp -lpthread -lgtest -lgtest_main
```

##Reference
http://stackoverflow.com/questions/13513905/how-to-easily-setup-googletest-on-linux