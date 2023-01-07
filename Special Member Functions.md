# Special Member Functions

### General
  | Description | Link| 
  |---------------|-----------------|
  | Msft  | [Link]( https://learn.microsoft.com/en-us/cpp/cpp/special-member-functions?view=msvc-170)            |
  | IBM  | [Link](https://www.ibm.com/docs/en/zos/2.4.0?topic=reference-special-member-functions-c-only )            |
  
*  **General**
   *  The special member functions are class (or struct) member functions that, in certain cases, the compiler automatically generates for you.
   *  These functions are
      *  default constructor
      *  destructor
      *  copy constructor
      *  copy assignment operator
      *  move constructor
      *  move assignment operator
  
    *  If your class does not define one or more of the special member functions, then the compiler may implicitly declare and define the functions that are used.
    *  The compiler does not generate functions if they are not needed.
  
*  **Usage:**

   * `default`
     * You can explicitly declare a default special member function by using the = default keyword.
     * This causes the compiler to define the function only if needed, in the same way as if the function was not declared at all.
  
   * `delete`
     *  To explicitly prevent automatic generation of a special member function, you can declare it as deleted by using the = delete keyword.

* **Restrictions**

  * The compiler generates a default constructor, a constructor that takes no arguments, only when you have not declared any other constructor.
  * If you have declared only a constructor that takes parameters, code that attempts to call a default constructor causes the compiler to produce an error message.