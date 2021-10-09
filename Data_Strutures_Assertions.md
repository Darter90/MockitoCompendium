<h1>Data Structures Assertions</h1>

In this page are grouped the Best Practices for asserting Data Structures.

---

<h4>Integer</h4>

Tips: these assertions works even on Float and Long class.

```
// is equals or not ?
assertEquals(anotherInteger, integerObject) or assertNotEquals(anotherInteger, integerObject)

// is null or not ?
assertNull(integerObject) or assertNotNull(integerObject)

// is instance of ?
assertTrue(integerObject instanceof Integer)

// is less or equals to zero ?
assertTrue(integerObject <= 0) or (assertFalse integerObject <= 0)
```

---

<h4>Object</h4>

```
// is equals or not ?
assertEquals(anotherObject, objectInstance) or assertNotEquals(anotherObject, objectInstance)

// is null or not ?
assertNull(objectInstance) or assertNotNull(objectInstance)

// is instance of ?
assertTrue(objectInstance instanceof objectClass)
```
---

<h4>String</h4>

```
// is equals or not ?
assertEquals(anotherString, stringObject) or assertNotEquals(anotherString, stringObject)

// is null or not ?
assertNull(stringObject) or assertNotNull(stringObject)

// is instance of ?
assertTrue(stringObject instanceof String)

// is empty or not ?
assertTrue(stringObject.isEmpty()) or assertFalse(stringObject.isEmpty())
```

---

<h4>Map</h4>

Tips: on Set, List and Array you can use the same assertions, but you must change methods based on data structure.


```
// is equals or not ?
assertEquals(anObject, mapObject) or assertNotEquals(anObject, mapObject)

// is null or not ?
assertNull() or assertNotNull()

// is instance of ?
assertTrue(mapObject instanceof Map<~>)

// is empty or not ?
assertTrue(mapObject.isEmpty()) or assertFalse(mapObject.isEmpty())

// containsKey or not ?
assertTrue(mapObject.containsKey(key)) or assertFalse(mapObject().containsKey(key))

// containsValue or not ?
assertTrue(mapObject().containsValue(value)) or assertFalse(mapObject().containsValue(value))
```

---

<h4>Exception Interface</h4>


Sample class:
```
public interface MyException {

default String myFunctionException() {
		throw new TypologyOfException();
	}
}
```

Unit Test:

```
@ExtendWith(MockitoExtension.class)
class MyExceptionTest {

    @Spy
    MyException myException;

    @Test
    void myFunctionException() {
        assertThrows(TypologyOfException.class, () -> myException.myFunctionException());
    }
}
```

