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


