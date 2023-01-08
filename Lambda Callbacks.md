# Lambdas and Callbacks

## Lambdas

### Links

| Description   | Link                                                                                                                                                              |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Msft          | [Link](https://learn.microsoft.com/en-us/cpp/cpp/lambda-expressions-in-cpp?view=msvc-170)                                                                         |
| Doc           | [Link](https://docs.google.com/presentation/d/1MWbu-UozNpDi2_u-tkGVqo6zRK5VTdBDSUBmCJUZuSg/edit?resourcekey=0-B-33QLc-2_gw0hx2oUHhmA#slide=id.g1c5cc391dd_2_295 ) |
| Youtube Video | [Link]( https://www.youtube.com/watch?v=zGPjSeMYFwQ&t=1413s)                                                                                                      |
  


### General
*   It is a convenient way of defining an anonymous function object (a closure) right at the location where it's invoked or passed as an argument to a function
*   Typically lambdas are used to encapsulate a few lines of code that are passed to algorithms or asynchronous functions
*   MSFT Link is very good

### Parts of a Lambda

* Image
    ![Image](https://drive.google.com/uc?id=18vW5rDCYF6NQ8z_WqOkNqg66mLFWOL0Q)

### Capture Clause

*   It specifies which variables are captured, and whether the capture is by value or by reference
*   Google Style guide is not happy about default capture by reference. 
*   Variables that have the ampersand `&` prefix are accessed by reference and variables that don't have it are accessed by value.
*   An empty capture clause, `[ ]`, indicates that the body of the lambda expression accesses no variables in the enclosing scope
*   Only variables that are mentioned in the lambda body are captured when a capture-default is used
  
*   **Restrictions**
    *   If a capture clause includes a capture-default `&`, then no identifier in a capture of that capture clause can have the form `&`identifier.
    *   If the capture clause includes a capture-default `=`, then no capture of that capture clause can have the form `=` identifier.
  
*   **Some Examples**
    ```
        struct S { void f(int i); };

        void S::f(int i) {
            [&, i]{};      // OK
            [&, &i]{};     // ERROR: i preceded by & when & is the default
            [=, this]{};   // ERROR: this when = is the default
            [=, *this]{ }; // OK: captures this by value. See below.
            [i, i]{};      // ERROR: i repeated
        }
    ```

### Parameter List

*   A parameter list is optional and in most aspects resembles the parameter list for a function.
*   In C++14, if the parameter type is generic, you can use the `auto` keyword as the type specifier. 
  
    ```
    // Here, we are telling the compiler to deduce the value of the `j` from the program
    // In a normal function, we cannot write like this
    [&, i](auto j) { ++x; return j == (i + x); }

    ```

    Under the hood, this is deduced from the auto using a template. 

### Return Type

*   The return type of a lambda expression is automatically deduced. You don't have to use the auto keyword unless you specify a trailing-return-type. 
*   You can omit the return-type part of a lambda expression
    *   If the lambda body contains just one return statement.
    *   If the expression doesn't return a value.