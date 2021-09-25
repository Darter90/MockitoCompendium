
<h1> What is Unit Testing </h1>

Unit Test means: <b>make sure the class or method you're working on right now works correctly</b>.

Unit Test must regards only the <i>behaviour</i> of a class or a method, in complete <i>isolation</i>. <br />You have not to work with business logic (this is Test Driven Development field...), or deal with databases and other instrument.

Last but not least, Unit Test MUST NOT contain any iterational or conditional structure, like if-else, for-loop, do-while, try-catch... 
<br />
This because there are good Unit Testing Libraries for that and because an Unit Test have to be readable and easy modificable by you and other developers who just want to make experiments.

Iterational and conditional structures can be used in Test Driven Development instead.

---

<h1>The reality</h1>

In reality, <b>we have to deal with codes that cannot be fully isolated</b>. Only POJO-like object can be isolated, or the most simple classes. <br />Usually, we have to deal with <b>Integration test</b>: an integration test, is a code where classes and methods cannot be fully contained inside the class or method itself; indeed, you have to deal with methods that calls other methods or require objects outside of the class or method under testing.

Mockito comes to help us with this.