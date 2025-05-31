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

## https://www.youtube.com/watch?v=XuSQU5Grv1g
With docker you are able to run single instance of application using docker run command
with kubectl u can run 1000 instance of application with single command and can scale to 2000
<img width="498" alt="image" src="https://github.com/user-attachments/assets/4106e705-d94c-4dbc-a1fb-b702e2b28f93" />
can also do rolling update and then rollback them if required
With k8s u can define no of state of application running 

<img width="463" alt="image" src="https://github.com/user-attachments/assets/d7043bdb-9474-4774-860b-49c7fa924bdc" />

Node isworker  machine where k8s is installed where container is running,if node fails appl fails so have more than one node 
cluster is a set of nodes together,if any node is failed then load is shared with other nodes,now who manages all these?
control plane(master node) manages all worker
when u install k8s u install 4 component
1) Api server - FE of k8s,users,management devices,CLI
2) etcd-k8s store all data here to manage cluster in distriburted key value pair
3) controller-does actual business to monitor which node is running or crasha nd to bring up/down container
4) scheduler-distribute work across nodes
5) on worker node we have kubelet which is agent,it make sure that container are running on node as expected
6) kube proxy -maintain role on node to commun8cate worker node and container
7) container runtinme-responsible for running container
8) <img width="505" alt="image" src="https://github.com/user-attachments/assets/82a6ac7f-ef5c-4cf3-a465-a24654527cae" />

kubectl - command line tool of k8s,cmd to operate cluster

<img width="482" alt="image" src="https://github.com/user-attachments/assets/38685857-0192-4cde-b1b5-fdc7fa3ad3fb" />

<img width="410" alt="image" src="https://github.com/user-attachments/assets/b6571647-7cbd-46f0-808b-161b1b5433b6" />

Aim of k8s is to deploy containe rin machine,it does not deploy container directly to worker node,the containe ris encapsulated into a k87s object known as pods(single instance of application)
1 container means 1 pod
to scale create more pod

# create pod
kubectl run nginix --image=<image_name> // it will create pod and will deploy nginix container in it,imafe is downladed from docker hub
This is imperative way to craete object whereas declarative way is to run yaml file with the speciifoication of the object in code repo
lavel is imp to filetr pod

<img width="401" alt="image" src="https://github.com/user-attachments/assets/37bfe38d-0ce6-450b-aeba-c9c12f237e7d" />

<img width="440" alt="image" src="https://github.com/user-attachments/assets/d247e17a-ccfa-4383-ad17-b8e622bd4abd" />


<img width="452" alt="image" src="https://github.com/user-attachments/assets/5d6dfb08-d940-4fa7-b893-3c964ec59afb" />

# get lisr of pods
kubectl get pods

## Replica sets(entire cluster)
Baklance load,availibility,a pod has 1:1 relation with node
<img width="453" alt="image" src="https://github.com/user-attachments/assets/96768666-1fcd-417e-80f7-08450bf0bf4f" />

<img width="470" alt="image" src="https://github.com/user-attachments/assets/9f3c2bb4-d9a5-4f12-9bd3-d8aba6af74ab" />
match label says what kind of pod falls under replica

<img width="529" alt="image" src="https://github.com/user-attachments/assets/8c71f10c-36d8-44fd-84c5-616a7c33b7b1" />

Now pods are create dautomatically by replica sets
For replica set to know which pods to monitor create label in pod definirion and use tha in replica set
<img width="511" alt="image" src="https://github.com/user-attachments/assets/50607ae2-ed28-4b30-ba70-ce70f2873d95" />

<img width="434" alt="image" src="https://github.com/user-attachments/assets/247e538a-98c9-444d-b63f-8bb7bf8a07af" />

## Rolling update
upgrade one after other,undo update ,
<img width="254" alt="image" src="https://github.com/user-attachments/assets/47b5559c-ba3b-49fa-a531-d8de8d9260e5" />

<img width="479" alt="image" src="https://github.com/user-attachments/assets/5ed05f8a-ee23-47ba-94f7-a4b28b931160" />

To updatre image after deployment
<img width="563" alt="image" src="https://github.com/user-attachments/assets/8b1a5c75-aad6-4e2f-b101-c9627ef97811" />

