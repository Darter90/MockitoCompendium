<h1>Reflections</h1>

Many times in Unit Tests you have to work with classes that you cannot access easily. 
Since you cannot modify the code in the class under test, you can use  Reflections package to access methods, fields and other stuffs that usually you cannot access in a more usual way.

---

<h4>Private Field</h4>

Imagen this situation:

```
public class PrivateField {
    
    // private value
    private String yourString;
    
    // public getter
    public String getYourString(){
        return yourString;
    }
}
```

In this example you have a class with a public method and a private field. You cannot access it or use a setter to fill that string value.

Reflection package comes to help us. Without going into detail, with Reflections <b>you can access to every field that is not public without touching the original class.</b> And for Unit Test is a great deal.

To start, you must import the package for Reflections:

```
import java.lang.reflect.*;
```

At this point, you must specify in your method that you are using Reflections to go against the rules of access modifiers.
You simply need to insert these Exceptions: <i>NoSuchFieldException</i> and <i>IllegalAccessException</i>

```
@Test
void testing() throws throws NoSuchFieldException, IllegalAccessException {

    // code goes here

}
```
Usually is the IDE to prompt you which kind of Exception you must insert for using Reflections, so keep an eye on it...

Now you can use Reflections. With Reflections, you have to incapsulate the private field into a <i>Reflection Object</i>, operate on the private field through the Object and then inject the value that you want.

```

@Test
void testingReflections() throws NoSuchFieldException, IllegalAccessException{

    // calling constructor
    PrivateField privateField = new PrivateField();

    // reflecting private field
    Field privateYourString = PrivateField.class.getDeclaredField("yourString");
    
    // opening field accessibility
    privateYourString.setAccessible(true);

    // injecting value
    String myValueForTest = "Hello World!";
    privateYourString.set(privateField, myValueForTest);

    // assert
    assertEquals(privateField.getYourString, myValueForTest);

}

```

---

<h4>Private Method</h4>

Let's change the class to make even the method private:

```
public class PrivateField {
    
    // private value
    private String yourString;
    
    // private getter
    private String getYourString(){
        return yourString;
    }
}
```

The idea is the same, but this time we have to use the <i>Method Reflection Object</i> instead of Field; plus, we have to call the method by <i>invoking it</i> and add a new Exceptions: <i>NoSuchMethodException</i> and <i>IllegalAccessException</i>:

```
@Test
void testingReflections() throws NoSuchFieldException, IllegalAccessException, NoSuchMethodException, InvocationTargetException {

    // calling constructor
    PrivateField privateField = new PrivateField();

    // reflecting private field
    Field privateYourString = PrivateField.class.getDeclaredField("yourString");
    
    // opening field accessibility
    privateYourString.setAccessible(true);

    // injecting value
    String myValueForTest = "Hello World!";
    privateYourString.set(privateField, myValueForTest);

    // reflecting private method
    Method privateMethod = PrivateField.class.getDeclaredMethod("getYourString");
    privateMethod.setAccessible(true);

    // assert
    assertEquals(privateMethod.invoke(privateField), myValueForTest);

}
```

On <a href="https://www.baeldung.com/java-reflection">Baeldung</a> you can find some hints and ideas for better using Reflections.