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



		
		
		