IP address are assigned to pod automatically
If web server pod want to acees redis they cannot use IP hardoded of redis pod in code coz IP can change if pod crashes or restart so we create service(redis-db) which act as proxy
<img width="499" alt="image" src="https://github.com/user-attachments/assets/feb38593-761f-428b-b787-45e26a2750f0" />

## ClusterIp service
service within cluster example-redis db,not exposed externally
<img width="605" alt="image" src="https://github.com/user-attachments/assets/f61e7cf8-a31b-4b5a-a250-ca871e6fb404" />

U can link service to the pod using selector

<img width="610" alt="image" src="https://github.com/user-attachments/assets/7f1160af-e294-4a01-939f-89d952310846" />

<img width="607" alt="image" src="https://github.com/user-attachments/assets/ed99762d-4b90-4b97-b8fe-12a3b9d7afc7" />


## Nodeport service
service accesible to user through node port

<img width="601" alt="image" src="https://github.com/user-attachments/assets/b5ab041e-8180-4942-acd1-a3f1fe9213b2" />

<img width="640" alt="image" src="https://github.com/user-attachments/assets/b390aef7-2ede-4788-a2c2-008396efbd93" />

<img width="594" alt="image" src="https://github.com/user-attachments/assets/194c8376-ba46-4b62-9c18-42d4da8ced7d" />

<img width="595" alt="image" src="https://github.com/user-attachments/assets/a68499c1-3d49-4446-8768-dfdacb0ddb39" />


## LoadBalancer service

If after scaling we have 3 pod with same name then it automatically forward req in load balanced way to any of the pod using random algo

<img width="1037" alt="image" src="https://github.com/user-attachments/assets/f04c408c-d5ec-4d40-ae6d-22c4f3f03fc8" />

## Microservice
<img width="595" alt="image" src="https://github.com/user-attachments/assets/bb1b478f-476f-4535-85a6-d43b6d87adc8" />

<img width="646" alt="image" src="https://github.com/user-attachments/assets/a0dc2fbc-677a-4e70-88fd-46e88d16b146" />

Link contatiners so that they can be called by each other

<img width="646" alt="image" src="https://github.com/user-attachments/assets/68870547-1c10-481d-9e0f-8ea9666355ac" />

<img width="629" alt="image" src="https://github.com/user-attachments/assets/728f5b1a-e88d-477a-b8d2-086ec5873c14" />

<img width="1078" alt="image" src="https://github.com/user-attachments/assets/89f8272e-0460-4663-b1e4-06dcbbb26954" />

create service for postgresql and redis sot heat they can be accessed by other pods

<img width="1078" alt="image" src="https://github.com/user-attachments/assets/be3e6fb2-8132-4caa-b68d-033ec8eee369" />

<img width="642" alt="image" src="https://github.com/user-attachments/assets/10148bd3-f7c8-4204-9d7c-22a70c15fb92" />

A service is required if we want to expose some of its service to other

<img width="842" alt="image" src="https://github.com/user-attachments/assets/72e1feda-25c0-4bac-9a18-49a00e997b7b" />

<img width="524" alt="image" src="https://github.com/user-attachments/assets/7042a6d8-af91-4944-ac38-672524f19e99" />

<img width="566" alt="image" src="https://github.com/user-attachments/assets/b8991936-82e7-4cba-a953-e1c65cbe549e" />

<img width="518" alt="image" src="https://github.com/user-attachments/assets/2807f83e-fa0b-4440-9247-1805f27691bc" />

<img width="520" alt="image" src="https://github.com/user-attachments/assets/1b7644e0-1738-40c2-9efc-fefecbe20bcc" />


![image](https://github.com/user-attachments/assets/9097cc07-6043-4b4c-94fd-80e0305e1c8a)

<img width="461" alt="image" src="https://github.com/user-attachments/assets/8021795a-a45b-4733-8fc5-4c62a99f2fdf" />

<img width="483" alt="image" src="https://github.com/user-attachments/assets/4f16db9f-bf23-4845-bd4e-a91967165ac4" />

<img width="434" alt="image" src="https://github.com/user-attachments/assets/6be0b2ad-3d10-464a-8e2b-ef0998cce9b6" />

Add type nodeport in result and vote app service

<img width="210" alt="image" src="https://github.com/user-attachments/assets/3937d71f-304e-4d7f-b350-2dd7ddfcd16c" />



















































