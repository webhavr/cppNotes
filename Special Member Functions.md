# Special Member Functions

### General
  | Description | Link                                                                                           |
  | ----------- | ---------------------------------------------------------------------------------------------- |
  | Msft        | [Link]( https://learn.microsoft.com/en-us/cpp/cpp/special-member-functions?view=msvc-170)      |
  | IBM         | [Link](https://www.ibm.com/docs/en/zos/2.4.0?topic=reference-special-member-functions-c-only ) |
  
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

### Explicit Default and Delete

* Explicitly Defaulted and deleted functions give you explicit control over whether the special member functions are automatically generated.

* **Rules**
  * If any constructor is explicitly declared, then no default constructor is automatically generated.
  * If a virtual destructor is explicitly declared, then no default destructor is automatically generated.
  * If a move constructor or move-assignment operator is explicitly declared, then:
    * No copy constructor is automatically generated.
    * No copy-assignment operator is automatically generated.
  
### Explicit Defaulted Functions:
*  You can default any of the special member functions:
   *  to explicitly state that the special member function uses the default implementation
   *  to define the special member function with a non-public access qualifier
   *  to reinstate a special member function whose automatic generation was prevented by other circumstances

### Deleted Functions
* You can delete special member functions as well as normal member functions and non-member functions to prevent them from being defined or called.
* Deleting of special member functions provides a cleaner way of preventing the compiler from generating special member functions that you don't want.


