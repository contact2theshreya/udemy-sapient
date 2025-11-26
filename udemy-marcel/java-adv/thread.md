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

## Thread-Shreyansh notes extra

In singleton class -bill plough solution -

static inner class is loaded when it is used

With enum – constructors are private and one instance per jvm automatica;lly

With double locking – as  writing will happen to cache so memory issue can be there and singleton can be break coz read will happen from memory so we used volatile as it will read and wr from memory

Reflection breaks singleton by accessing private constructor

 And creating new object using that

<img width="809" height="445" alt="image" src="https://github.com/user-attachments/assets/62d9f8f7-27df-4387-8dfb-e063f5d7594b" />

<img width="940" height="401" alt="image" src="https://github.com/user-attachments/assets/07ac68e8-d539-4941-a27a-4f4b89bb4c67" />

Os scheduler assigns thread to CPU

Machine code is stored in code segment
Registyer issued to stored intermediate result

On context switching thread will store intermediate data in register

Process 1 and 2 – multitasking(dodnt share resources)

Inside each process – many threads so multithreading_share 
resources)
Deamonb tgread – as soon as one of  user theread deads ,deamon thread will get killed

Ex – GC is deamon thread as soon as program ends GC will also stop,autosave is also deamon thread.

<img width="742" height="495" alt="image" src="https://github.com/user-attachments/assets/923e14f6-259f-493f-9634-90d8142f31a9" />



In above even if producer method is sybchronized if it is being accessed by 2 diif object even if the two object belongs to diff thread they both will enter synchronized block

To solve this we have custom locks

Xclusive lock is wr lock(where u can do both rd and wr)
Optimistic -no lock acquired

<img width="940" height="473" alt="image" src="https://github.com/user-attachments/assets/cb8b093a-957c-48ee-8867-5b23849f25e3" />




If row version is same as prev then update is done using validate method of stamp else not – optimistic lock coz no unlock is done here it just check only row version
In custom lock similar to wait and notify u use await() and signal()

With forkjoin pool executor – big task is divided into subtask using fork() and finally they combined to get final result
Whenever subtask needs to return value then go for recursive task else recursivetaskaction
Platform threads is wrapper around os thread

No 1:1 mapping between os and vrtual thread so if VT needs to go for I/O then os thread will pick other virtual tread
Jvm creates only virtal thread with system call so it is fast unlike normal thread where we create os thread

Achieve immutability in builder coz it has no setter

Here’s a clear, concise comparison of virtual threads vs normal (platform) threads, especially as used in Java (Project Loom), but the concepts apply generally.
________________________________________
✅ Virtual Thread vs Normal Thread
1. What They Are
🧵 Normal Thread (Platform Thread)
•	A traditional OS-backed thread.
•	Each thread maps 1:1 to an operating system thread.
•	Limited in quantity (thousands at most).
•	Expensive to create and block.
🫧 Virtual Thread
•	A lightweight, user-mode thread managed by the JVM—not the OS.
•	Many virtual threads can run on a small pool of carrier (platform) threads.
•	You can create millions cheaply.
•	Blocking is inexpensive; JVM parks the virtual thread instead of blocking an OS thread.
________________________________________
✅ 2. Key Differences
Feature	Virtual Thread	Normal Thread (Platform)
Backed by OS thread?	❌ No (user-mode)	✅ Yes
Creation cost	Very low (cheap, fast)	High
Blocking cost	Very cheap (JVM parks it)	Expensive (blocks OS thread)
Use case	High-concurrency tasks (e.g., servers)	CPU-bound or low-concurrency tasks
Max count	Millions	Thousands
Scheduling	Managed by JVM	Managed by OS
Performance characteristics	Great for I/O-bound workloads	Better for CPU-heavy workloads
________________________________________
✅ 3. When to Use Which?
Use Virtual Threads for:
•	Handling many simultaneous client requests
•	I/O-heavy workloads (network calls, database calls)
•	Replacing complex async/reactive frameworks with simple blocking code
Use Normal Threads for:
•	CPU-bound tasks (number crunching, parallel processing)
•	Long-lived OS-dependent operations
•	When you need strong OS-level control (thread affinity, priorities)
________________________________________
✅ 4. Example (Java)
Normal thread
Thread t = new Thread(() -> {
    // work
});
t.start();
Virtual thread
Thread t = Thread.ofVirtual().start(() -> {
    // work
});
________________________________________
🔥 Key Insight
Virtual threads do NOT make tasks faster; they make concurrency cheaper.
They help you scale to thousands or millions of logically blocking tasks.
________________________________________
If you want, I can show a benchmark comparison, how they work internally, or migration tips from normal threads to virtual threads.

Lombok is external libraru coz we doi entry in pom wherase record is feature of java class
Lombok nec=ver restrict u to add setter unlike record


















