# Constructor Destructor

[Constructor Destructor](./docs/Constructor%20Destructor.pdf)

Sample Image - ![Image](https://drive.google.com/uc?id=)

### Shallow and Deep Copy

*   **Main Points**

    *   **Shallow Copy**
        *   The two copies contain references to the same value in memory
        *   Faster
  
    *   **Deep copy**
        *   We copy each field from the original to the copy, but as we do so, we perform a deep copy of those instead of just copying the references
        *   Slower

*   **Shallow Copy**
*   ![Image](https://drive.google.com/uc?id=1Yg5QfEG_MX7TxkphsSORP68goeTn4wmK)

*   **Deep Copy**
*   ![Image](https://drive.google.com/uc?id=1jZxRBJJ4DUq_0BIXnQ0i-FAzSWuZzt0a)


### Copy and Move Operators

* Slides -  [Link](https://docs.google.com/presentation/d/1aW5UvMqr7nIeWDMVlXh0It4pit8MBMlwfp1OcgwH9Zg/edit?resourcekey=0-w-NXIU6M8dxTngKHJxPOgw#slide=id.gd01c13137e_2_38)

*  **Basics** 

    *   Constructors create an object and don't have a return type
    *   Assignment operations return an L-value reference to the object
  
    *   Copy takes L-value reference as an input
    *   Move takes R-value reference as an input

  
    ```
        C(const C&);  // “Copy constructor”
        C(C&&);       // “Move constructor”

        // Input on the Right and Output on the Left
        C& operator = (const C&);  // “Copy assignment”
        C& operator = (C&&);       // “Move assignment”
    ```

*   **Rule of Thumb - 1**
  
    *   For a Construction and Assignment Pair
    *   You should always do the same thing to each one of these 2 pairs - Construction and Assignment

    ```
        // Construction
        C(const C&) = delete;
        C(C&&) = default;
        
        // Assignment
        C& operator = (const C&) = delete;
        C& operator = (C&&) = default;

    ```

*   **Rule of Thumb - 2** 
 
    *   For a Copy and Move Pair
    *   You should always say what you are going to do with atleast one of them - either a copy pair, or a move pair
    *   If you say something about any one of the 2, the other pair is implicitly deleted.
    *   Frequent pattern in Chromium Code is to define the Copy Ops and don't say anything about the Move Ops, which means they are implicity deleted. 

    ```
        // Copy Ops

        C(const C&) = delete;              // Not copyable
        C& operator = (const C&) = delete; // (or movable)
    ```

    ```
        // Move Ops

        C(C&&) = default;               // Copyable
        C& operator = (C&&) = delete;   // Not Movable
    ```

*   **Example**
    *   Make the class copyable.

    ```
    C(const C&) = default;             // Copyable
    C& operator = (const C&) = default;
    // (Remember, move ops are implicitly deleted now!)
    ```

*   **Movable**
    *   Means - Copyable with an assumption
    *   Copyable, but assumes source won't be read again before destruction
    *   Source is not destructed on move, but the assumption is that source won't be used anymore later until its destruction. 
  
    *   Need of Moves - 

        1. Only one copy exists at any give time:
           *   A move only type like unique pointer ensures that only one copy of the object exists at any given time, and the old one gets destroyed. 
           *   Such object can only be moved and cannot be copied. 

        2.    Assuming the source is not usable anymore, some times the moves can be more efficient than the copy itself

*   **Suggestions**
    *   Use `= default`, but
        *   It uses shallow copy of pointer members