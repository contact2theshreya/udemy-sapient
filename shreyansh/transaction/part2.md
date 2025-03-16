if u dont want spring to automatically choose transaction managaer , then u can tell spring by creating a bean of datasourcemanager
if u are using @transaction on method which contains externa aapi call which is time taking then your application will choke coz api call is taking more time to resolve 
so use programmatic way in this case
Use transaction template which is wrapper around start,end and commit transaction u dont need to write it explicitly
transactiontemplet execute method takes callback
in programmatic way u can provide transaction propagatioin in 2 wqat

<img width="568" alt="image" src="https://github.com/user-attachments/assets/f9cad8e1-e24e-4bfc-b2e1-de1f76e31eb0" />

<img width="655" alt="image" src="https://github.com/user-attachments/assets/12246d0e-5112-45be-a596-08c41dfd9629" />

<img width="523" alt="image" src="https://github.com/user-attachments/assets/2ca1ff44-d8b9-4445-85d3-000096dc8880" />

<img width="539" alt="image" src="https://github.com/user-attachments/assets/f2c1ebac-7a47-4833-a1e1-b1ada2dd4527" />

<img width="572" alt="image" src="https://github.com/user-attachments/assets/dbfdb323-6361-4d5d-8c4b-fd9ed3959da2" />

<img width="550" alt="image" src="https://github.com/user-attachments/assets/154ddf18-d1e5-4a62-83a7-362fa23945d6" />

<img width="626" alt="image" src="https://github.com/user-attachments/assets/e66fe327-7bfc-4648-853b-ba4e4f9e2c37" />

<img width="517" alt="image" src="https://github.com/user-attachments/assets/4d88c697-1e54-454d-b2a8-9b71eb1e32d8" />

<img width="544" alt="image" src="https://github.com/user-attachments/assets/2cb886fd-ddb5-4aff-9305-de1f725e2357" />

<img width="596" alt="image" src="https://github.com/user-attachments/assets/1bc0bf9d-b923-4af4-b873-994609e46aab" />

<img width="521" alt="image" src="https://github.com/user-attachments/assets/5a2ba071-fdf0-4645-bd1a-dc8f060e60f5" />










