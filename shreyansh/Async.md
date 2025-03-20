<img width="606" alt="image" src="https://github.com/user-attachments/assets/fe09ac18-9c14-487a-a25d-50a83cb81645" />

<img width="625" alt="image" src="https://github.com/user-attachments/assets/31132250-49ff-4e6f-aa8f-584995d761f4" />

thread from the pool will pick task from queue,as thread1 and 2 has picked task 1 and 2 , now task3 to 5 will go in queue and when task 6 will come 
 as queu is full and max pool size is 4 so thread 3 will pick task 6

 <img width="518" alt="image" src="https://github.com/user-attachments/assets/d55c69de-2086-45f9-9196-aa45be2b5381" />

 <img width="560" alt="image" src="https://github.com/user-attachments/assets/b2cf62b4-978a-4786-ab11-61f857a05191" />

 <img width="529" alt="image" src="https://github.com/user-attachments/assets/91e9ae65-4d3d-47ea-a073-e96c1f122829" />

 when @Enableasync annotation is present , it will create bean for async classes,everytime u het that method new thread will be created

 <img width="549" alt="image" src="https://github.com/user-attachments/assets/8a9cbbec-a81f-447e-bf95-d1d795a43a30" />

 Default executor-threadpool with min max pool size

<img width="527" alt="image" src="https://github.com/user-attachments/assets/2b6adb7b-c79f-4f64-9ee4-72322559d0ab" />

<img width="620" alt="image" src="https://github.com/user-attachments/assets/8cc10ffc-6ff4-4ae3-a5f7-f2957182f4bc" />

<img width="566" alt="image" src="https://github.com/user-attachments/assets/0c80940d-d834-4a5a-a41d-7a6b4412cee3" />

as corepool size is 8 of default thread pool executor that's why in above out till task 8 are present, then it will get repeated

<img width="593" alt="image" src="https://github.com/user-attachments/assets/b2935293-077d-44c4-8cf4-b1bf034ef07e" />

To overcome drawback of default threadpool executor we will make our own threadpool executor

<img width="598" alt="image" src="https://github.com/user-attachments/assets/0646293f-8ec2-4047-8ba7-cdac459bebd7" />

<img width="581" alt="image" src="https://github.com/user-attachments/assets/0e99eb78-aab0-4ea6-a885-675f317d144e" />

<img width="563" alt="image" src="https://github.com/user-attachments/assets/96c1271d-bf37-429a-b524-c7f7869ba045" />

<img width="559" alt="image" src="https://github.com/user-attachments/assets/e97d32c3-e2b8-42d0-9a63-8a904f0ae7e3" />

<img width="550" alt="image" src="https://github.com/user-attachments/assets/0339afbc-daff-45fc-8279-c83fe442a1c6" />

<img width="565" alt="image" src="https://github.com/user-attachments/assets/059a716b-1593-4457-a670-a3265e4c1d71" />






<img width="566" alt="image" src="https://github.com/user-attachments/assets/58602f41-c10b-429b-8220-cc2e56e3cd01" />












