# Frequent

This file carries the most frequent things in CPP

### Access Specifiers

*   In C++, there are 3 access specifiers:

*   **Private inheritance:**

  | Accessibility | Private Members | Protected Members        | Public Members |
  | ------------- | --------------- | ------------------------ | -------------- |
  | Base Class    | Yes             | Yes                      | Yes            |
  | Derived Class | No              | Yes (as private members) | Yes            |

*   **Protected inheritance   :**

  | Accessibility | Private Members | Protected Members | Public Members             |
  | ------------- | --------------- | ----------------- | -------------------------- |
  | Base Class    | Yes             | Yes               | Yes                        |
  | Derived Class | No              | Yes               | Yes(inherited as protected |
  |               |                 |                   | variables)                 |

*   **Public inheritance:**

  | Accessibility | Private Members | Protected Members | Public Members |
  | ------------- | --------------- | ----------------- | -------------- |
  | Base Class    | Yes             | Yes               | Yes            |
  | Derived Class | No              | Yes               | Yes            |


### Const

  | Description | Link                                                                       |
  | ----------- | -------------------------------------------------------------------------- |
  | Msft        | [Link](https://learn.microsoft.com/en-us/cpp/cpp/const-cpp?view=msvc-170 ) |
  


*  **Usage for Values:**

   * **Variable**
        + The `const` keyword specifies that a variable's value is constant and tells the compiler to prevent the programmer from modifying it.


   * **Pointer**
        + The `const` keyword can also be used in pointer declarations.
        + A pointer to a variable declared as `const` can be assigned only to a pointer that  is also declared as `const`.


   * **Object**
        + For objects that are declared as const, you can only call constant member functions. The compiler ensures that the constant object is never modified.


* **Usage for Member Functions:**

   * Declaring a member function with the const keyword specifies that the function is a "read-only" function that doesn't modify the object for which it's called. 
   * A constant member function:
     - can't modify any non-static data members
     - can't call any member functions that aren't constant.
   * To declare a constant member function, place the `const` keyword after the closing parenthesis of the argument list.
   * The `const` keyword is required in both the declaration and the definition.


* **General**

   * For a non-constant object, you can call either constant or non-constant member functions. 

* **Restrictions:**

   * You can't declare constructors or destructors with the `const` keyword.


### Constexpr

  | Description | Link                                                                           |
  | ----------- | ------------------------------------------------------------------------------ |
  | Msft        | [Link](https://learn.microsoft.com/en-us/cpp/cpp/constexpr-cpp?view=msvc-170 ) |


### Override

  | Description | Link                                                                                |
  | ----------- | ----------------------------------------------------------------------------------- |
  | Msft        | [Link](https://learn.microsoft.com/en-us/cpp/cpp/override-specifier?view=msvc-170 ) |
  | CPP Ref     | [Link](https://en.cppreference.com/w/cpp/language/override )                        |
  

*  **Usage:**

   * You can use the `override` keyword in Derived Class as well as Base Class to designate member functions that override a virtual function in a base class. 
   *  The example in the MSFT reference link clearly describes it.  
   *  When you use override, the compiler generates errors instead of silently creating unintended new member functions.

* **Restrictions**

  * `override` specifier ensures that the function is virtual and is overriding a virtual function from a base class. A compile-time error is generated if this is not true. 
  *  Meaning we CANNOT override a non-virtual method. 


### Final

  | Description | Link                                                                             |
  | ----------- | -------------------------------------------------------------------------------- |
  | Msft        | [Link](https://learn.microsoft.com/en-us/cpp/cpp/final-specifier?view=msvc-170 ) |
  
  

*  **Usage:**

   * **Virtual Functions**
        + You can use the `final` keyword to designate virtual functions that cannot be overridden in a derived class.

   * **Class**
        + You can also use it to designate classes that cannot be inherited.

* **Restrictions**

  * Attempting to override a `final` virtual function or a base class would result in a compile time error. 


### Virtual

  | Description | Link                                                                               |
  | ----------- | ---------------------------------------------------------------------------------- |
  | Msft        | [Link](https://learn.microsoft.com/en-us/cpp/cpp/virtual-functions?view=msvc-170 ) |
  
  

*  **General:**

   * A virtual function is a member function that you expect to be redefined in derived classes.
   * Virtual functions ensure that the correct function is called for an object, regardless of the expression used to make the function call. 

* **Usage**

  * When you refer to a derived class object using a pointer or a reference to the base class, you can call a virtual function for that object and execute the derived class's version of the function
  * The function from the derived class is invoked for objects of the derived class, even if it is called using a pointer or reference to the base class.
  * If a class is declared that does not provide an overriding implementation of the Base Class function, the default implementation from the base class is used.
  
* **Restrictions**

  * Functions in derived classes override virtual functions in base classes only if their type is the same. A function in a derived class cannot differ from a virtual function in a base class in its return type only; the argument list must differ as well.
  * Because virtual functions are called only for objects of class types, you cannot declare global or static functions as virtual.


### Static

  | Description | Link                                                                                |
  | ----------- | ----------------------------------------------------------------------------------- |
  | Msft        | [Link](https://learn.microsoft.com/en-us/cpp/cpp/static-members-cpp?view=msvc-170 ) |
  | IBM         | [Link](https://www.ibm.com/docs/en/zos/2.4.0?topic=only-static-data-members-c )     |
  

* Classes can contain:
  * Static Data Members
  * Static Member Functions 

* **Static Data Members**

  * When a data member is declared as static, only one copy of the data is maintained for all objects of the class.
  * Static data members are not part of objects of a given class type. They belong to the whole class. 
   
  * **Definition**
    * Declaration of a static data member is not considered a definition. 
    * The data member is declared in class scope, but definition is performed  at file scope. 
  
  * **Usage**
    * Static data members can be referred to without referring to an object of class type
    * For the static member to exist, it is not necessary that any objects of the class type exist.
  
  * **Restrictions**
    * A static data member can be of any type except for void or void qualified with const or volatile
    * You cannot declare a static data member as mutable.
    * You can only have one definition of a static member in a program.

* **Static Member Functions**
  
  * **Definition** 
    * Unlike static member data, static member functions can be defined in class scope.  
  
  **Usage**
    * Like static data members, you may access a static member function f() of a class A without using an object of class A.
    * For the static member function to exist, it is not necessary that any objects of the class type exist.

  * **Restrictions**
    * You cannot have static and nonstatic member functions with the same names and the same number and type of arguments.
    * A static member function does not have a this pointer, since it is not associated with any class object
    * You can only have one definition of a static member in a program.
    * A static member function can access only the names of static members, enumerators, and nested types of the class in which it is declared.

  