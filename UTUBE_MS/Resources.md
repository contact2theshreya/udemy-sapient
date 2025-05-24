https://github.com/SaiUpadhyayula/spring-boot-microservices/tree/master
https://www.youtube.com/watch?v=lh1oQHXVSc0&list=PLSVW22jAG8pBnhAdq9S8BpLnZ0_jVBj0c&index=2&t=2239s

Use testcontaienr for intergration testing to pull docker image at runtime for example mongodb and set the url property dynamically at runtine when test starts up to run
see test in productservice-https://github.com/SaiUpadhyayula/spring-boot-microservices/blob/master/product-service/src/test/java/com/programmingtechie/productservice/ProductServiceApplicationTests.java
Move common dependency and tags to parent project so that it can be available to all child

## step 1
1) https://www.youtube.com/watch?v=lh1oQHXVSc0&list=PLSVW22jAG8pBnhAdq9S8BpLnZ0_jVBj0c&index=1
2) craete all service and shift to parent module
3) use testcontainer for testing in tegration
4) https://programmingtechie.com/articles/spring-boot-microservices-tutorial
https://programmingtechie.com/articles/spring-boot-microservices-tutorial-part-2

In order service-docker/mysql/init.sql has command creatre database order service if not exist

<img width="473" alt="image" src="https://github.com/user-attachments/assets/bcbaf719-c735-4010-9533-94b3ab9385ab" />

@AutoConfigureWireMock(port = 0)--start wiremock server in this random port 

<img width="344" alt="image" src="https://github.com/user-attachments/assets/3c1be614-9bee-475c-b60c-cd1b4e15f1d6" />
https://programmingtechie.com/articles/spring-boot-microservices-tutorial-part-3

In app.properties of test folder,test cases will pick configuration from that file so add an inventory wiremock url
Inventory stub indicated whenever inventory irl calls with the given url and http method then return the response
<img width="541" alt="image" src="https://github.com/user-attachments/assets/b20d1bcd-6b2b-42e3-b6c2-a64a49492236" />

<img width="541" alt="image" src="https://github.com/user-attachments/assets/be7d2a51-1982-4d3a-942c-86684afe6cb7" />
## security

https://programmingtechie.com/articles/spring-boot-microservices-tutorial-part-4

## API Documentation
https://programmingtechie.com/articles/spring-boot-microservices-tutorial-part-5

##  Aggregate REST API documentauiion in Gateway

https://programmingtechie.com/articles/spring-boot-microservices-tutorial-part-5

<img width="473" alt="image" src="https://github.com/user-attachments/assets/1d6e68de-663b-4bf3-b882-1e4db8c82125" />

## CKT breaker
https://programmingtechie.com/articles/spring-boot-microservices-tutorial-part-6

##  Integrating Kafka with Schema Registry
https://programmingtechie.com/articles/spring-boot-microservices-tutorial-part-8





