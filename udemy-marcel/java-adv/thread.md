## Thread safety
https://www.geeksforgeeks.org/java/thread-safety-and-how-to-achieve-it-in-java/

To ensure thread safety in Spring Boot and Java, use immutable objects, minimize shared state, and employ proper synchronization with keywords like synchronized or ReentrantLock. For Spring-specific concerns, use @Scope("prototype") for request-specific beans or ThreadLocal for thread-local data to prevent multiple threads from interfering with each other's state. 
General Java thread safety

•	Use immutable objects: Objects that cannot be changed after creation are inherently thread-safe, as there is no risk of concurrent modification. The String class is a common example.

•	Synchronize critical sections: Use the synchronized keyword on methods or blocks of code to ensure that only one thread can execute them at a time. This prevents race conditions on shared resources.

o	Best practice: Synchronize only the minimal code necessary to access the shared resource, not entire methods if possible.

o	Best practice: Avoid synchronizing on this or the class object, and instead use a dedicated private lock object to prevent unintended lock contention.

•	Use Java's concurrency utilities: The java.util.concurrent package provides thread-safe data structures and tools (like ConcurrentHashMap) and more advanced locking mechanisms (ReentrantLock) that can be more efficient than synchronized.

•	Minimize shared state: Design your classes to have as little shared mutable state as possible. Consider splitting a class into smaller, more focused components.

•	Understand visibility: Use the volatile keyword to ensure that changes to a variable are visible across all threads. However, volatile does not guarantee atomic operations, so it's often used in conjunction with other synchronization techniques. 


Spring Boot specific rules
•	Understand bean scopes: Spring's default Singleton scope is not inherently thread-safe; a single instance is shared across all requests.

•	Use @Scope("prototype"): For stateful beans that must be specific to a single request, use the "prototype" scope. Spring will create a new instance of the bean for each request, ensuring no state is shared between them.

•	Use ThreadLocal: For situations where you need to store data that is local to a single request/thread throughout the request lifecycle, use ThreadLocal. This is common for things like user context or request-specific data.

•	Use @Scope("request"): This scope is an alias for "prototype" and is often clearer when dealing with web-specific requests.

•	Be careful with transactions: When using multiple threads within a transaction, ensure the transaction context is propagated correctly to child threads. Database connections are not thread-safe, so proper synchronization or using a transaction-aware executor is necessary. 
•	
•	SerializationUtils.clone does not ensure thread safety. It creates a deep copy of the object, so modifications to the cloned object do not affect the original. However, if the original object is accessed or modified by multiple threads, external synchronization is still required to ensure thread safety. The method itself does not provide any locking or synchronization.

•	Immutable Objects: If the object within the singleton is itself immutable (its state cannot be changed after creation), then no additional synchronization is required for modifications to that object, as there are no modifications to protect. However, if the reference to the immutable object within the singleton can change, then that reference assignment still needs to be thread-safe.

In summary, while the singleton pattern itself ensures a single instance, protecting the mutable state of that instance from concurrent access by multiple threads requires explicit thread-safety mechanisms like synchronization or leveraging inherently thread-safe constructs like enums.


ThreadLocal ensures thread safety by providing each thread with its own independent, isolated copy of a variable. This mechanism avoids the potential for race conditions and data corruption that can occur when multiple threads access the same shared mutable data concurrently. 

How ThreadLocal Achieves Isolation

The core principle of ThreadLocal is data isolation, not synchronization. 

•	Per-Thread Storage: When a thread accesses a ThreadLocal variable using its get() or set() methods, it operates on a unique copy of the variable stored within a special map (ThreadLocalMap) inside the Thread object itself.

•	No Shared State: Since no two threads ever access the same memory location for the ThreadLocal variable's value, there is no shared mutable state to protect.

•	Avoiding Synchronization: This design eliminates the need for explicit synchronization mechanisms (like locks or the synchronized keyword), which can be complex to manage and introduce performance overhead. 

Analogy
Think of it like a shared class with a public static notebook (ThreadLocal object). Every "student" (thread) who uses the notebook gets their own personal, private copy of the pages inside it (the value). A change made by one student does not affect the pages of another student's copy, so they can all write simultaneously without interfering with each other. 

Key Benefits
•	Eliminates Race Conditions: By ensuring data is not shared, it inherently prevents the data corruption issues associated with concurrent access.

•	Improves Performance: It allows threads to operate in parallel without waiting for locks, which can increase application throughput and responsiveness.

•	Simplifies Code: It simplifies concurrent programming by allowing developers to maintain state within a thread without explicitly passing it through every method call or managing complex synchronization logic. 
Important Considerations

•	Memory Leaks: In long-running threads or thread pools, you must call the remove() method when the task is complete to prevent memory and resource leaks, as the value might persist with the thread even after the task finishes.

•	Object Mutability: While the ThreadLocal variable itself provides thread isolation, the object it holds might be mutable. If that mutable object is somehow leaked to and accessed by other threads, thread safety issues can still arise
<img width="468" height="648" alt="image" src="https://github.com/user-attachments/assets/d6500c31-efc8-4641-bf91-5ca3a2439c63" />
