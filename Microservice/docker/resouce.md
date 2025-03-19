https://github.com/in28minutes/spring-microservices-v3/tree/main/04.docker/01-step-by-step-changes#readme
https://github.com/in28minutes/spring-microservices-v3/tree/main/91.docker
If you are using Window 10 and are using docker toolbox

with docker image we can build multiple container

https://www.youtube.com/watch?v=exmSJpJvIPs

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

## with interactive mode, u can run commands inside container

<img width="476" alt="image" src="https://github.com/user-attachments/assets/7d32c9ba-5942-4d46-b8bd-d4993149546d" />

docker uses os kernel and virtualize application layer whereas VM has its own kernel so VM virtualize os kernel as well  as App layer that's why docker is lyt wt and takes less memory than VM and faster than VM  but VM is compatible with every system/os but docker is originally made for linux that's why docker images are linux based so we run linhux based images in our system using docker desktop which add a layer of lyt wt  hypervisor which internally uses lytwt linux distribution so our host machine supports multiple VM


