Create ec2 instances of all 3

<img width="940" height="343" alt="image" src="https://github.com/user-attachments/assets/e4c94c0a-c51b-40a3-954a-61e31f268b87" />

From local connect to Jenkins instance by passing Jenkins IP the install Jenkins 

<img width="940" height="210" alt="image" src="https://github.com/user-attachments/assets/a6974d91-92b6-437f-bfd3-a6da7b690e88" />



Allow port 8080 to access Jenkins and install plugins

<img width="940" height="534" alt="image" src="https://github.com/user-attachments/assets/7f0daf8a-9743-4572-a2aa-f8265f36b899" />


Now open jenkis using jenkinsapi:8080,install plugins->create pipeline by giving git repo,branch and enable github hook trigger in Jenkins  to enable pipeline automatticaly whenever code changes  and add github webhook using Jenkins url in github

<img width="940" height="527" alt="image" src="https://github.com/user-attachments/assets/738a3ae4-446b-4b1c-b5f8-6f090a66ef4f" />

<img width="940" height="483" alt="image" src="https://github.com/user-attachments/assets/0a51504e-4f16-4f63-aa09-fe9abc455c49" />



Now connmect to soanrcube instance and install java and sonarcute duwload using curl command then start sonarcube using command
Allow its port from ec2 instance by adding inboiund rule in security group of that instance
Now go to sonarcubeIp:port in browser to aces sonarcube,now create project yhere and integrate with jenkins

<img width="940" height="506" alt="image" src="https://github.com/user-attachments/assets/9cf5eebc-7940-494a-9aea-ad03f20a7d9b" />


Add sonarcube scanner and ssh2easy plugin in Jenkins adna dd sonar sewrver that u created in ec2 in Jenkins and in build step of Jenkins add sonarscanner step
Add doscerfile in project
Now install docker in docker ec2 and add it in Jenkins and in postbuild step add this

<img width="940" height="559" alt="image" src="https://github.com/user-attachments/assets/4aed72a8-2376-4231-a393-ac3bd16f82b3" />


https://www.geeksforgeeks.org/devops/introduction-to-jenkins-pipeline-as-code-jenkinsfile/
/////////////////////////////////////////////////////
<img width="940" height="499" alt="image" src="https://github.com/user-attachments/assets/0274afd6-8fe5-46d0-b248-7081f5d1191f" />


Deploy to k8s using argocd
This is for 1 branch

<img width="940" height="539" alt="image" src="https://github.com/user-attachments/assets/a8f170c4-0c6c-4739-b681-4027433c2f40" />

<img width="940" height="551" alt="image" src="https://github.com/user-attachments/assets/653ccdb4-df6f-4edd-a185-46b8d92511ce" />



https://github.com/iam-veeramalla/Jenkins-Zero-To-Hero/blob/main/Interview_Questions.md
https://github.com/iam-veeramalla/Jenkins-Zero-To-Hero/blob/main/README.md

<img width="940" height="527" alt="image" src="https://github.com/user-attachments/assets/8f26d1ed-789a-46d0-98af-f25b4deeb552" />

And give repository url tro access jenkinsfile of your repo
https://github.com/iam-veeramalla/Jenkins-Zero-To-Hero/blob/main/java-maven-sonar-argocd-helm-k8s/spring-boot-app/JenkinsFile(has all task of CI)
in argocd,give repo url,cluster path and manifest file path
https://medium.com/@muppedaanvesh/a-hands-on-guide-to-argocd-on-kubernetes-part-1-%EF%B8%8F-7a80c1b0ac98

RESOUCE - https://youtu.be/icZUzgtz_d8
Llar to Jenkins slave we have runner in git action which is VM to execute our build command in pipeline 
Runner can be shared like ubuntu/windows latest or private runner where u create own VM

<img width="940" height="474" alt="image" src="https://github.com/user-attachments/assets/4b54ebba-bd58-437b-af99-720e7155d62b" />


https://github.com/jaiswaladi246/Github-Actions-Project/blob/main/.github/workflows/cicd.yml
u can create your own runner hwere


<img width="940" height="525" alt="image" src="https://github.com/user-attachments/assets/40e993c6-c1bc-44df-935c-accb9070abe7" />

<img width="940" height="498" alt="image" src="https://github.com/user-attachments/assets/1fcffc19-9f30-4a59-8c2e-fd15da54ab54" />

## Canary deployment raed
https://medium.com/@bounouh.fedi/a-practical-guide-to-canary-deployments-in-kubernetes-4c6fe9070df2
