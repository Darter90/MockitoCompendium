<h1>doThrows</h1>

With Mockito you can call Exceptions by yourself, by using the when/thenReturn syntax and the <b>doThrows</b> method. This instruction is really usefull, since you can use it to call an Exception in a <a href="https://en.wikipedia.org/wiki/Black-box_testing">black box test</a>.

For example:

```
// other stuffs from the servlet...

DispatcherClass dispatcher = requestObject.getRequestDispatcher(resourceObject, optionsObject);
        try {
            if (dispatcher != null) {
                dispatcher.include(requestObject, responseObject);
            } else {
                logger.error("dispatcher is null");
            }
        } catch (Exception e) {
            logger.error("something else is appened: " + e);
        }
```

This snippet comes from a servlet. You don't know anything about it, the back-end, how it works... for <i>reasons</i> you are not allowed to know something about it. And your job, is to call that exception for a Unit Test. Here comes the doThrows method from Mockito:


```
// other stuffs from the test...

doThrow(new ServletException("fake error generate with Mockito")).when(dispatcher).include(requestObject, responseObject);
```

That's all. <b>Simple and clear</b>.