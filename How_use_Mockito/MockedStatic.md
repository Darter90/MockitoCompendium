<h1>MockedStatic</h1>

While you're working, It could happen to you to face Unit Tests where static methods are often used. These kinds of methods must be managed with a particular instruction of Mockito, named MockedStatic. In few words, <b>you mock the static method itself by creating in runtime a fake call</b>.

---

<h4>How it works</h4>

Given this example:

```
public class MyStaticExample {

    public static String sayHello(String name) {
        return ("Hello" + name);
    }
}
```

Here we have a static method to test. When compared to other mocks, static methods must be mocked inside the single @Test instance, recreate part of the behaviour (but is not always necessary), use them in that moment and then terminate them. <b>If you don't terminate the static method call</b> after finishing the single @Test, <b>it will stay in memory</b> and will throws errors and unwanted situation during the building process of the application. Usually I'm used to close it after the Assertions step.

```
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.MockedStatic;
import org.mockito.junit.jupiter.MockitoExtension;

import static org.junit.jupiter.api.Assertions.*;
import static org.mockito.Mockito.*;

@ExtendWith(MockitoExtension.class)
class MyStaticExampleTest {

    @Test
    void sayHello() {

        // creating the static mock handler
        MockedStatic<MyStaticExample> theMock = mockStatic(MyStaticExample.class);

        // fake call with when/thenReturn
        String name = "Kevin";
        String valueToReturn = String.format("Welcome %s", name);
        theMock.when(() -> MyStaticExample.returnName(name)).thenReturn(valueToReturn);

        // assert
        assertEquals(valueToReturn, MyStaticExample.sayHello(name));

        // close MockedStatic object
        theMock.close();

    }
}
```

Tips: In the examples in the <a href="https://www.baeldung.com/mockito-mock-static-methods">documentation</a>, It's showed that you can use try-with-resources blockcode instead of closing the MockedStatic by hands. Personally speaking, since it's Best Practice to not introduce try-catch structures inside the Unit Tests, I prefere to close it by hand. The choice is yours.