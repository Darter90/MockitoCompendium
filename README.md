

<h1>Welcome</h1>

This is a compendium for Java Developer and Unit Testers that have to work with Mockito and jUnit in their projects. It is not intended as a step-by-step guide, but as a reference for skilled developers and tester, looking for a pathway on <i>how the things must be done</i>.


This documentation is developed with <a href="https://docsify.js.org/#/">Docsify</a> and his plugins ecosystem:


* <b>moon/sun button</b>: switch between light and dark mode;
* <b>left side</b>: side navigation bar with toggle hamburger button;
* <b>bottom</b>: navigate between pages, credits.

---

<h1>jUnit</h1>

<a href="https://junit.org/junit5/">jUnit</a> is a simple framework to write repeatable tests. It is an instance of the xUnit architecture for unit testing frameworks.

With this framework you can prepare the field for a Unit Test case in Java and access to the Assertion methods.

You must have jUnit5 installed via Maven or Grandle in your project to use Mockito;
and Version 5 of jUnit is incompatible with the old jUnit4. <br /> 
If somebody in your team needs to use jUnit4 for any reason, you must add a plugin named <a href="https://mvnrepository.com/artifact/org.junit.vintage/junit-vintage-engine">jUnit Vintage Engine</a>, with Maven or Grandle. This plugin creates a compatibility layer from jUnit4 to jUnit5, nothing more nothing less.

---

<h1>Mockito</h1>

<a href="https://site.mockito.org/">Mockito</a> is a mocking framework that tastes really good. It lets you write beautiful tests with a clean & simple API. <br /> Mockito doesn’t give you hangover, because the tests are very readable and they produce clean verification errors. 

With Mockito, you can create <b>mocks</b> in runtime and mimate objects, methods and behaviours during code execution. You need to add this framework via Maven or Grandle after installing jUnit5.

---

<h1>Other Documentations</h1>

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
