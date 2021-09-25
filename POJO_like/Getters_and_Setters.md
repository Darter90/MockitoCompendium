<h1>Getters and Setters</h1>

Unit testing getters and setters is pretty much simple:

let's make an example for the name value:
````
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
                () -> assertNotNull(person.getName(), "name must not be null")
        );

    }
````

Repeat more or less the same assertions in all the other methods.<br />
This is the test case right now:

````

````