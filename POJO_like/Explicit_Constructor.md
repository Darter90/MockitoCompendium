<h1>Explicit Constructor</h1>

Let's take with this example:

````
import java.util.ArrayList;
import java.util.Date;
import java.util.List;

public class Person {

    // some properties
    private String name;
    private String surname;
    private Integer dateSubscription;
    private Integer age;
    private String birthday;
    private List<Integer> personCode;

    // constructor
    Person(String name, String surname, Date dateSubscription, Integer age, String birthday, Integer aRandomValue) {
        this.name = name;
        this.surname = surname;
        this.dateSubscription = dateSubscription.getDate();
        this.age = age;
        this.birthday = birthday;
        this.personCode = setCode(name, surname, aRandomValue);
    }

    /* getters and setters */
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getSurName() {
        return surname;
    }

    public void setSurName(String surname) {
        this.surname = surname;
    }

    public Integer getDateSubscription() {
        return dateSubscription;
    }

    public void setDateSubscription(Date dateSubscription) {
        this.dateSubscription = dateSubscription.getDate();
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public String getBirthday() {
        return birthday;
    }

    public void setBirthday(String birthday) {
        this.birthday = birthday;
    }

    /* set a name code */
    public String getCode() {
        return personCode.toString();
    }

    public List<Integer> setCode(String name, String surName, Integer aRandomValue) {

        personCode = new ArrayList<Integer>();
        char[] toElaborate = (name + surName).toCharArray();

        for (char aChar : toElaborate) {
            int value = aChar;
            personCode.add(value);
        }

        personCode.add(aRandomValue);

        return personCode;

    }

}
````

You have a POJO-like class for a Person. This can be imagined as a Model for a database, or a structure for a Controller that requires to do something with it. 

You got private values to be setted with a constructor, getters and setters and one last method inserted into the constructor for set up a
sort of unique value for that specific Person.

Unit Testing a POJO like this is simple, but you have to write many lines of code. Usually this is the first kind of object to test, not only because they are really a lot in a codebase, but because they are <i>easy</i> to assert.

---

<h1>Let's start</h1>

<h4>The explicit constructor</h4>

Since you have an explicit constructor, you cannot use @Spy annotation and @BeforeEach setUp() syntax. <b>This is a limitation of Mockito</b>. 
Current Best Practice suggest to create a method for unit testing the constructor, with external properties to assign to it. If needed, just copy-paste it into the other methods to create an instance of the object.

Usually this is not a good practice in software development, since 
<i>you must not repeat yourself</i>...but in Unit Test you need to setting up every test as an entity completely separated from the rest of the code.
And you must have many fields for Unit Test if you want to play with the code and test particular situations.


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
<li>if setted values are what we suppose they are.</li>
</ul>


let's make an example with just the name value:

````
// constructor

    assertEquals(name, person.getName(), "name value");
    assertTrue(person.getName() instanceof String);
    assertNotNull(person.getName());
````

As you can see, we can use the getter to make the unit test more complete and usefull.

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
        // surname
        (...)
        );

````

Remember to use good comments to better explain and divide every section of the Unit Test

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
                () -> assertEquals(name, person.getName(), "name value must be equal"),
                () -> assertTrue(person.getName() instanceof String, "name must be instance of String"),
                () -> assertNotNull(person.getName(), "name must not be null"),
                // surname
                () -> assertEquals(surname, person.getSurName(), "surname value must be equal"),
                () -> assertTrue(person.getSurName() instanceof String, "surname must be instance of String"),
                () -> assertNotNull(person.getSurName(), "surname must not be null"),
                // dateSubscription
                () -> assertEquals(dateSubscription.getDate(), person.getDateSubscription(), "dateSubscription value must be equal"),
                () -> assertTrue(person.getDateSubscription() instanceof Integer, "dateSubscription must be instance of Integer"),
                () -> assertFalse(person.getDateSubscription() <= 0, "dateSubscription must not be 0 or less"),
                () -> assertNotNull(person.getDateSubscription(), "dateSubscription must not be null"),
                // age
                () -> assertEquals(age, person.getAge(), "age value must be equal"),
                () -> assertTrue(person.getAge() instanceof Integer, "age must be instance of Integer"),
                () -> assertNotNull(person.getAge(), "age must not be null"),
                // birthday
                () -> assertEquals(birthday, person.getBirthday(), "birthday value must be equals"),
                () -> assertTrue(person.getBirthday() instanceof String, "birthday must be instance of String"),
                () -> assertNotNull(person.getBirthday(), "birthday must not be null"),
                // aRandomValue
                () -> assertTrue(aRandomValue instanceof Integer, "aRandomValue must be instance of Integer"),
                () -> assertFalse(aRandomValue <= 0, "aRandomValue must not be 0 or less"),
                () -> assertNotNull(aRandomValue, "aRandomValue must not be null")
        );
    }

}
````

Next page for getters and setters