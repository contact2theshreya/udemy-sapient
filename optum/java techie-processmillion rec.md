Multithreading | Process Millions of Records in Batches | Hands-on Example<img width="468" height="73" alt="image" src="https://github.com/user-attachments/assets/c8b1d9d0-10c5-44b5-a7d4-5bb33fa9ff75" />


https://youtu.be/qaSBljS6SZk<img width="468" height="50" alt="image" src="https://github.com/user-attachments/assets/bf45fae8-77dc-4727-9117-ed3fe3f15f38" />

<img width="452" height="239" alt="image" src="https://github.com/user-attachments/assets/19759a01-edf1-4b4f-b5c1-f15872be06e7" />

\<img width="237" height="154" alt="image" src="https://github.com/user-attachments/assets/8e621b92-6a6b-42ed-803f-cc8a5cc16809" />


If the entire task executes in single thread then it will take lot of time
U can use parallel stream to increase concurrency
<img width="468" height="75" alt="image" src="https://github.com/user-attachments/assets/111e1b4c-3fc4-4ce1-9431-719f9a53f2d8" />

<img width="452" height="314" alt="image" src="https://github.com/user-attachments/assets/73a37800-8784-4689-b4de-cf0bbd0ae074" />

But this is not a good approach , so process result in batches by thread to process concurrently<img width="468" height="67" alt="image" src="https://github.com/user-attachments/assets/74475d57-b388-4d85-a8d9-83a13569b38a" />

<img width="452" height="234" alt="image" src="https://github.com/user-attachments/assets/5f0f771f-d0dd-4b97-a7e2-7f473c4cfd4e" />

<img width="452" height="146" alt="image" src="https://github.com/user-attachments/assets/c4d1bad5-1ca2-4ea2-a502-d565e837e8cb" />


Add controller to call this method
https://github.com/Java-Techie-jt/order-batch-processing
Now it took 3.9 sec with yraditional approach(w/o batych)
<img width="468" height="100" alt="image" src="https://github.com/user-attachments/assets/77b038dd-854b-4cb2-a872-f996dd0af5eb" />

<img width="452" height="253" alt="image" src="https://github.com/user-attachments/assets/7c493d1e-f2c5-4ccf-af71-b195e4be6c54" />


Now use parallestream – it will spin up random no of thread from core and pull thread from forkjoinpool(execution time-2.28sec)
<img width="452" height="107" alt="image" src="https://github.com/user-attachments/assets/0d06ef21-8d7e-4bfd-b390-897584e733e1" />


<img width="468" height="75" alt="image" src="https://github.com/user-attachments/assets/0765c195-30ca-4b4d-b733-01b8107dd426" />



Now do batching
<img width="452" height="128" alt="image" src="https://github.com/user-attachments/assets/dd353749-d7d9-4368-ad71-3b4d41fe0565" />

<img width="468" height="50" alt="image" src="https://github.com/user-attachments/assets/3c311dcc-d5a9-4478-a9b1-44582cf494cc" />

Make batch<img width="452" height="195" alt="image" src="https://github.com/user-attachments/assets/a11fbc8e-c590-49d4-9a57-0d5eb601cb9d" />


supplkyAsync needs return type but not runasync
<img width="468" height="75" alt="image" src="https://github.com/user-attachments/assets/90e9ca89-47a8-4b68-ae2a-593bbd547f6b" />


<img width="452" height="86" alt="image" src="https://github.com/user-attachments/assets/7f04c55a-fef8-4ce9-9ab4-cab232eebbb2" />

<img width="468" height="50" alt="image" src="https://github.com/user-attachments/assets/d5455b38-822e-40cd-94de-3a5c45458f3a" />

With batches ececution time is 913ms<img width="452" height="243" alt="image" src="https://github.com/user-attachments/assets/0279f29c-d653-4e7c-933f-5240984c374c" />

<img width="468" height="50" alt="image" src="https://github.com/user-attachments/assets/4eeed056-5c03-4da0-922f-cbb11992f084" />


Nou u can use your threadpool(custom thread name)<img width="451" height="317" alt="image" src="https://github.com/user-attachments/assets/f0508d2b-7f42-4244-bf4f-80c556958a4b" />


private final ExecutorService executorService = Executors.newFixedThreadPool(6 );
  List<CompletableFuture<Void>> futures = batches
                .stream()
                .map(
                        batch -> CompletableFuture.runAsync(() -> processProductIds(batch),executorService))
                .collect(Collectors.toList());





![Uploading image.png…]()

