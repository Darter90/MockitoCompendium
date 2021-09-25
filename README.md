

<h1>Welcome</h1>

This is a compendium for Java Developer and Unit Testers that have to deal with Mockito and jUnit in their projects. <br /> It is not intended as a user guide step-by-step, but as a reference for <i>how the things must be done</i>.


Is developed with <a href="https://docsify.js.org/#/">Docsify</a> and his plug-ins ecosystem without any in-depth knowledge:


* <b>moon/sun button</b>: switch between light and dark visualization mode
* <b>left side</b>: side navigation bar with toggle hamburger button 
* <b>bottom</b>: navigate between pages

---

<h1>jUnit</h1>

<a href="https://junit.org/junit5/">jUnit</a> is a simple framework to write repeatable tests. It is an instance of the xUnit architecture for unit testing frameworks.

With this framework you can prepare the field for a unit test case and access to the assertion methods

You must have jUnit5 in your project to use Mockito.
Version 5 of jUnit is incompatible with the old jUnit4. <br /> 
You need, in your project, a plug-in named <a href="https://mvnrepository.com/artifact/org.junit.vintage/junit-vintage-engine">jUnit Vintage Engine</a> to create a compatibility layer with jUnit4.

---

<h1>Mockito</h1>

<a href="https://site.mockito.org/">Mockito</a> is a mocking framework that tastes really good. It lets you write beautiful tests with a clean & simple API. <br /> Mockito doesn’t give you hangover because the tests are very readable and they produce clean verification errors. 

With Mockito you create mocks in runtime and mimate objects, methods and their behaviour during code execution.

---

<h1>Documentation</h1>



<ul>
<li>
<a href="https://junit.org/junit5/docs/5.7.2/api/org.junit.jupiter.api/org/junit/jupiter/api/Assertions.html">jUnit5 @Assertions</a>
</li>
<li>
<a href="https://devqa.io/junit-5-annotations/">
jUnit5 @Annotations</a>
</li>
<li>
<a href="https://www.baeldung.com/mockito-annotations">
Mockito @Annotations</a>
</li>
<li>
<a href="https://www.baeldung.com/mockito-series">
Mockito in general</a>
</li>

</ul>
