<h1>Explicit Constructor</h1>

Since you have an explicit constructor, you cannot use @Spy annotation and @BeforeEach setUp() syntax. <b>This is a limitation of Mockito</b>. 
Current Best Practice suggest to create a method for unit testing the constructor, with external properties to assign to it. If needed, just copy-paste it into the other methods to create an instance of the object.

Usually this is not a good practice in software development, since 
<i>you must not repeat yourself</i>...but in Unit Test field you need to setting up every test as <b>an entity completely separated from the rest of the code</b>.
And you must have many @Test methods in your test case, if you want to play with the code and test particular situations.


Let's start by arranging the Unit Test:

````
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.junit.jupiter.MockitoExtension;

import java.util.Date;

import static org.junit.jupiter.api.Assertions.*;

@ExtendWith(MockitoExtension.class)
class PersonTest {

    // value for constructor
    String name;
    String surname;
    Date dateSubscription;
    Integer age;
    String birthday;
    Integer aRandomValue;
}
````

Now you have to create an object with a specific @Test case for the constructor:

````
    @Test
    void constructor(){

        name = "name";
        surname = "surname";
        dateSubscription = new Date();
        age = 30;
        birthday = "21/04/1990";
        aRandomValue = 34;

        Person person = new Person(
            name,
            surname,
            dateSubscription,
            age,
            birthday,
            aRandomValue
        );
    }
````

Question: <b>what do you have to assert in a constructor</b>?

Answer:

<ul>
<li>the object instance;</li>
<li>if values are null;</li>
<li>every value instance;</li>
<li>if setted values are what you suppose they are.</li>
</ul>


Let's make an example with just the name value:

````
// constructor

    assertEquals(name, person.getName());
    assertTrue(person.getName() instanceof String);
    assertNotNull(person.getName());
    assertFalse(person.getName().isEmpty());
````

As you can see, we can use the getters into the assertions to make the Unit Test more complete and usefull.
For the constructor, we just need few lines:

````
    assertTrue(person instanceof Person);
    assertNotNull(person);
}
````

Since we have to repeat more or less the same assertions for every value of the object, we can use the <b>assertAll()</b> method to group them all and launch them all together. You can even add messages to better specify what are you testing:

````
assertAll(
        "constructor",
        // name
        () -> assertEquals(name, person.getName(), "name value must be equals"),
        () -> assertTrue(person.getName() instanceof String, "name must be instance of String"),
        () -> assertNotNull(person.getName(), "name must not be null"),
        () -> assertFalse(person.getName().isEmpty()),
        // surname
        (...)
        );

````

Remember to use comments to better explain and divide every section of the Unit Test

This is the complete test for the constructor test case:

````
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.junit.jupiter.MockitoExtension;

import java.util.Date;

import static org.junit.jupiter.api.Assertions.*;

@ExtendWith(MockitoExtension.class)
class PersonTest {

    // value for constructor
    String name;
    String surname;
    Date dateSubscription;
    Integer age;
    String birthday;
    Integer aRandomValue;


    @Test
    void constructor(){

        // value for test
        name = "name";
        surname = "surname";
        dateSubscription = new Date();
        age = 30;
        birthday = "21/04/1990";
        aRandomValue = 34;

        // creating a Person object
        Person person = new Person(
                name,
                surname,
                dateSubscription,
                age,
                birthday,
                aRandomValue
        );


        /* Assert */

        assertAll(
                "constructor",
                // person
                () -> assertTrue(person instanceof Person),
                () -> assertNotNull(person),
                // name
                () -> assertEquals(name, person.getName()),
                () -> assertTrue(person.getName() instanceof String),
                () -> assertNotNull(person.getName(),
                () -> assertFalse(person.getName().isEmpty()),
                // surname
                () -> assertEquals(surname, person.getSurName()),
                () -> assertTrue(person.getSurName() instanceof String),
                () -> assertNotNull(person.getSurName()),
                () -> assertFalse(person.getSurName().isEmpty()),
                // dateSubscription
                () -> assertEquals(dateSubscription.getDate(), person.getDateSubscription()),
                () -> assertTrue(person.getDateSubscription() instanceof Integer),
                () -> assertFalse(person.getDateSubscription() <= 0),
                () -> assertNotNull(person.getDateSubscription()),
                // age
                () -> assertEquals(age, person.getAge()),
                () -> assertTrue(person.getAge() instanceof Integer),
                () -> assertFalse(person.getAge() >= 18),
                () -> assertNotNull(person.getAge()),
                // birthday
                () -> assertEquals(birthday, person.getBirthday()),
                () -> assertTrue(person.getBirthday() instanceof String),
                () -> assertNotNull(person.getBirthday()),
                () -> assertFalse(person.getBirthday().isEmpty()),
                // aRandomValue
                () -> assertTrue(aRandomValue instanceof Integer),
                () -> assertFalse(aRandomValue <= 0),
                () -> assertNotNull(aRandomValue)
        );
    }

}
````

Next page for getters and setters