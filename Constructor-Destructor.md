# Constructor Destructor

[Constructor Destructor](./docs/Constructor%20Destructor.pdf)



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
  
    *   Construction and Assignment Pair
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
 
    *   Copy and Move Pair
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