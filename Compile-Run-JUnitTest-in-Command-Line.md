##How to run JUnitTest in CommandLine

Use the following sample code, TestJUnit4.java:
```java
import org.junit.Test;
import junit.framework.TestCase;
    
public class TestJUnit4 extends TestCase {
    int value1 = 2, value2 = 3, expectedResult = 5;
    
    @Test
    public void testSuccess() {
        assertTrue(value1 + value2 == expectedResult);
    }
}
```

Download Junit jars (Both!) and put them in your src folder:

* [junit.jar](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22junit%22%20AND%20a%3A%22junit%22)
* [hamcrest-core](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22org.hamcrest%22%20AND%20a%3A%22hamcrest-core%22)

Run the following commands:

```
// Compile
javac -cp .;junit-4.11-beta-1.jar;hamcrest-core-1.3.jar TestJUnit4.java
// Run
java -cp .;junit-4.11-beta-1.jar;hamcrest-core-1.3.jar org.junit.runner.JUnitCore TestJUnit4
```

The expected results:

```
JUnit version 4.11-beta-1
.
Time: 0.004

OK (1 test)
```