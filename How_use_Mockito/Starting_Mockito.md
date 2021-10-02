<h1>Starting Mockito</h1>

In the main page of this Compendium is written that Mockito is used to <i>mock</i> objects and their funcionalities.

Mockito allows to <b>create mock objects of classes and interfaces</b>, which through it is possible to stub return values for methods and verify if they are called during the code execution.

---

<h4>Where to drink</h4>

Mockito has many ways to work with mocks and you can find all of them on <a href="https://www.baeldung.com/tag/mockito/"> Baeldung</a> or the <a href="https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html">Mockito Documentation</a>

But let's start with an example

---

<h4>@Mock</h4>

Take this example of configuration class:

```
public class ConfigurationOfSomething {

private Map<String, ConfigurationInstructions> configurationList;

    public void configurationSettings( ConfigurationInstructions config) {
        
        if (configurationList == null) {
            configurationList = new HashMap<>();
        }
        if (config.getId() == "A535")
            configurationList.put(config.getCountryIsocode(), config);
        }

}
```

This class has a problem for your Unit Test: it requires a <i>config</i> object to work. Since you are creating a Unit Test, you cannot implemenet and work on all the new object and imange if it is an Interface...

What do you do? Do you start implementing a new class? 
If your answer is <b>No</b> you're correct, since this is the wrong way to work on this test.

To resolve this problem, you have to <i>mock</i> that ConfigurationInstructions class by using the <b>@Mock</b> annotation; this is the main @Annotation that works out-of-the-box with the Best Practice syntax that I showed you in <a href="http://localhost:3000/#/Arrange_Act_Assert">Arrange -> Act -> Assert</a>

By mocking that class, you will be able to pass it to the method of the class under test and then stub the value of getId() method.

First, arrange the test:

```
// all imports...

@ExtendWith(MockitoExtension.class)
class ConfigurationOfSomething {

    @Spy
    ConfigurationOfSomething configurationOfSomething;

    // here you can insert all
    // the mocks that you need

    @Mock
    ConfigurationInstructions config;

    @BeforeEach
    void setUp() {
        configurationOfSomething = new ConfigurationOfSomething();
    }

    @Test
    void configurationSettings() {

         // code goes here

    }

}
```

And here we are: you mocked the ConfigurationInstructions class, or interface, by creating a mock object that will be activated in runtime.

---

<h4>when()/thenReturn()/verify()</h4>

But before assing config to the software under test, we have to mock even the method into the if statement: <b>config.getId()</b>.
Since Mockito do not know how to deal with methods of mocked objects, you must specify what they need to return when they are called into the code. This can be achieved by using the <b>when()/thenReturn()</b> syntax of Mockito framework:

```
String Id = "A535";
when(config.getId()).thenReturn(Id);
```

At the end of the code you can assert if the method has been called correctly for just one time, by using the <b>verify()</b> method of Mockito framework. This method is a sort of Assertion, so it as the same importance of the classic Assertions of jUnit:

```
verify(config, times(1)).getId(Id);
```

The complete code:

```
// all imports...

@ExtendWith(MockitoExtension.class)
class ConfigurationOfSomething {

    @Spy
    ConfigurationOfSomething configurationOfSomething;

    @Mock
    ConfigurationInstructions config;

    @BeforeEach
    void setUp() {
        configurationOfSomething = new ConfigurationOfSomething();
    }

    @Test
    void configurationSettings() {

        // value for test
        String Id = "A535";

        /* When calls */
        when(config.getId()).thenReturn(Id);

        // calling method
        configurationOfSomething();

        // verify
        verify(config, times(1)).getId(Id);
    }
```

In theory, you have to test even the HashMap<>, but since it is a private field you cannot access to...<a href="https://darter90.github.io/MockitoCompendium/#/Private_fields_and_Static_methods/Reflections">or not?<a>