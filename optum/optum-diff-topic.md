https://github.com/Java-Techie-jt/java8

Async and non blocking
<img width="468" height="75" alt="image" src="https://github.com/user-attachments/assets/ba8f36b4-b727-477c-aa28-194a6261b866" />

<img width="131" height="63" alt="image" src="https://github.com/user-attachments/assets/225d7bd7-c56d-4de4-a042-2739edd88f9f" />

<img width="259" height="140" alt="image" src="https://github.com/user-attachments/assets/dff9a37b-6786-4d3f-ab08-1bd29005cd89" />

Thread 1 afetr receiving resp from db then it would complete ,but this is blocking coz all thread occupied with db driver to get response<img width="468" height="67" alt="image" src="https://github.com/user-attachments/assets/b3b5c30f-c65f-4480-a51a-41d5eab80b4b" />

<img width="452" height="212" alt="image" src="https://github.com/user-attachments/assets/bc7af191-1f44-4844-a91a-132dc8ce5f6b" />

Here each thread wont wait for db driver ,coz this task will be handled by event loop<img width="468" height="50" alt="image" src="https://github.com/user-attachments/assets/16a49a67-fed2-4ffe-bbb8-98391bba1ece" />

<img width="300" height="131" alt="image" src="https://github.com/user-attachments/assets/faf7d50b-7c0e-4c8d-924d-79b81aaa5104" />

<img width="452" height="256" alt="image" src="https://github.com/user-attachments/assets/44ba5001-1a62-49e9-ac66-5b0e90f20298" />

<img width="452" height="226" alt="image" src="https://github.com/user-attachments/assets/e018b15d-beb7-4350-adde-1b64327602a2" />

