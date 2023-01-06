# Frequent

This file carries the most frequent things in CPP

### Access Specifiers

*   In C++, there are 3 access specifiers:

*   **Private inheritance:**

  | Accessibility | Private Members | Protected Members        | Public Members |
  |---------------|-----------------|--------------------------|----------------|
  | Base Class    | Yes             | Yes                      | Yes            |
  | Derived Class | No              | Yes (as private members) | Yes            |

*   **Protected inheritance   :**

  | Accessibility | Private Members | Protected Members | Public Members             |
  |---------------|-----------------|-------------------|----------------------------|
  | Base Class    | Yes             | Yes               | Yes                        |
  | Derived Class | No              | Yes               | Yes(inherited as protected |
  |               |                 |                   | variables)                 |

*   **Public inheritance:**

  | Accessibility | Private Members | Protected Members | Public Members |
  |---------------|-----------------|-------------------|----------------|
  | Base Class    | Yes             | Yes               | Yes            |
  | Derived Class | No              | Yes               | Yes            |


### Const

*  **References**

  | Description | Link| 
  |---------------|-----------------|
  | Msft  | [Link](https://learn.microsoft.com/en-us/cpp/cpp/const-cpp?view=msvc-170 )            |
  


*  **Values:**

   * **Variable**
        + The `const` keyword specifies that a variable's value is constant and tells the compiler to prevent the programmer from modifying it.


   * **Pointer**
        + The `const` keyword can also be used in pointer declarations.
        + A pointer to a variable declared as `const` can be assigned only to a pointer that  is also declared as `const`.


   * **Object**
        + For objects that are declared as const, you can only call constant member functions. The compiler ensures that the constant object is never modified.


* **Member Functions:**

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

*  **References**

  | Description | Link| 
  |---------------|-----------------|
  | Msft  | [Link](https://learn.microsoft.com/en-us/cpp/cpp/constexpr-cpp?view=msvc-170 )            |