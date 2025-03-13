Trace request across all microservice
All microservice will send to ditsributed trace server (zipkin)and it will send to DB
Launch zipkin as docker container
https://github.com/in28minutes/spring-microservices-v3/tree/main/04.docker/01-step-by-step-changes#readme

https://github.com/in28minutes/spring-microservices-v3/blob/main/v3-upgrade.md

## Docker compose
create docker-compose.yaml in parent folder corresponding to other small projects
<img width="960" alt="image" src="https://github.com/user-attachments/assets/a45d6cfc-88d9-4f33-ab57-ff9b04ed265f" />
(2) Try adding restart: always to zipkin-server in docker-compose.yaml

  zipkin-server:
    image: openzipkin/zipkin:2.23
    mem_limit: 300m
    ports:
      - "9411:9411"
    networks:
      - currency-network
    restart: always #Restart if there is a problem starting up
    https://github.com/in28minutes/spring-microservices-v3/blob/main/04.docker/backup/docker-compose-05-zipkin.yaml


