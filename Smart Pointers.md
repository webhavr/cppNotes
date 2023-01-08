# Smart Pointers

### PDF
[Smart Pointer](./docs/Smart%20Pointers%20C++.pdf)

### Chromium Talk

 | Description | Link                                                                                          |
 | ----------- | --------------------------------------------------------------------------------------------- |
 | Video       | [Link](https://www.youtube.com/watch?v=MpwbWSEDfjM )                                          |
 | Doc         | [Link](https://docs.google.com/document/d/1VRevv8JhlP4I8fIlvf87IrW2IRjE0PbkSfIcI6-UbJo/edit ) |
  
  

### What can go wrong

*   Pointers are a common cause of security problems in Chrome
*   The most common type is a use-after-free (UaF). You have a pointer to an object (i.e. a goat), that object gets deleted, then something else (a cow) gets allocated in the same place. The pointer still thinks it’s pointing to a goat, and that misunderstanding can be used by attackers

### Should you ever use a native pointer?

*   In C++, a native pointer looks like Foo*
*   You can avoid use-after-frees by never using native pointers, but there are performance trade-offs, so this isn’t always feasible
*   The style guide says raw pointers (and references) are ok for giving access to an object, e.g. passing as a function parameter
*   You should not use native pointers in the following cases:
    *   As fields in objects, since these are the ones that tend to lead to use-after-frees
    *   To express ownership - when ownership gets passed around, this is very difficult to do correctly. If you have to do this, use a std::unique_ptr

## Types of smart pointers and pointer like objects

### `std::unique_ptr<Foo>`

*   This expresses unique ownership to an object in the heap
*   Holds your pointer and deletes it when it goes out of scope
*   Can’t be copied, because it’s unique ownership, but it can be moved
*   Is the size of a pointer, the object it points to lives elsewhere in the heap

### `absl::optional<Foo>`

*   Use when you want to return a value when 
    *   either there’s no value to give back
    *   or, in case of an error

*   **Idea**
    *   This is more clear than using a native pointer and bool to express the same thing

*   This type is a pointer-like object because it provides the -> and * operators, even though it holds an object inside of it by value, rather than a pointer
  
*   **Size:**
    *   That means the object is held in the space allocated for the optional
    *   the size of the optional is the size of the thing it’s holding, plus a flag.

*   **Comparison with the `std::unique_ptr<>`**:
    
    *   Similar to a std::unique_ptr because it uniquely holds that object
    
    *   **Dissimilar:**
        *   It is copyable if the object inside is copyable, while `std:unique_ptr` is non-copyable
        *   Doesn’t need a heap allocation, the object in the optional and the optional itself is all on the stack.
        *   `absl::optional` CANNOT be forward declared since have to include the type in the optional. A forward declaration isn’t enough since the optional needs to know the size of the object


		
		
		
