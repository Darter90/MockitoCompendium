<h1>Arrange -> Act -> Assert</h1>


Everytime you have to work on a Unit Test, there are three operations to follow in order:

1) The first operation consists in <b>creating the test object</b>, together with the other objects and elements of the code such as @Annotations and references to the testing frameworks;

2) The second operation consists in executing the methods of the software under testing with the help of mocks, reflections and other instruments, if necessary, and proceeding step by step until the resolution of the code;

3) The third and last phase is the verification phase, in which the assertions or verification tools offered by the test frameworks are used.
Here, you have to explain what is intended to happen at the end of the test (it is not always possible, reason why verification assertions exists). 


This 3-phase pattern does not have a precise name, but can be summarized as “the 3 A's of software testing”. The 3 phases are called <b>Arrange</b> -> <b>Act</b> -> <b>Assert</b>.

Surely the Arrange and Act phases influence each others and requires more or less time than the Assert phase. 

---

<h1>Let's begin!</h1>

<h4>Maven dependencies</h4>

These are the Minimum Required dependencies for making test by yourself and make experiments with Mockito + jUnit5 Frameworks:

````
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.4.2</version>
        <scope>test</scope>
    </dependency>
        <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-core</artifactId>
        <version>3.6.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-inline</artifactId>
        <version>3.6.0</version>
        <scope>test</scope>
        </dependency>
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-junit-jupiter</artifactId>
        <version>3.6.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.junit.platform</groupId>
        <artifactId>junit-platform-runner</artifactId>
        <version>1.2.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.junit.vintage</groupId>
        <artifactId>junit-vintage-engine</artifactId>
        <version>5.4.2</version>
        <scope>test</scope>
    </dependency>
</dependencies>
````
---

<h4>A simple class</h4>

Let's make an example by using a simple Java class to test:

````
public class SoftwareToTest {

    public int sum(int a, int b){
        return a + b;
    }

    public float subtract(float a, float b){
        return a - b;
    }

}
````
---

<h4>Arrange</h4>

On every IDE there's an option to select and generate the test case file.
Check your IDE instruction for that, but remember to select jUnit5 and put it in your <b>test folder</b>. Maven generates automatically the required folder usually.

These are the minimum required import for the test file:
````
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.junit.jupiter.MockitoExtension;
import org.mockito.Spy;

import static org.junit.jupiter.api.Assertions.*;
````


After that, start by arranging the test case in this way:

````
@ExtendWith(MockitoExtension.class)
class SoftwareToTestTest {

    @Spy
    SoftwareToTest softwareToTest;

    @BeforeEach
    void setUp(){
        softwareToTest = new SoftwareToTest();
    }

  // other stuffs...

}
````

Explanation:

<ul>
<li><b>@ExtendWith(MockitoExtension.class)</b>: this Mockito @Annotation is used to indicate that you are using Mockito code, like the <b>mock()</b> method;
</li>
<li><b>@Spy</b>: this Mockito @Annotation is used to track the true object. Usually is used on the instance of the class under test;
</li>
<li><b>@BeforeEach</b>: this jUnit5 @Annotation specify that the following method must be called <i>before each</i> tested method;
</li>
<li><b>void setUp()</b>: this is a specific method of jUnit5 and <b>IT MUST BE NAMED</b> in this way and inserted before a <b>@BeforeEach</b> Annotation.

Everytime you launch a test method, a new instance of the class is created and this makes the operations really memory intensive.

But thanks to this method and this syntax, you can say to the JVM to clean memory and recall a new instance of the class every time you launch a new test case; 
</li>
</ul>

---

<h4>Act</h4>

Now you have to write a test case.<br />
Since this class has two method that sum and subract values, you just need to test if the methods works.

Let's start with sum():

````
@Test
void sum() {

    int a = 5;
    int b = 5;

    softwareToTest.sum(a, b);
}
````

Every test case is followed by a <b>@Test</b> Annotation from jUnit5.
In theory, if the test pass, it means that the method has worked as intended. In more complex cases, you have to use the debugger to see each step of the code execution and track all the lines of code; in our example is unnecessary since the simplicity of this code.

In any case, you have to Assert the result.

---

<h4>Assert</h4>

In Unit Tests you have to <i>assert the final result</i> of the methods that you're testing. Since you cannot return or print results in Unit Tests to demonstrate that the program is not failing, you have to use Assertion methods to check the results.

For example...in this case, we have to assert that <i>(a + b) must be the result of sum() method</i>. So, we have to compare the sum() method with the actual sum of these values:

````
// code...

assertEquals((a + b), softwareToTest.sum(a, b));
}
````

That's all... this is an example of how Unit Tests must be written and intended.

---

<h4>Complete example code</h4>

````
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.Spy;
import org.mockito.junit.jupiter.MockitoExtension;

import static org.junit.jupiter.api.Assertions.*;


@ExtendWith(MockitoExtension.class)
class SoftwareToTestTest {

    @Spy
    SoftwareToTest softwareToTest;

    @BeforeEach
    void setUp(){
        softwareToTest = new SoftwareToTest();
    }

    @Test
    void sum() {

        // value for test
        int a = 5;
        int b = 5;
        int c = a + b;

        // calling method
        softwareToTest.sum(a, b);

        // assert
        assertEquals(c, softwareToTest.sum(a, b));
    }

    @Test
    void subtract() {

        // values for test
        int a = 4;
        int b = 6;
        int c = a - b;

        // calling method
        System.out.println(softwareToTest.subtract(4, 6));

        // assert
        assertEquals(c, softwareToTest.subtract(a, b));
    }
    
}
````