Above is supported by reactive progg
With backpressure support if a[plication is not able to handle hoge data then we can tell db to hold on and let application work on the data it has then to give next basically to slow down data from db based on config

<img width="468" height="134" alt="image" src="https://github.com/user-attachments/assets/23276126-70c1-4538-9ad4-8ab705cc853b" />

<img width="182" height="86" alt="image" src="https://github.com/user-attachments/assets/f369e3af-c285-40d0-9e0a-f7a1107f9247" />

<img width="325" height="156" alt="image" src="https://github.com/user-attachments/assets/cbefe671-66b0-4bf5-956b-b0aa77498364" />

Subscriber will call req to get data from publisher<img width="468" height="50" alt="image" src="https://github.com/user-attachments/assets/a457f6b6-c375-44f1-a93a-4422a353503e" />

<img width="452" height="55" alt="image" src="https://github.com/user-attachments/assets/34548c90-3f24-4f0d-b071-d608f1deef85" />

<img width="339" height="111" alt="image" src="https://github.com/user-attachments/assets/bc3df10e-3058-4b29-99e5-bb22b4c65bfe" />


Subscribe() – subsciper will invoke publisher 

Then pub will send subscription() even to subscriber confirming that subscription() is successful

Subscriber will call req(n) to pub to get n data from. Publisher

Publisher will send stream – onNexrt()

All done – oncomplete()

<img width="468" height="192" alt="image" src="https://github.com/user-attachments/assets/2b294b54-00e8-436a-94c0-cb0d521b2e9b" />

<img width="225" height="145" alt="image" src="https://github.com/user-attachments/assets/21e524de-7f62-41c8-967c-bdfd68e21020" />

Mono can only handle one object,it will act as pub lishetr<img width="468" height="50" alt="image" src="https://github.com/user-attachments/assets/d0f5519b-60c8-4eaf-b1cc-a7b82776be75" />

<img width="452" height="233" alt="image" src="https://github.com/user-attachments/assets/8319e899-d90d-421b-bd8e-7847d9cd1556" />


https://github.com/Java-Techie-jt/springboot-webflux-demo/blob/main/src/test/java/com/javatechie/webflux/MonoFluxTest.java
<img width="468" height="92" alt="image" src="https://github.com/user-attachments/assets/51192a1f-72f9-42b0-99fd-3dcd374d39e2" />

<img width="452" height="136" alt="image" src="https://github.com/user-attachments/assets/9fb32741-253d-4031-913a-a83317c433b0" />

With above we will get 5 onnext with 1 onerror and after error we cant do onnext

Synchronus blocking w/o reactive code
---untill all elements gets p[roicessed ,we wont see result
<img width="468" height="125" alt="image" src="https://github.com/user-attachments/assets/a7ef5a6e-fff6-4348-8a2a-3fb7889a863f" />

<img width="452" height="220" alt="image" src="https://github.com/user-attachments/assets/724119b3-4b5e-43ec-ad96-9c97b444749b" />

<img width="420" height="71" alt="image" src="https://github.com/user-attachments/assets/eaf09ff2-0293-4698-a0dd-d827f9a43743" />

In case of flux ,as elements are being processed in loop we get the result from api continuously so it is non blocking(media type is imp and pub will push event to subscribr) and if u cancel request(stop page load) it immediately stop processing in BE  unlike traditional approach<img width="468" height="101" alt="image" src="https://github.com/user-attachments/assets/10ef09b0-664c-4e67-b8d3-397ee4e64234" />

<img width="452" height="149" alt="image" src="https://github.com/user-attachments/assets/871d8d4d-3e74-4961-8534-12ed9f6afda7" />

<img width="224" height="104" alt="image" src="https://github.com/user-attachments/assets/141c5726-c864-4fcc-b6d5-9aaf093fcd26" />



Handle concurrent req from client
Can do horizontal scaling with k8s so move away from thread per req model and handle higher load of req with less no of thread
<img width="468" height="142" alt="image" src="https://github.com/user-attachments/assets/1861a91c-c087-48c7-b9e9-5502d1fe0993" />

<img width="275" height="131" alt="image" src="https://github.com/user-attachments/assets/af121fd4-a5d4-48e7-af11-acf9e2ffbe5b" />

<img width="216" height="133" alt="image" src="https://github.com/user-attachments/assets/3463359c-f382-42ea-b491-fab84647e67c" />


In event driven async non blocking ,data will be push as an event using onnext() and oncomplet() means all events are pushed,on error() – receives error
<img width="468" height="92" alt="image" src="https://github.com/user-attachments/assets/82fb1cfb-02f5-4452-be07-d799cc49b56d" />

<img width="199" height="119" alt="image" src="https://github.com/user-attachments/assets/73213983-479e-405c-a5a4-8016991bdb41" />

Save(),NO DATA IN DB – only oncomplete()
Backpressure – to tell DB to slow down data
<img width="468" height="75" alt="image" src="https://github.com/user-attachments/assets/7461b886-7aad-4199-8f5c-f989a8e52a65" />

<img width="452" height="97" alt="image" src="https://github.com/user-attachments/assets/fb462d92-ad2d-4328-a938-141e46dc1731" />

<img width="265" height="107" alt="image" src="https://github.com/user-attachments/assets/8f657ae3-9134-41b3-ba35-eab78306541c" />

<img width="251" height="72" alt="image" src="https://github.com/user-attachments/assets/ababe43a-8afb-4f41-96b9-3fe520f70c26" />

Reactor library – for reactive programming<img width="468" height="50" alt="image" src="https://github.com/user-attachments/assets/4782675c-f925-449d-ac83-4952c2892044" />

<img width="199" height="97" alt="image" src="https://github.com/user-attachments/assets/6953a847-58dc-48c4-9976-815add9e7864" />

Flux and mono are the implementation of reactor stream specification 
Mono represent 0 to 1 element
<img width="468" height="75" alt="image" src="https://github.com/user-attachments/assets/8a4e5b5e-6eaf-4eb0-aa1d-46724e895413" />

<img width="344" height="128" alt="image" src="https://github.com/user-attachments/assets/e00c4f9f-9f8e-4cd2-8668-37749fab46be" />

<img width="286" height="147" alt="image" src="https://github.com/user-attachments/assets/00d9da01-509c-4924-b8a2-d206d8b7fc86" />

<img width="452" height="152" alt="image" src="https://github.com/user-attachments/assets/069023f1-437e-42cc-8982-70fd41f7d7f8" />

Verify() is like subscribe<img width="468" height="50" alt="image" src="https://github.com/user-attachments/assets/53708d42-f511-45fb-82c7-88b6d5d042a3" />

<img width="452" height="48" alt="image" src="https://github.com/user-attachments/assets/a6b238f5-37f1-4eea-849e-f2067a65e885" />


If return type is json from api then broser will keep page load till it gets whole data unlike produces mediarype stream json
Data will be displayed as they come
<img width="468" height="117" alt="image" src="https://github.com/user-attachments/assets/9ca31387-5e33-422b-8240-b3118452e1bb" />

<img width="275" height="134" alt="image" src="https://github.com/user-attachments/assets/d97df15d-0250-49b4-a05e-30c2c8fa7cb3" />

Infinit stream test case<img width="468" height="50" alt="image" src="https://github.com/user-attachments/assets/1044615d-d72e-4094-8e19-e7279c3efe50" />

<img width="452" height="126" alt="image" src="https://github.com/user-attachments/assets/0dd807f6-8563-4982-a47a-857640deaa4f" />

<img width="205" height="67" alt="image" src="https://github.com/user-attachments/assets/9b3f1698-a591-4f36-9d4e-a2047dfe944a" />

<img width="202" height="128" alt="image" src="https://github.com/user-attachments/assets/6af0fd4c-7d7f-4619-a05e-bcd0440530b4" />

Routefn -roter the incoming req,llar to @RequestMapping
Handler function handles the request and response
Similar to the body of requestmapping annotation
<img width="468" height="100" alt="image" src="https://github.com/user-attachments/assets/e3705c91-3297-435e-b4af-e7ed496a1341" />


Handler fn has 2 classes -serverreq(handles http req)
Serverresp (handles http response)
<img width="468" height="100" alt="image" src="https://github.com/user-attachments/assets/84bab4b7-f9a4-4767-b6d4-6e28239e0ab5" />

To test infinit stream call .cancel() in stepverifier<img width="468" height="50" alt="image" src="https://github.com/user-attachments/assets/6edf0ab4-ddca-4b2c-a5c8-d64794435deb" />

<img width="452" height="127" alt="image" src="https://github.com/user-attachments/assets/63a280eb-03ec-4f7c-93b6-1b8bbd1ff32f" />

<img width="243" height="111" alt="image" src="https://github.com/user-attachments/assets/6de89867-9ecf-456e-a7b4-53fad9184309" />

<img width="452" height="111" alt="image" src="https://github.com/user-attachments/assets/baf390b8-97d9-4004-8da6-ee47ae52cb78" />

<img width="452" height="160" alt="image" src="https://github.com/user-attachments/assets/d8003aad-29de-47c3-8d96-8d1485d78a27" />

GRAPHQL APOLLO
https://adhithiravi.medium.com/getting-started-with-apollo-client-in-your-react-app-986c0443d7dd
<img width="468" height="84" alt="image" src="https://github.com/user-attachments/assets/df9d0b58-6517-4667-9c70-2899ddca9648" />



FGeneric props
https://youtu.be/xFNk2nfDh4M

REDUX TOOLKIT
https://medium.com/@reactmasters.in/comprehensive-guide-to-redux-toolkit-in-react-js-ae9aa333d71a

SMART EMAIL ASSISTANT JAVA
https://youtu.be/vAaxHqNHsvY
WEBPACK
Webpack: Boost Your React App's Performance
https://youtu.be/yJrcib6ZITw
GIT ACTION
https://youtu.be/R8_veQiYBjI

GRAPHQL
https://www.geeksforgeeks.org/advance-java/spring-boot-graphql-integration/
https://www.geeksforgeeks.org/advance-java/spring-boot-graphql-integration/
with mutation
To implement GraphQL mutations in Spring Boot, you need to use the spring-boot-starter-graphql dependency and define a Mutation type in your schema, which is then handled by a corresponding Spring controller method annotated with @MutationMapping. 
Key Steps:
1.	Set up the Spring Boot Project:
Use Spring Initializr to create a new project with the necessary dependencies:
•	Spring Web
•	Spring for GraphQL
•	Spring Data JPA (for data persistence)
•	Database driver (e.g., H2 for simplicity, PostgreSQL, etc.)
•	Lombok (optional, for boilerplate code)
2.	Define the GraphQL Schema:
Create a schema file (e.g., schema.graphqls) in src/main/resources/graphql/. In this file, define your data types and the Mutation type.
<img width="468" height="649" alt="image" src="https://github.com/user-attachments/assets/eaa4b2f6-67be-402e-8056-6224e75eff97" />

graphql
type Book {
    id: ID!
    title: String!
    author: String!
}

input BookInput {
    title: String!
    author: String!
}

type Query {
    # ... other queries
    allBooks: [Book]!
}

type Mutation {
    createBook(bookData: BookInput!): Book!
    # Other mutations like updateBook, deleteBook
}
The input type is a special object type used for passing data to mutations, which is a recommended practice over using numerous scalar arguments.
1.	Implement Data Model and Repository:
Create a Java entity class (e.g., Book) and a Spring Data JPA repository interface to interact with the database.
java
@Entity
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String title;
    private String author;
    // Getters, setters, constructors...
}

@Repository
public interface BookRepository extends JpaRepository<Book, Long> {}
2.	Create a Mutation Resolver:
Create a Spring component (e.g., a @Controller or @Component) that contains methods to resolve the mutations defined in your schema.
java
@Controller
public class BookMutationResolver {

    private final BookRepository bookRepository;

    public BookMutationResolver(BookRepository bookRepository) {
        this.bookRepository = bookRepository;
    }

    @MutationMapping
    public Book createBook(@Argument BookInput bookData) {
        Book book = new Book();
        book.setTitle(bookData.getTitle());
        book.setAuthor(bookData.getAuthor());
        return bookRepository.save(book);
    }
}
The @MutationMapping annotation maps the method to the createBook field in the Mutation type of your schema. The @Argument annotation binds the GraphQL input arguments to your method parameters.
3.	Test the Mutation:
Run your application and use a tool like GraphiQL (usually available at http://localhost:8080/graphiql by default with the Spring Boot GraphQL starter) to test your mutation.
graphql
mutation CreateNewBook {
  createBook(bookData: { title: "My GraphQL Book", author: "Jane Doe" }) {
    id
    title
    author
  }
}
In Java, VM options and environment variables serve different purposes in configuring a Java application and its runtime environment.

VM Options (JVM Arguments):
•	Purpose: These arguments are passed directly to the Java Virtual Machine (JVM) when it starts. They control the JVM's behavior, memory allocation, garbage collection, and other low-level settings.
•	Usage: They are typically specified on the command line when invoking the java command, using flags like -Xmx (for maximum heap size), -D (for system properties), or -XX: (for advanced JVM options).
•	Scope: VM options primarily affect the specific JVM instance they are passed to. System properties set via -D can be accessed within the Java application using System.getProperty().
•	Examples:
•	java -Xmx512m MyClass (sets maximum heap size to 512MB)
•	java -Dmy.property=value MyClass (sets a system property named my.property)
Environment Variables:
•	Purpose: These are key-value pairs set at the operating system level, providing configuration information to processes running within that environment, including Java applications. They are used for broader system settings, paths, and sensitive information like API keys.
•	Usage: They are set using shell commands (e.g., export VAR=value in Linux/macOS, set VAR=value in Windows Command Prompt) or through system configuration tools.
•	Scope: Environment variables are accessible to any process launched within the environment where they are defined. Java applications can retrieve their values using System.getenv().
•	Examples:
•	JAVA_HOME=/usr/lib/jvm/java-11 (specifies the Java Development Kit installation directory)
•	API_KEY=your_secret_key (stores a sensitive API key)
Key Differences:
•	Target: VM options target the JVM itself, while environment variables target the operating system environment in which the JVM runs.
•	Access: VM options (specifically system properties) are accessed via System.getProperty(), while environment variables are accessed via System.getenv().
•	Persistence: Environment variables can persist across multiple application runs (depending on how they are set), while VM options are typically specific to each java command invocation.
•	Security: Environment variables are often used for sensitive information as they are not directly embedded in the application code, unlike hardcoded values.
In summary, VM options are for fine-tuning the JVM's performance and behavior, while environment variables provide a way to externalize configuration and sensitive data from the application code, making it more flexible and secure.


AI responses may include mistakes.

•	No Re-renders on Value Change: Unlike useState, updating the .current property of a ref does not trigger a component re-render. This makes it suitable for managing values that don't directly affect the component's visual output.   The state in Redux is stored in memory. This means that, if you refresh the page the state gets wiped out. The state in redux is just a variable that persists in memory because it is referenced by all redux functions.
•	A misconception is:
•	In redux, we know that the state is stored as an object.
•	This is not correct. State in redux can be any valid JavaScript value, not just an object. It just usually makes the most sense for it to be an object (or a special object like an array) because that allows for a more flexible data structure (but you could make the state just be a number for example, according to your need).
•	
https://medium.com/@bhairabpatra.iitd/usequery-hook-in-react-b06ef604ea46
https://medium.com/@yadav-ajay/cache-control-6676620f31c0
https://www.developerway.com/posts/implementing-advanced-use-previous-hook
USEPREVIOUS
https://medium.com/@lama.ibrahim96/implementing-custom-hooks-useprevious-usetimeout-3f0adbf81cf1
https://www.developerway.com/posts/implementing-advanced-use-previous-hook

REDUX TOOLKIT
https://medium.com/@reactmasters.in/comprehensive-guide-to-redux-toolkit-in-react-js-ae9aa333d71a
https://www.geeksforgeeks.org/reactjs/how-to-use-redux-toolkit-in-react-for-making-api-calls/



















<img width="451" height="689" alt="image" src="https://github.com/user-attachments/assets/e06ef29a-e907-41b9-af79-0870f412a91f" />
