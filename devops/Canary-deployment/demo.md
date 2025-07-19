## resopurces
https://www.youtube.com/watch?v=0QhUhrWGB9k

Deployment strategy - rolling update,canary ,blue green

If version1 with 4 replica is deployed in k8s cluster and now v2 came and if u don’t follow any strategy then u remive v1 and its 4 replica now u install v2 with 4 copy so install and uninstall if it takes 10 min (service down for 10 min)

So use deployment strategy to reduce downtime

## Rolling update  - near zero downtime(Default strategy)
instead of uninstalling prev version , it will add by default 25% of new copy(r5) of v2 and hen r5 is ready it will replace r4 of v1
with r5 of v2

<img width="346" height="210" alt="image" src="https://github.com/user-attachments/assets/3b624332-faa1-4f25-98d8-384bfe2e9e48" />

So version 1 iwith 3 copy is still serving traffic when we replace v2 replica with v4
1replica - 25%
Use redness probe in k8s to define when r5 is ready

Make 4 replica of nginix
<img width="394" height="88" alt="image" src="https://github.com/user-attachments/assets/020743c0-c412-495e-b852-12795ca009c7" />

<img width="500" height="332" alt="image" src="https://github.com/user-attachments/assets/50fdd967-e5d6-4309-8979-e69a4ac1c5c5" />

do kubectl edit deploy and change image name of v2 and u wil see now rolling update has started and only one replica of v1 got terminated

## canary
<img width="470" height="261" alt="image" src="https://github.com/user-attachments/assets/db6a2702-2d6b-48b2-8700-fc5883796d8b" />

LOADBALANCER

<img width="546" height="164" alt="image" src="https://github.com/user-attachments/assets/10b439d1-68d2-4dd9-b04e-b83ecc2acea9" />
create deploy,service,inges of each version
<img width="459" height="127" alt="image" src="https://github.com/user-attachments/assets/6b8a8451-f671-416b-ba5a-430afc8091c3" />

use below steps

https://kubernetes.github.io/ingress-nginx/examples/canary/

https://www.techtarget.com/searchitoperations/answer/When-to-use-canary-vs-blue-green-vs-rolling-deployment
