<h1>POJO-like</h1>

This is an example of POJO-like class:

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

This is a POJO-like class for creating a Person's indentity. This can be imagined as a Model for a database, or a structure for a Controller that requires to do something with it. 

You got private values to be setted with a constructor, getters, setters and one last method inserted into the constructor for set up a
sort of unique value for that specific Person.

Unit Testing a POJO-like class is simple, but you have to write many lines of code; usually this is the first kind of object to test in a project, not only because they are really a lot in a codebase, but because they are <i>easy</i> to assert and useful for achieving a good code coverage percentage.