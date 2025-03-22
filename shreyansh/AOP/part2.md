<img width="578" alt="image" src="https://github.com/user-attachments/assets/5dd6c17e-1c54-4a4c-b8d5-5a01ea521fef" />

we can see that in output thread name are same not different which is incorrect coz async creates new thread

<img width="607" alt="image" src="https://github.com/user-attachments/assets/567b464e-1510-4d9c-89dc-1aabec8120ba" />

with transaction and asyncc ->async child method will not be in transaction environment so any failiure happens on 
update user method it will not be rollbacked

<img width="568" alt="image" src="https://github.com/user-attachments/assets/a90fbf8e-6113-4c20-9ef8-54f604466097" />

Now usecase 3 is the safe way to use async with transactional annotation coz main thread is free when it call async method and it can proceed further and inside async we are using transaction so it will be managed by same thread
so it is used industry wise
<img width="588" alt="image" src="https://github.com/user-attachments/assets/aaba161a-112e-4952-b1c6-e17fd5a70882" />

Both future and completable future can be the return type of async method

<img width="555" alt="image" src="https://github.com/user-attachments/assets/43a0c002-58af-4437-aa1e-8aa4fe7a1387" />

<img width="455" alt="image" src="https://github.com/user-attachments/assets/4ad6a9cb-9f6b-4305-9634-cccae6ef4639" />

<img width="563" alt="image" src="https://github.com/user-attachments/assets/03bd434f-9c15-42a4-a9c3-3af4bde9bd46" />

<img width="727" alt="image" src="https://github.com/user-attachments/assets/ee2c3486-efed-4fff-9b97-02ff2597a884" />

<img width="419" alt="image" src="https://github.com/user-attachments/assets/a6fd06e4-9ea8-4575-b039-67e53e15092f" />

<img width="761" alt="image" src="https://github.com/user-attachments/assets/f911c6d9-8021-4629-8ce2-570f351e27db" />

<img width="581" alt="image" src="https://github.com/user-attachments/assets/71bf3323-5e98-4aca-9fbe-f377f5ab3f4f" />

<img width="694" alt="image" src="https://github.com/user-attachments/assets/5f769e77-40f0-4209-8062-31faf4e4b5dc" />










