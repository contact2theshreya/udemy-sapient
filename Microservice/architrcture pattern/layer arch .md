Here’s an example of how a **Layered Architecture** can be implemented in **Java**. The layers in this architecture are typically:

1. **Presentation Layer** (Controller)
2. **Business Logic Layer** (Service)
3. **Data Access Layer** (Repository)

Let's create a simple application with the following components:

- **Model**: A `Product` class.
- **Repository**: A simple class that interacts with the data (we'll simulate data storage with an in-memory list).
- **Service**: The business logic layer that uses the repository to retrieve and manage data.
- **Controller**: A presentation layer that interacts with the service and handles user requests.

### 1. **Product Model** (Domain/Entity)
```java
public class Product {
    private int id;
    private String name;
    private double price;

    // Constructor
    public Product(int id, String name, double price) {
        this.id = id;
        this.name = name;
        this.price = price;
    }

    // Getters and Setters
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }
}
```

### 2. **Repository Layer** (Data Access Layer)
```java
import java.util.ArrayList;
import java.util.List;

public class ProductRepository {
    private List<Product> productList;

    // Constructor to simulate data storage
    public ProductRepository() {
        this.productList = new ArrayList<>();
        productList.add(new Product(1, "Product1", 10.0));
        productList.add(new Product(2, "Product2", 20.0));
        productList.add(new Product(3, "Product3", 30.0));
    }

    // Get all products
    public List<Product> getAllProducts() {
        return productList;
    }

    // Get a product by id
    public Product getProductById(int id) {
        return productList.stream()
                          .filter(product -> product.getId() == id)
                          .findFirst()
                          .orElse(null);
    }

    // Add a new product
    public void addProduct(Product product) {
        productList.add(product);
    }
}
```

### 3. **Service Layer** (Business Logic Layer)
```java
import java.util.List;

public class ProductService {
    private ProductRepository productRepository;

    // Constructor to initialize the repository
    public ProductService(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }

    // Get all products
    public List<Product> getAllProducts() {
        return productRepository.getAllProducts();
    }

    // Get product by ID
    public Product getProductById(int id) {
        return productRepository.getProductById(id);
    }

    // Add new product
    public void addProduct(Product product) {
        productRepository.addProduct(product);
    }
}
```

### 4. **Controller Layer** (Presentation Layer)
```java
import java.util.List;

public class ProductController {
    private ProductService productService;

    // Constructor to initialize the service
    public ProductController(ProductService productService) {
        this.productService = productService;
    }

    // Display all products
    public void displayAllProducts() {
        List<Product> products = productService.getAllProducts();
        for (Product product : products) {
            System.out.println("ID: " + product.getId() + ", Name: " + product.getName() + ", Price: " + product.getPrice());
        }
    }

    // Display a product by ID
    public void displayProductById(int id) {
        Product product = productService.getProductById(id);
        if (product != null) {
            System.out.println("Product found: " + "ID: " + product.getId() + ", Name: " + product.getName() + ", Price: " + product.getPrice());
        } else {
            System.out.println("Product with ID " + id + " not found.");
        }
    }

    // Add a new product
    public void addProduct(Product product) {
        productService.addProduct(product);
        System.out.println("Product added: " + product.getName());
    }
}
```

### 5. **Main Application Class**
```java
public class Main {
    public static void main(String[] args) {
        // Initialize the layers
        ProductRepository productRepository = new ProductRepository();
        ProductService productService = new ProductService(productRepository);
        ProductController productController = new ProductController(productService);

        // Display all products
        System.out.println("Displaying all products:");
        productController.displayAllProducts();

        // Add a new product
        Product newProduct = new Product(4, "Product4", 40.0);
        productController.addProduct(newProduct);

        // Display all products after adding the new one
        System.out.println("\nDisplaying all products after adding a new product:");
        productController.displayAllProducts();

        // Display product by ID
        System.out.println("\nDisplaying product with ID 2:");
        productController.displayProductById(2);
    }
}
```

### Explanation of Layers:
1. **Model (Product)**: Represents the entity that holds the data.
2. **Repository**: Provides data access logic (simulating interaction with a database or data source).
3. **Service**: Contains the business logic. It fetches data from the repository and can perform actions like adding or processing data.
4. **Controller**: Interacts with the user or other systems, displays results, and calls the service layer to fetch or manipulate data.

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

### Summary:
- **Layered Architecture** in Java allows you to separate concerns between the presentation (UI), business logic, and data access layers.
- Each layer has a clear responsibility, and they communicate with each other in a downward direction.
- This example shows a basic CRUD-like operation using a controller to interact with the service layer, which in turn interacts with the repository to fetch or update data.
