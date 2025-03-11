1) all microservice config is present in github and clud config server will be connected to github to detect the changes,whever any commit is done in github ,cloud config server will be notified of the same
2) Add dependency config client to talk to cloud config server and in app.prop and port to talk of config server
3) spring.config.import=optional:configserver:http://localhost:8888
4) create limit service - https://github.com/in28minutes/spring-microservices-v3/tree/main/03.microservices/limits-service
5) https://github.com/in28minutes/spring-microservices-v3/blob/main/03.microservices/step07.md
6) https://github.com/in28minutes/spring-microservices-v3/blob/main/03.microservices/01-step-by-step-changes/readme.md#step-01
7) https://github.com/in28minutes/spring-microservices-v3/blob/main/03.microservices/01-step-by-step-changes/readme.md#step-01
8) We will be using following ports for running our microservices and components. Copy them and have them handy as we go further in the course!

1. Limits Microservice
Ports: 8080, 8081, etc.

2. Spring Cloud Config Server
Port: 8888

3. Currency Exchange Microservice
Ports: 8000, 8001, 8002, etc.

4. Currency Conversion Microservice
Ports: 8100, 8101, 8102, etc.

5. Netflix Eureka Naming Server
Port: 8761

6. API Gateway
Port: 8765

7. Zipkin Distributed Tracing Server
Port: 9411


9) Now limit service will pick properties not from his own app.prop but from the propert file which is in git repo of limit0service.properties
10) Feign-easy to call other microservice with less boilerplate code
11) Automatic load balancing can be also done with the help of eureka
12) spring cloud LB is used by feign -client side load balancing
13) With API GAteway
Initial

- http://localhost:8765/CURRENCY-EXCHANGE/currency-exchange/from/USD/to/INR

- http://localhost:8765/CURRENCY-CONVERSION/currency-conversion/from/USD/to/INR/quantity/10

- http://localhost:8765/CURRENCY-CONVERSION/currency-conversion-feign/from/USD/to/INR/quantity/10



Lower Case

- http://localhost:8765/currency-exchange/currency-exchange/from/USD/to/INR

- http://localhost:8765/currency-conversion/currency-conversion/from/USD/to/INR/quantity/10

- http://localhost:8765/currency-conversion/currency-conversion-feign/from/USD/to/INR/quantity/10



Custom Routes

- http://localhost:8765/currency-exchange/from/USD/to/INR

- http://localhost:8765/currency-conversion/from/USD/to/INR/quantity/10

- http://localhost:8765/currency-conversion-feign/from/USD/to/INR/quantity/10

- http://localhost:8765/currency-conversion-new/from/USD/to/INR/quantity/10

BULKHEAD-NO OF CONCURRENT CALLS TO ALLOWED
