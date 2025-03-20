In **Clean Architecture**, the goal is to create a system where the core business logic (Entities and Use Cases) is **independent of frameworks, UI, and external systems** like databases. The outer layers (like UI and data access) depend on well-defined interfaces to communicate with the core, and not the other way around. 

Here’s an example of **Clean Architecture** implemented in **Java**, with the following layers:

1. **Entities** (Core business models)
2. **Use Cases** (Application logic)
3. **Interface Adapters** (Controller, Gateways, etc.)
4. **Frameworks and Drivers** (Database, UI, external frameworks)

We will build a simple application that manages **Products**, with these layers.

---

### 1. **Entities** (Core Business Logic)

Entities represent the core business objects of your application. They don’t depend on any other layer or framework.

```java
public class Product {
    private int id;
    private String name;
    private double price;

    public Product(int id, String name, double price) {
        this.id = id;
        this.name = name;
        this.price = price;
    }

    // Getters and Setters
    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }
}
```

### 2. **Use Cases** (Application Logic)

The **Use Cases** define the application's specific business operations, often interacting with the entities. The use case layer contains the business rules, and it **does not depend on external systems**.

```java
import java.util.List;

public interface ProductUseCase {
    List<Product> getAllProducts();
    Product getProductById(int id);
    void addProduct(Product product);
}

public class ProductUseCaseImpl implements ProductUseCase {
    private ProductRepository productRepository;

    public ProductUseCaseImpl(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }

    @Override
    public List<Product> getAllProducts() {
        return productRepository.getAllProducts();
    }

    @Override
    public Product getProductById(int id) {
        return productRepository.getProductById(id);
    }

    @Override
    public void addProduct(Product product) {
        productRepository.addProduct(product);
    }
}
```

### 3. **Interface Adapters** (Controllers and Gateways)

This layer contains code that translates data from the **Use Case layer** to the **Frameworks and Drivers** layer and vice versa. Here’s where you can implement a **Controller** that interacts with the user interface.

```java
import java.util.List;

public class ProductController {
    private ProductUseCase productUseCase;

    public ProductController(ProductUseCase productUseCase) {
        this.productUseCase = productUseCase;
    }

    public void displayAllProducts() {
        List<Product> products = productUseCase.getAllProducts();
        products.forEach(product -> 
            System.out.println("ID: " + product.getId() + ", Name: " + product.getName() + ", Price: " + product.getPrice()));
    }

    public void displayProductById(int id) {
        Product product = productUseCase.getProductById(id);
        if (product != null) {
            System.out.println("Product found: " + "ID: " + product.getId() + ", Name: " + product.getName() + ", Price: " + product.getPrice());
        } else {
            System.out.println("Product with ID " + id + " not found.");
        }
    }

    public void addProduct(Product product) {
        productUseCase.addProduct(product);
        System.out.println("Product added: " + product.getName());
    }
}
```

### 4. **Frameworks and Drivers** (External Frameworks like Databases)

This layer implements concrete classes for interacting with databases, frameworks, or external systems. Here we simulate a **ProductRepository** using an in-memory list.

```java
import java.util.ArrayList;
import java.util.List;

public interface ProductRepository {
    List<Product> getAllProducts();
    Product getProductById(int id);
    void addProduct(Product product);
}

public class InMemoryProductRepository implements ProductRepository {
    private List<Product> products = new ArrayList<>();

    public InMemoryProductRepository() {
        // Add some sample data
        products.add(new Product(1, "Product1", 10.0));
        products.add(new Product(2, "Product2", 20.0));
        products.add(new Product(3, "Product3", 30.0));
    }

    @Override
    public List<Product> getAllProducts() {
        return products;
    }

    @Override
    public Product getProductById(int id) {
        return products.stream().filter(p -> p.getId() == id).findFirst().orElse(null);
    }

    @Override
    public void addProduct(Product product) {
        products.add(product);
    }
}
```

### 5. **Main Application Class**

This is the entry point where we wire everything together by creating instances of each layer and invoking methods.

```java
public class Main {
    public static void main(String[] args) {
        // Frameworks & Drivers: Create an in-memory repository
        ProductRepository productRepository = new InMemoryProductRepository();

        // Use Case: Create the use case with the repository
        ProductUseCase productUseCase = new ProductUseCaseImpl(productRepository);

        // Interface Adapters: Create the controller with the use case
        ProductController productController = new ProductController(productUseCase);

        // Test the application
        System.out.println("Displaying all products:");
        productController.displayAllProducts();

        // Add a new product
        Product newProduct = new Product(4, "Product4", 40.0);
        productController.addProduct(newProduct);

        // Display all products again after adding the new one
        System.out.println("\nDisplaying all products after adding a new product:");
        productController.displayAllProducts();

        // Display product by ID
        System.out.println("\nDisplaying product with ID 2:");
        productController.displayProductById(2);
    }
}
```

### Explanation of Layers:

1. **Entities**: The `Product` class is an entity that represents the core business object.
2. **Use Cases**: `ProductUseCase` defines the business logic (e.g., fetching and adding products).
3. **Interface Adapters**: `ProductController` interacts with the user and calls methods from the Use Case layer. It’s responsible for displaying data and accepting inputs.
4. **Frameworks and Drivers**: `InMemoryProductRepository` simulates data persistence. In a real-world application, this would be replaced by a database repository or an external system.

### Sample Output:

```txt
Displaying all products:
ID: 1, Name: Product1, Price: 10.0
ID: 2, Name: Product2, Price: 20.0
ID: 3, Name: Product3, Price: 30.0

Product added: Product4

Displaying all products after adding a new product:
ID: 1, Name: Product1, Price: 10.0
ID: 2, Name: Product2, Price: 20.0
ID: 3, Name: Product3, Price: 30.0
ID: 4, Name: Product4, Price: 40.0

Displaying product with ID 2:
Product found: ID: 2, Name: Product2, Price: 20.0
```

### Key Points of Clean Architecture in This Example:
- **Separation of Concerns**: The core business logic (entities and use cases) is completely decoupled from frameworks, databases, and UI.
- **Testability**: Each layer can be independently tested. For example, you can mock the `ProductRepository` to test the `ProductUseCase` independently of the database.
- **Flexibility**: The UI layer (controller) can be replaced with any framework, and the database layer can be replaced with any type of persistence mechanism without affecting the core business logic.

This clean separation of layers allows for flexibility, scalability, and maintainability, especially as your application grows more complex.
