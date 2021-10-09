<h1>@InjectMocks</h1>

Few sections ago you've learned that with Mockito + jUnit @BeforeEach syntax, you can instanciate objects easily and without compromise the memory management.

But sometimes, you'll not be able to use this trick and you'll be forced to create a new object into every @Test case. For example, in those constructors that requires parameters before instanciate them.

But there a solution for this...more or less.

<b>@InjectMocks</b> is an annotation to put over the @Spy annotation, every time that you want to use the Mockito @BeforeEach syntax on objects' constructors <b>that requires parameters before their instantiation</b>. In spite of the name, it works even if you must use parameters that are not mocks, like primitive values. 

Here's a piece of code for example:

```
@InjectMocks
@Spy
MyClassToTest myClassToTest;

@Mock
TheParameterMock theParameterMock

int intValue = 5;

@BeforeEach
void setUp(){
    myClassToTest = new MyClassToTest(theParameterMock, intValue);
}
```

Unfortunatelly, this @Annotation doesn't works on constructors that do not accepts null values. Since mocked object are fakes, if a constructor doesn't like null values you cannot use @InjectMock. And so... you have to instantiate a new object for every @Test case and create a not null parameter specific for that test case.