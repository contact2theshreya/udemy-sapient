https://github.com/in28minutes/spring-microservices-v3/tree/main/05.kubernetes
https://github.com/in28minutes/spring-microservices-v3/tree/main/05.kubernetes/01-step-by-step-changes#step-00

<img width="578" alt="image" src="https://github.com/user-attachments/assets/b47c0d2a-552e-4522-85b1-c58cc9482b6b" />

<img width="425" alt="image" src="https://github.com/user-attachments/assets/b3689884-4af8-47a9-8f1d-569c165a690c" />

each instance running is POD and ingres is used for routing

<img width="406" alt="image" src="https://github.com/user-attachments/assets/6102deeb-911f-46b5-ba30-2012377a3b4a" />
Node is server
ecah worker node has agent called kubelet and masyer connects with worker using api,container based appllication run inside pod
pod is an isolated env has its own resources and container run inside it


<img width="377" alt="image" src="https://github.com/user-attachments/assets/28ac0d49-58ab-4d5a-bc40-2cbde3096310" />

pod

<img width="356" alt="image" src="https://github.com/user-attachments/assets/6259e216-dcf2-48d3-9a56-20aa0748b37a" />

## mastre compnents
<img width="478" alt="image" src="https://github.com/user-attachments/assets/ae13db1a-c71d-465f-9d50-0112b11022f7" />

<img width="449" alt="image" src="https://github.com/user-attachments/assets/be83271f-21ec-42ff-bab2-0ab1128f009a" />

<img width="446" alt="image" src="https://github.com/user-attachments/assets/542b19cc-975f-4618-8579-a01e2ea92e52" />

<img width="169" alt="image" src="https://github.com/user-attachments/assets/69569590-965b-4f8d-8ffb-41ee7a4e343f" />

## https://www.youtube.com/watch?v=a-nWPre5QYI
**K8** -  clodu orchestrationa nd it is cloud agnostic it is generic u can it on AWS,GCP or digital ocean or in any of your cluster
ex-aws elastic container service file like config ,deployment file will not run as it is digital nocean
etcd is database and api server takes deployment config file and talks to controller which actually execute
containers actually run on worker node ,min 2 worker node should be ther

<img width="353" alt="image" src="https://github.com/user-attachments/assets/d09a0d63-ff1a-48de-9f48-8ab3f2309bbc" />

## steps 
1) Instruction (please start 2 container of nginix) goes to api server in an authenticated manner
2) controller will amke 2 pod and each will run nginix container
3) scheduler will asign each pod to worker machine under CRI by giving instruction to kubelet
4) kube proxy provide networking and traffic rule form Load balancer  to you worker node
5) when u agin give instructio tto  run 5 container of nginix ,api server will check from etcd that currently 2 are running so controllr will make 3 more pod and scheduler will distribute these pods to worker node again
6) In case of killing container api sevrer will give instruction to kubelet
7) CRI -container run time interface to run container using container runtime 
<img width="279" alt="image" src="https://github.com/user-attachments/assets/08e002a9-ac4b-436f-a336-2d85ac941e23" />
  CCM (cloud control manager) is part of control plane ,when u give instruction to api server that to craete load balancer as  this is not a job of k8s so api server will tell CCM to craete laod balancer , now CCM internally will talk to different cloud provider example if u need aws loadbalancer CCM will talk to aws api

<img width="369" alt="image" src="https://github.com/user-attachments/assets/e98110d0-7734-427a-a118-26152fbe4170" />















