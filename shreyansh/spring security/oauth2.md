<img width="440" alt="image" src="https://github.com/user-attachments/assets/150e5619-a5fe-41c0-83b6-2f33998f1349" />

<img width="619" alt="image" src="https://github.com/user-attachments/assets/911e2dbf-efe3-49e2-bad3-04db0bae3b81" />

<img width="574" alt="image" src="https://github.com/user-attachments/assets/1f8f02e9-da26-45b0-af7c-d4ddeb7e8d39" />

<img width="576" alt="image" src="https://github.com/user-attachments/assets/de3969de-ed50-425e-b34a-56c1dd31296e" />

<img width="575" alt="image" src="https://github.com/user-attachments/assets/af571c4d-8233-4dd8-9bcd-357d39a7d21c" />

<img width="553" alt="image" src="https://github.com/user-attachments/assets/1bac1498-0beb-420e-b537-3b209780ea2a" />

<img width="606" alt="image" src="https://github.com/user-attachments/assets/83b78c2c-51c9-40bb-a2ed-b0ff6900e040" />

<img width="533" alt="image" src="https://github.com/user-attachments/assets/34cf8c3a-86db-4731-b9ad-a87e13b5d10a" />

<img width="517" alt="image" src="https://github.com/user-attachments/assets/0f872d69-d211-47ca-bede-8df50485d4c1" />

<img width="549" alt="image" src="https://github.com/user-attachments/assets/293849ae-f418-42bb-855f-538ab855a278" />

<img width="505" alt="image" src="https://github.com/user-attachments/assets/47465fe8-9f90-4a41-9999-85b0a1b83222" />

<img width="547" alt="image" src="https://github.com/user-attachments/assets/f886aedf-a624-442d-8592-c6da248aec78" />

<img width="531" alt="image" src="https://github.com/user-attachments/assets/274b6fa2-2aef-40ff-8944-44c7d6e8d7ff" />

<img width="459" alt="image" src="https://github.com/user-attachments/assets/a4d0d3e9-b39e-4738-a6db-864756c8675b" />

<img width="551" alt="image" src="https://github.com/user-attachments/assets/457b48af-193b-42d1-b1f5-da693dbf180e" />

## Resouce owne password credential - insta username and password is sent

<img width="493" alt="image" src="https://github.com/user-attachments/assets/38496b6b-2bf8-4b66-887f-7f7c536872fc" />

## Implicit grant
There is no refresh token in implicit grant so to get new token call the same api
<img width="480" alt="image" src="https://github.com/user-attachments/assets/c143bd8e-28c0-4f2e-bcdc-94fb6a499cd6" />

<img width="458" alt="image" src="https://github.com/user-attachments/assets/a47768bd-22d5-4b59-931e-e80108570cc4" />


<img width="476" alt="image" src="https://github.com/user-attachments/assets/7f6ebd31-652d-40f9-be8b-50f30320df65" />

<img width="352" alt="image" src="https://github.com/user-attachments/assets/dc06455a-77fd-4b97-9190-e463d013a31d" />

## Note
State is used to prevent csrf attack
If attacker calls authorixzn api to gmail server and in return it got authorisation code
And this code attacker has saved it and he did not use it
If valid user send to /authorui api and waiting for code and meanwhile attacker intercepted request and he sent his own authorise code and u get token from attacker code and using this token u will send to server and server will send attacker details so u will get signing to Insta using attacker
With state in response along with authorise code , if attacker state is not matched with  your state that u sent to authorisation api then authorise code is wrong

Client credential grant -  resource owner and client is same
