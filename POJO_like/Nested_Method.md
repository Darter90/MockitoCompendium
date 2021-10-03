
<h1>Nested Method</h1>

Into the class constructor we have a nested method: <b>setCode()</b>. This method is an example of Integration test nested into the class.

The best approach in this case, is to Unit Test the method separately to understaand is behavior and then return into the constructor in a second moment.

Since we have a private property that change into a String, we need
to access it with a <a href="https://darter90.github.io/MockitoCompendium/#/Private_fields_and_Static_methods/Reflections">Reflection</a> and use it for
our assertions before it becames a String.
I'll write about Reflection in the next test case. For now take it as it is.

In this case the situation is not so complicated, but in other kinds of codes you may have to Unit Test hundreds of lines of code before reach a section with a nested method. In that case, you must be patient and be caution, since every previous line of code is closely related to the nested method under test.

In any case, a good idea is to use the debugger of the IDE and track every step of the execution.

This is the unit test of that method:

````
    @Test
    void getCode_and_setCode() throws NoSuchFieldException {

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

        // old Code for future assert
        String oldCode = person.getCode();

        // reflecting personCode field
        Field privatePersonCode = Person.class.getDeclaredField("personCode");
        privatePersonCode.setAccessible(true);

        // new values for test
        String anotherName = "Frank";
        String anotherSurname = "McKenzy";
        Integer anotherRandomValue = 487;

        // setting value
        person.setCode(anotherName, anotherSurname, anotherRandomValue);

        /* Assert */
        assertAll(
                "personCode",
                () -> assertEquals(privatePersonCode.get(person).toString(), person.getCode(), "anotherPersonCode must be equals to personCode"),
                () -> assertNotEquals(privatePersonCode.get(person).toString(), oldCode, "old personCode is no more"),
                () -> assertTrue(privatePersonCode.get(person) instanceof ArrayList, "personCode must be instance of ArrayList"),
                () -> assertFalse(person.getCode().isEmpty(), "personCode must not be an empty String")
        );
    }
````

And this is the final test case of this class:

````
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.junit.jupiter.MockitoExtension;

import java.lang.reflect.Field;
import java.util.ArrayList;
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
    void constructor() {

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
                () -> assertFalse(person.getName().isEmpty(), "name is not an empty String"),
                // surname
                () -> assertEquals(surname, person.getSurName(), "surname value must be equal"),
                () -> assertTrue(person.getSurName() instanceof String, "surname must be instance of String"),
                () -> assertNotNull(person.getSurName(), "surname must not be null"),
                () -> assertFalse(person.getSurName().isEmpty(), "surname is not an empty String"),
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
                () -> assertFalse(person.getBirthday().isEmpty(), "birthday is not an empty String"),
                // aRandomValue
                () -> assertTrue(aRandomValue instanceof Integer, "aRandomValue must be instance of Integer"),
                () -> assertFalse(aRandomValue <= 0, "aRandomValue must not be 0 or less"),
                () -> assertNotNull(aRandomValue, "aRandomValue must not be null")
        );
    }

    @Test
    void getName_and_setName() {

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

        // new name value
        String anotherName = "another name";

        // setting value
        person.setName(anotherName);


        /* Assert */

        assertAll(
                "name",
                () -> assertEquals(anotherName, person.getName(), "name must be equal to anotherName"),
                () -> assertNotEquals(name, person.getName(), "old name is no more"),
                () -> assertTrue(person.getName() instanceof String, "name must be instance of String"),
                () -> assertNotNull(person.getName(), "name must not be null"),
                () -> assertFalse(person.getName().isEmpty(), "name is not an empty String")
        );
    }

    @Test
    void getSurName_and_setSurName() {

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

        // new surname value
        String anotherSurname = "another surname";

        // setting value
        person.setSurName(anotherSurname);


        /* Assert */

        assertAll(
                "surname",
                () -> assertEquals(anotherSurname, person.getSurName(), "surname must be equal to anotherSurname"),
                () -> assertNotEquals(surname, person.getSurName(), "old surname is no more"),
                () -> assertTrue(person.getSurName() instanceof String, "surname must be instance of String"),
                () -> assertNotNull(person.getSurName(), "surname must not be null"),
                () -> assertFalse(person.getSurName().isEmpty(), "surname is not an empty String")
        );
    }

    @Test
    void getDateSubscription_and_setDateSubscription() {

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

        // new dateSubscription value
        Date anotherDateSubscription = new Date();

        // setting value
        person.setDateSubscription(anotherDateSubscription);


        /* Assert */

        assertAll(
                "dateSubscription",
                () -> assertEquals(anotherDateSubscription.getDate(), person.getDateSubscription(), "dateSubscription must be equal to anotherDateSubscription"),
                () -> assertNotEquals(dateSubscription, person.getDateSubscription(), "old dateSubscription is no more"),
                () -> assertTrue(person.getDateSubscription() instanceof Integer, "dateSubscription must be instance of Integer"),
                () -> assertFalse(person.getDateSubscription() <= 0, "dateSubscription must not be 0 or less"),
                () -> assertNotNull(person.getDateSubscription(), "dateSubscription must not be null")
        );
    }

    @Test
    void getAge_and_setAge() {

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

        // new age value
        Integer anotherAge = 25;

        // setting value
        person.setAge(anotherAge);


        /* Assert */

        assertAll(
                "age",
                () -> assertEquals(anotherAge, person.getAge(), "age must be equals to anotherAge"),
                () -> assertNotEquals(age, person.getAge(), "old age is no more"),
                () -> assertTrue(person.getAge() instanceof Integer, "age must be instance of Integer"),
                () -> assertFalse(person.getAge() <= 0, "age must not be 0 or less"),
                () -> assertNotNull(person.getAge(), "age must be not null")
        );
    }

    @Test
    void getBirthday_and_setBirthday() {

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

        // new birthday value;
        String anotherBirthday = "25/12/1968";

        // setting value
        person.setBirthday(anotherBirthday);


        /* Assert */
        assertAll(
                "birthday",
                () -> assertEquals(anotherBirthday, person.getBirthday(), "birthday must be equals to anotherBirthday"),
                () -> assertNotEquals(birthday, person.getBirthday(), "old birthday is no more"),
                () -> assertTrue(person.getBirthday() instanceof String, "birthday must be instance of String"),
                () -> assertNotNull(person.getBirthday(), "birthday must be not null"),
                () -> assertFalse(person.getBirthday().isEmpty(), "birthday is not an empty String")
        );
    }

    @Test
    void getCode_and_setCode() throws NoSuchFieldException {

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

        // old Code for future assert
        String oldCode = person.getCode();

        // reflecting personCode field
        Field privatePersonCode = Person.class.getDeclaredField("personCode");
        privatePersonCode.setAccessible(true);

        // new values for test
        String anotherName = "Frank";
        String anotherSurname = "McKenzy";
        Integer anotherRandomValue = 487;

        // setting value
        person.setCode(anotherName, anotherSurname, anotherRandomValue);

        /* Assert */
        assertAll(
                "personCode",
                () -> assertEquals(privatePersonCode.get(person).toString(), person.getCode(), "anotherPersonCode must be equals to personCode"),
                () -> assertNotEquals(privatePersonCode.get(person).toString(), oldCode, "old personCode is no more"),
                () -> assertTrue(privatePersonCode.get(person) instanceof ArrayList, "personCode must be instance of ArrayList"),
                () -> assertFalse(person.getCode().isEmpty(), "personCode must not be an empty String")
        );
    }

}
````