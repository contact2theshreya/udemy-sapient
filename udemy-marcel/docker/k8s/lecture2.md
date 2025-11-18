INTRO to K*S
What if container or VM goes down
Node is vm where workloads are running
node has pod(encapsulate>=1) container

Schedular – keep watching the request  to assign to pod
Api server – authentication,authorization (entry point)
Deployment controller – makes sure deployment is healthy
Lly namesoace controller and  node controller
Api server after assigning req – store entry in etcd about pod,request assigned ,pod status etc
Cri – receives req from kubelet and make sure to manage container lifecycle
Kube proxy  - to setup pod to pod ntw

1) brew install minikube//with mikube create control node and worker nodes
2) minikube start --nodes 2

<img width="666" height="313" alt="image" src="https://github.com/user-attachments/assets/23146734-fd04-4bd0-91de-be659f4c2ff1" />


Now use kubelet to interact with cluster
Install kubelet on mac
Brew I kubectl

<img width="864" height="166" alt="image" src="https://github.com/user-attachments/assets/f2ed7c29-6390-4617-b320-052425a06655" />


Now before creating pods, it will have control plane componentr running as pod and 1/1 means 1 container out of 1

<img width="940" height="424" alt="image" src="https://github.com/user-attachments/assets/a149e44a-de19-442b-84d5-2efdd2b975ba" />

Kind – k8s on docker(in docker engine we provisioned certain docker container as node of k8s it is lyt weight(each container will act like a node unlike micikube)

SET UP MULTI NODE k8s CLUSTER USING KIND
1—brew install kind
2—kind create cluster –name fist-cluster//it will create single node wjich act as both control and worker plane

<img width="689" height="273" alt="image" src="https://github.com/user-attachments/assets/5ef853d6-d0f1-4b24-9689-d8a5c0bcc33b" />


Now go inide this container using
Docker exec -it fits-cluster-contol-plane  sh
3—kind get cluster
Now create another cluster with multiple node using config.yaml file
kind create cluster --name my-first-kind --config config.yaml

<img width="940" height="483" alt="image" src="https://github.com/user-attachments/assets/c6a95701-d302-4ab9-b02e-fe5e50f40aa3" />







docs: https://kind.sigs.k8s.io/docs/user/quick-start/
https://raw.githubusercontent.com/kubernetes-sigs/kind/main/site/content/docs/user/kind-example-config.yaml
commands:
install kind
brew install kind
create a single node cluster
kind create cluster --name my-first-kind
kubectl cluster-info --context kind-my-first-kind
delete the cluster
kind delete cluster --name my-first-kind
create a cluster with 1 control plane and 2 worker nodes
kind create cluster --name my-first-kind --config config.yaml
list the clusters
kind get clusters//first-cluster,multi-node
switch the context
kubectl config use-context kind-first-cluster

## Create pod
1)	Imperative way – run 
Kubectl run –image=nginix nginix-pod
Kubectl describe pod/nginix//se metadata of pod

<img width="794" height="235" alt="image" src="https://github.com/user-attachments/assets/a08f74ac-e535-4e8d-8b11-2ecbcec8fb7a" />


Create pod.yasml file-declarative way

<img width="567" height="278" alt="image" src="https://github.com/user-attachments/assets/b2ba99b0-452c-45f2-aad9-e456a9500136" />

Kubectl create -f pod,yaml
Edit pod config
Kubectl edit <podname>
Now after edit pply change bu 
Kubectl apply -f <yaml file>
Go inside  pod
Kubectl ecec -it …

Pod version rolling update so that user wont be impacted

## Create deployment

<img width="634" height="273" alt="image" src="https://github.com/user-attachments/assets/b1ea174a-297a-45c3-862e-0dcb573de915" />

<img width="589" height="51" alt="image" src="https://github.com/user-attachments/assets/8242702a-ce41-4eb9-84af-d0bdbacb6b5d" />


Deployment is also created as pod

<img width="698" height="203" alt="image" src="https://github.com/user-attachments/assets/97e72188-4358-4662-adc8-3850ab47b3fd" />







Kubect get deploty
Scale deployment

<img width="485" height="48" alt="image" src="https://github.com/user-attachments/assets/f113eb33-8ff8-47be-83b1-6a1bc336a10c" />

<img width="940" height="476" alt="image" src="https://github.com/user-attachments/assets/38b6372e-3c22-425f-8a68-1ee625da7491" />

In deployment deploy pod sample with container nginix
In Kubernetes, a Pod file defines the smallest, single unit of deployment that runs a process, while a Deployment file acts as a higher-level manager that orchestrates and ensures the reliable operation, scaling, and self-healing of multiple Pods. 
Key Differences
Feature 	Pod File (YAML)	Deployment File (YAML)
Abstraction Level	Lowest level unit, runs containers.	Higher-level abstraction, manages Pods and ReplicaSets.
Lifecycle Mgmt	If a Pod crashes or is deleted, it is gone permanently and not replaced automatically.	Automatically replaces failed or terminated Pods to maintain a desired number of replicas (self-healing).
Scaling	Not designed for scaling; requires manual creation of multiple files or use of a controller.	Easily scalable by changing the replicas count in the file.
Updates	No built-in mechanisms for rolling updates or rollbacks; manual management is required.	Supports rolling updates and easy rollbacks to previous versions without downtime.
Use Case	Primarily for one-off tasks, testing, or debugging purposes.	Recommended for running long-running, stateless applications in production environments to ensure high availability and resilience.
Summary
•	A Pod file is the basic blueprint that tells Kubernetes how to run a container (or a group of related containers) with shared resources.
•	A Deployment file uses the Pod definition as a template within its own configuration (spec.template) to manage the application's overall desired state, availability, and lifecycle. 
For most real-world sce
Create deployment file

<img width="888" height="484" alt="image" src="https://github.com/user-attachments/assets/10c9ea4a-e0d8-4338-97cd-d0768da5eb77" />

 




To access the application first find IP of ythis pod

<img width="848" height="239" alt="image" src="https://github.com/user-attachments/assets/74d715ef-416c-42a4-9d47-368aa09406df" />


We have to expose this app to outside the deployment for that we need to create service

<img width="903" height="406" alt="image" src="https://github.com/user-attachments/assets/64507247-36ef-41a1-be7b-877ccb04d603" />

<img width="940" height="450" alt="image" src="https://github.com/user-attachments/assets/7c98de60-3da4-454a-8836-32c17af0fedc" />

Use env variable in yaml file and use it in applicxation code

Metrics server analyses load from pod or container runtime and give to api server and api server decides on the basis of threshold that whether it should perform horizontal scaling or vertical scaling



