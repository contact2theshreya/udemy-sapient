https://github.com/in28minutes/spring-microservices-v3/tree/main/04.docker/01-step-by-step-changes#readme
https://github.com/in28minutes/spring-microservices-v3/tree/main/91.docker
If you are using Window 10 and are using docker toolbox

=> Use 192.168.99.100 instead of localhost.

Note: If 192.168.99.100 does not work, you can find the IP by using the command docker-machine ip

1) Install docker
2) docker container run -d -p 5000:5000 in28min/hello-world-nodejs:0.0.1.RELEASE
docker container run -d -p 5000:5000 in28min/hello-world-java:0.0.1.RELEASE
docker container run -d -p 5000:5000 in28min/hello-world-python:0.0.1.RELEASE
docker container ls //give running conainer details
docker image ls//list all images
docker container stop cc
docker container run -d -p 5001:5000 in28min/hello-world-nodejs:0.0.1.RELEASE
docker container run -d -p 5002:5000 in28min/hello-world-nodejs:0.0.1.RELEASE
docker container stop cc
docker container run -d -p 5001:5000 in28min/hello-world-nodejs:0.0.1.RELEASE
docker container run -d -p 5002:5000 in28min/hello-world-nodejs:0.0.1.RELEASE
docker container run -p 5003:5000 in28min/hello-world-nodejs:0.0.1.RELEASE
docker container run -p 5003:5000 in28min/hello-world-nodejs:0.0.1.RELEASE
//Download image if it is available in your machine else downlaod it globallty
Multi [platform support-can run any platform just docker engine has to be installed
we can have as many container for the same image
-d is don't tie up termainl with the liofetime of container


 
docker --version
docker container ls
docker build -t in28min/hello-world-docker:v1 .
docker image list
docker run -d -p 5000:5000 in28min/hello-world-docker:v1
docker build -t in28min/hello-world-docker:v2 .
docker container run -d -p 5000:5000 in28min/hello-world-docker:v2
docker build -t in28min/hello-world-docker:v3 .
docker container run -d -p 5000:5000 in28min/hello-world-docker:v3
docker build -t in28min/hello-world-docker:v4 .
