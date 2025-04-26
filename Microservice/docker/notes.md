## Resource
https://youtu.be/31k6AtW-b3Y

## **steps**
1. Install docker cli and desktop
2.  Docker deamon does all work like create,scale container,pull images
3.  containers actually run images
4.  images can be deploy on cloud
5.  docker container ls->list all running container and docker container ls -a->list all container
6.  docker exec <container_name> ls->will run ls command inside container
8.  <img width="278" alt="image" src="https://github.com/user-attachments/assets/b175b599-c049-4512-9c04-cfcd54eb2442" /> ->with this permanently you are attached to this conatiner as u have run in interactive mode

<img width="480" alt="image" src="https://github.com/user-attachments/assets/8ea8fe72-c083-4a9a-b8e5-749e34633ee2" />
docker network inspect brodge//list all container running inside bridge

9.  run it --network=host <cont_name>//contatiner is atteched to your host machine
10.  u nnede to expose port in bridge coz those ports resides in docker unlike host network
11.  --network=none//no internet access to this network

12.  ## create custom network
13.  <img width="282" alt="image" src="https://github.com/user-attachments/assets/3eeae59f-d80b-4a57-acbb-25e35083c574" />
Now make a container tony startk in this network
<img width="335" alt="image" src="https://github.com/user-attachments/assets/c6354803-ce07-4dc0-98a5-acd16a93d6cc" />
lly create busybox
Now thhese two container can communicate with each other by name and not ip coz IP can change ,u can do ping tony_stark from the busybox container

Each ciontainer has some memory by defauklt and when container is destroyed it's memory is also destroyed
so to prevent this we use docker volumes which is permanent storage
as contatiner are isolateed by default so we cannt share data,but we can mount volume from any container to another container
ex-macbook desktop folder is moun t to ubuntu container

<img width="319" alt="image" src="https://github.com/user-attachments/assets/facdbfd1-38ae-449b-8302-82acab1aa741" />

u can do ping tony_
<img width="515" alt="image" src="https://github.com/user-attachments/assets/62545ec9-0358-4c9a-ac71-66236d38aded" />
changes inside test folder will be reflected in abc folder of ubuntu and vice versa
similar to gitgnore  use dockerignotre uin project tp not include files whily copy commsnd in dockerfile

<img width="308" alt="image" src="https://github.com/user-attachments/assets/c7ec51ff-53ac-477b-8b8e-382b42a4f182" />
Execte all code below wprkdir inside app folder

## Multi stage build
Use output of one stage to other
![Screenshot_20250426_114829](https://github.com/user-attachments/assets/63dbf7d0-581d-4e8d-8abe-ee2680b8c114)
![Screenshot_20250426_114916](https://github.com/user-attachments/assets/af87e3ea-753c-4d28-be52-248ef8fe370a)



