## Resources
https://www.youtube.com/watch?v=ylEy4eLdhFs

<img width="464" height="214" alt="image" src="https://github.com/user-attachments/assets/f842264f-44fd-4aaa-a226-e5523a5de563" />

with jenkins-build ,deploy,test and release jobs can be done but now all these can be done with github action

In the repo create a .github/workflow folder
click on setup a workflow

<img width="1094" height="566" alt="image" src="https://github.com/user-attachments/assets/9957ebe0-d4bc-4f11-b993-ce6bddebc155" />

<img width="544" height="219" alt="image" src="https://github.com/user-attachments/assets/0e02c0b4-b290-43bd-9cab-9025fab6e765" />

<img width="967" height="547" alt="image" src="https://github.com/user-attachments/assets/2d528d91-34f0-4c8c-9ee9-a92ab0b1c487" />
whenever something push on this repo this job will be run which is in yaml file


<img width="806" height="507" alt="image" src="https://github.com/user-attachments/assets/3d2e7fbb-02fa-4ff3-b9fc-ae17433b083e" />

<img width="791" height="404" alt="image" src="https://github.com/user-attachments/assets/49e4242f-27ba-4228-9cdf-a9b7511cbdc6" />

name: hello-world
on: push
jobs:
  my-job:
    runs-on: ubuntu-latest
    steps:
      - name: my-step
        run: echo "Hello World!"
