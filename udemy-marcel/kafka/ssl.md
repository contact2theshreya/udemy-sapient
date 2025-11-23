How to pass sensitive data over internet to avoid hacking by middle man
So we use SSL/TLS

<img width="510" height="179" alt="image" src="https://github.com/user-attachments/assets/56c0fcb4-8b24-45c3-9536-7f2f63ec7a3d" />


Tls is successor to ssl

<img width="506" height="268" alt="image" src="https://github.com/user-attachments/assets/c4792745-c327-40ed-8803-b62450028f3f" />

<img width="565" height="203" alt="image" src="https://github.com/user-attachments/assets/e3617401-5c86-414a-bc24-adaa47fb08cd" />



Encryption – converting plain text information into coded form


<img width="385" height="197" alt="image" src="https://github.com/user-attachments/assets/afa6ca85-82a9-4d05-b9ea-4d4e4ac9c403" />

<img width="385" height="203" alt="image" src="https://github.com/user-attachments/assets/b4274217-bf4f-4263-b837-f9b1cf3f212a" />


 
Asymmetric -diff key is used

<img width="454" height="236" alt="image" src="https://github.com/user-attachments/assets/0c2dfa32-a55b-43f6-a545-255f79029cc6" />

<img width="461" height="186" alt="image" src="https://github.com/user-attachments/assets/c5b318b4-8d24-4a7b-8f3f-e17194f6c353" />


steps

<img width="359" height="172" alt="image" src="https://github.com/user-attachments/assets/9b94d36a-ca68-42f2-ad89-c826b998de67" />


1)	
2)	Swerver has public and private key,server keeps private key with it and transfer public key to client

<img width="458" height="241" alt="image" src="https://github.com/user-attachments/assets/26d8ab6c-148e-4cd0-93fe-4e501e89e36c" />


1)	
2)	Then browser will encypt data using publiuc key and server will decrypt using private key

<img width="369" height="208" alt="image" src="https://github.com/user-attachments/assets/52090494-86a2-4dcb-93c2-6e82e53b9a8c" />

<img width="499" height="242" alt="image" src="https://github.com/user-attachments/assets/f16e40a8-ec01-4b67-bc38-f6a859c51d5d" />

<img width="497" height="295" alt="image" src="https://github.com/user-attachments/assets/56d9b079-8e54-40c6-a96c-09d9165426a8" />

1)	
2)	

How integrity is maintained – send msg +hash(msg) to server now server will do hash(msg) if it matches with the prev hash then data is correct

<img width="430" height="191" alt="image" src="https://github.com/user-attachments/assets/dc8222a0-c097-4895-82c7-02607cd77511" />

<img width="511" height="290" alt="image" src="https://github.com/user-attachments/assets/9d811d8f-a929-45bf-90f1-a6f5dae26e30" />



Now server will use secret key and it finds 84 that means data is correct

<img width="495" height="199" alt="image" src="https://github.com/user-attachments/assets/92029054-7265-4933-8931-609341c292c6" />

<img width="395" height="229" alt="image" src="https://github.com/user-attachments/assets/c810899c-122c-4a1e-8ac4-fe436fa995b4" />

<img width="377" height="351" alt="image" src="https://github.com/user-attachments/assets/1cb90fb7-0ccf-4eb0-bc1d-223ea2d2a9d3" />

Server will send public key to CA and then CA will give him certificate then server will send certificate to client and client will verify certificate using fingerprint and all

<img width="531" height="370" alt="image" src="https://github.com/user-attachments/assets/e370463a-e7e8-4f43-b525-753b2ccab0e9" />

<img width="533" height="199" alt="image" src="https://github.com/user-attachments/assets/9463ff3f-4066-4c09-82d2-59c24f9343ff" />

<img width="357" height="181" alt="image" src="https://github.com/user-attachments/assets/f7da7a4c-ec98-4941-8b60-60bfd8e11f75" />

![Uploading image.png…]()

In asymmetric encryption ,server will send ouyblic key to client and client will make new key using public and will send to server and server will decrypt  so client key we encypted usingf server public key  and sent encypted data to server

But hacjer can attack here – when server will send public key to client ,hacker will stole the server public key and will send his public key to client
Client will encrypt his key with hackers public key  and will send encrypted key to server but in between hacker will stole the key and will put his public key in network and server will use his public key then

Soln is to use SSLA certificate

Server will send public key to CA to issue ceret
CA has its own pub and pri key
CA will keep server pub key in cert and sign it suing server pub key +CA  pub key

NOW server will send both public key and cert to client
Now client will go to CA as CA info is in certificate(issuer)
NOW CA  will send his pub lic kety to client and now client will check sign in certicateusing both publiuc key




