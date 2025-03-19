https://github.com/in28minutes/spring-microservices-v3/tree/main/03.microservices

# u can give cmd arguemeny t with port number to run you application,this will take priority over app.prop port number
_Dserver.port=8001
Feign-rest service client to call to service using proc

## Ribbon-client side loadbalacing
https://www.geeksforgeeks.org/spring-cloud-client-side-load-balancing-with-ribbon/
use ribbon to find details form naming server

https://github.com/in28minutes/spring-microservices-v3/tree/main/03.microservices/naming-server

get rid of hardcoding port of >1 instance of servcie using service registry
Ribbon will talk to naming server and will retreive details by discbling list of server from app.prop coz app.prop has eureka enable so ribbon will talk to it

## Api gateway-auth,rate limit,logging,fault tolerance,security
use ziuul
https://howtodoinjava.com/spring-cloud/spring-cloud-api-gateway-zuul/
https://dzone.com/articles/how-to-build-an-api-gateway-with-netflix-zuul-spri

## Distributed tyracing 
Putt all log in queue(rabbot) and send to zipkin
spring cloud sleuth will add a unique id to request so implement it in all microservicve
https://howtodoinjava.com/spring-cloud/spring-cloud-zipkin-sleuth-tutorial/
https://www.javainuse.com/spring/cloud-sleuth
https://www.geeksforgeeks.org/spring-cloud-bus/

## Fault tolerance
Hystrix
@HystrixCommand(fallbackMethod="")

