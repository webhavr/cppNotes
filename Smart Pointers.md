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

*   CPP Ref Link - [Link](https://www.cppstories.com/2018/05/using-optional/)

*   Use when you want to return a value when 
    *   either there’s no value to give back
    *   or, in case of an error
    *   By adding the boolean flag to other types, you can achieve a thing called “nullable types”. The flag is used to indicate whether the value is available or not.

*   **Idea**
    *   This is more clear than using a native pointer and bool to express the same thing

*   **Concept**
    *   This type is a pointer-like object because it provides the -> and * operators, even though it holds an object inside of it by value, rather than a pointer
  
*   **Size:**
    *   That means the object is held in the space allocated for the optional
    *   the size of the optional is the size of the thing it’s holding, plus a flag.

*   **Comparison with the `std::unique_ptr<>`**:
    
    *   Similar to a std::unique_ptr because it uniquely holds that object
    
    *   **Dissimilar:**
        *   It is copyable if the object inside is copyable, while `std:unique_ptr` is non-copyable
        *   Doesn’t need a heap allocation, the object in the optional and the optional itself is all on the stack.
        *   `absl::optional` CANNOT be used to forward declare since have to include the type in the optional. A forward declaration isn’t enough since the optional needs to know the size of the object


### `base::scoped_refPtr<Foo>`

*   Use carefully! Refcounting is hard!
*   It’s an owning smart pointer, so owns a pointer to something allocated in the heap
  
*   **Chrome’s equivalent of `std::shared_ptr`:**

    *   Gives shared ownership of the underlying object, since it can be copied.
    *   When all `scoped_refptrs` pointing to the same object are gone, that object gets destroyed

*   **Differences with the `std::shared_ptr`:**

    *   `scoped_refptr` requires the ref counting happens in the object, where in shared_ptr it happens outside the object.
    * The ThreadSafe part of RefCountedThreadSafe is important because if there are `scoped_refptrs` to the same object on different threads, they could race and be wrong which can lead to a double free. With RefCountedThreadSafe, you get atomic refcounting, which makes it thread safe

### `base::WeakPtr<Foo>` and `base::WeakPtrFactory<Foo>`

*   Main purpose is for asynchronous work, which is most work in Chrome
*   The issue with async work is that there isn’t a continuous stack frame. You can do work on a stack frame, you go away for a while and when you come back, the state of that stack frame is gone. 
*   Any state you want to keep across tasks needs to be bound with the task, but that’s risky with pointers, as the use-after-free 
*   `WeakPtrFactory` provides a side channel that watches the object and tells `WeakPtr` if the underlying object is still there.
*   `WeakPtrFactory` watches the object and when the object is destroyed, the weakptrfactory inside of it is destroyed, and marks a bit
*   When the asynchronous task comes back, and the `Weakptr` inside it comes back, if the `Weakptrfactory` is still present, it can continue the work, else not. 

### `base::SafeRef<Foo>`

*   Use when you want to guarantee that Foo exists and is valid
*   If the assumption that the object is valid is broken, then the process is guaranteed to terminate safely and make a crash report. That’s not ideal, but it’s better than a security bug and ensures we hear about the bug.
*   Makes human understanding easier because it reduces possible code branches. Instead of Foo being either null or non-null, it’s always non-null and reduces the number of states your code can be in. Always prefer fewer states.
*   Built on top of WeakPtr, so it does require a WeakPtrFactory to be present, but its purpose is not the same. 

*   **Differences between `SafeRef` and `WeakPtr`**
    *   `SafeRef` can't be null
    *   Can't observe whether the object is alive or not
  
*   **Advantage of `SafeRef` over `WeakPtr`**
    *   Gives the option to guarantee that the pointer is valid here, and there is no need to check it like a weak pointer. This helps to reduce the total number of states a program can be in
    *   Even if it is not valid, it will not generate a security bug and the crash should be fixed somewhere else



### `raw_ptr<Foo>`
*   Use when you have a pointer as a class member (unless one of the other types has features you’re looking for)
Keeps a reference count in the memory allocator (Chrome’ has its own called PartitionAlloc)
*   If the object is deleted, the allocator will ‘poison’ the memory that object occupied and keep the memory around so it’s not reused, while there is a raw_ptr pointing to it. This reduces the risk/impact of a use-after-free bug.
*   These currently aren’t turned on outside the browser process, but you should use them any time you have class members in the browser process, including in code that is used in multiple processes.
*   These have weak refcounting, unlike scoped_refptr which is strong refcounting
*   A strong refcount means the refcount owns the object. When the count goes to 0, the object gets deleted 
*   This weak refcount keeps the memory allocated, but doesn’t keep the object in the memory alive, so they don’t affect the behaviour of the code
These can exist at the same time (e.g. a raw_ptr to an object owned by scoped_refptr).
	
		
		
