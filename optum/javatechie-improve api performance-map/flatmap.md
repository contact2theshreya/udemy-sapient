Multithreading Hands-On Example | Improve API Performance

https://github.com/Java-Techie-jt/api-performance-demo/tree/main
https://www.youtube.com/watch?v=8WGJV2N08eQ&list=RDMMhNRG-CM4_yQ&index=4
<img width="468" height="250" alt="image" src="https://github.com/user-attachments/assets/e9c0cbf7-4540-41ba-b044-3bfa16348e3f" />

<img width="236" height="142" alt="image" src="https://github.com/user-attachments/assets/0383e299-0538-4e1f-bad9-5bc209c3f6f4" />

Here main thread will be block until each response is written , since it’s a synchronous call
Solution – each in diff thread concurtrently
<img width="468" height="75" alt="image" src="https://github.com/user-attachments/assets/559e14ce-685c-4ec2-b008-def5206e1838" />

<img width="267" height="156" alt="image" src="https://github.com/user-attachments/assets/70c0f1c2-cba9-41b4-aed0-cc37c7bf870c" />


Here v1 endpoint is sync and v2 is async by completable future ,we are calling each one in sepearte thread and once each completes we are returning result

Async approach is taking less time  rather than sync
<img width="468" height="142" alt="image" src="https://github.com/user-attachments/assets/4ddf30e0-7d48-4397-a57a-b19ac1c083ec" />

<img width="452" height="264" alt="image" src="https://github.com/user-attachments/assets/673dd4eb-c5ae-4c35-a31a-40defed2d6b6" />


https://www.youtube.com/watch?v=CwvlS3ViGFQ

Map – 1:1 mapping i.e u i/p 1 and o/p 1
Flatmap – 1:M – for 1 i/p we get multiple out ex phone number array in customer so in .map(cut->cust.pno) will give –[[pno1,pno2]]

With flatmap – [pno1,pno2]
<img width="468" height="217" alt="image" src="https://github.com/user-attachments/assets/346d4a78-e484-4bd9-a3f9-a0c0d4a8163d" />


<img width="452" height="182" alt="image" src="https://github.com/user-attachments/assets/b55a6b5d-5fd3-4aed-9d52-8d11c7689863" />


<img width="443" height="326" alt="image" src="https://github.com/user-attachments/assets/74c75561-4a6f-45ab-b998-2db1a07a81e4" />


<img width="452" height="202" alt="image" src="https://github.com/user-attachments/assets/fa46ee1f-b973-4fde-8049-f9739ff1cd57" />

<img width="452" height="232" alt="image" src="https://github.com/user-attachments/assets/f03f329a-1095-40ea-a058-4dbec030c769" />


<img width="452" height="255" alt="image" src="https://github.com/user-attachments/assets/f0af2929-94fb-4e7f-8021-478a66400a65" />

# optional

<img width="325" height="94" alt="image" src="https://github.com/user-attachments/assets/af3dc185-d71a-49c7-8cdf-7aea0bb649d4" />

In of() it will do a null check and if null found then it will throw NPE<img width="468" height="50" alt="image" src="https://github.com/user-attachments/assets/6bf132b6-2979-4290-91ac-af0c6d9d1fb5" />

<img width="452" height="176" alt="image" src="https://github.com/user-attachments/assets/5027a4e6-88f6-41cc-86d3-dda81f1dac7d" />

No such value present exception  in .get() if no email found<img width="468" height="25" alt="image" src="https://github.com/user-attachments/assets/a66544d6-50bc-404b-b71a-7659c5076b28" />

<img width="414" height="108" alt="image" src="https://github.com/user-attachments/assets/c2725c82-27da-47dc-8745-d61bdf1c3443" />


So use orelse
<img width="468" height="75" alt="image" src="https://github.com/user-attachments/assets/25869eca-d644-43ea-858b-2f0a1cc022db" />

<img width="378" height="49" alt="image" src="https://github.com/user-attachments/assets/6238345a-192f-4e71-99cd-823df228c1f6" />
