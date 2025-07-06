Authentication server- 3rd party application for token genration
Resource server - Your application

jwt IS stateless
sign withg private key and verify with public key(RSA)
HMAIC - secret key is used for bith generationa nd verificationb
jwt 0- b64(header).b64(payload).b64(claims)

<img width="664" alt="image" src="https://github.com/user-attachments/assets/8fc9a330-2575-431b-817f-f9c8497a00d1" />


<img width="579" alt="image" src="https://github.com/user-attachments/assets/ae7fe0be-376c-4e33-ae1d-f2bd5980be48" />


<img width="611" alt="image" src="https://github.com/user-attachments/assets/f4870292-d881-4259-a4ee-82d323ee0dd2" />


<img width="604" alt="image" src="https://github.com/user-attachments/assets/e672e4d1-47ba-43a6-8223-25d09f4a5132" />

In DB with jsessionid u store expiry time,roles,userid


<img width="655" alt="image" src="https://github.com/user-attachments/assets/23691158-cce1-4c01-b087-af0b8ef335b0" />

jsession id is steful coz it is stored in DB whereas JWT is stateless


<img width="543" alt="image" src="https://github.com/user-attachments/assets/95339a45-2ac1-4a23-bead-4e66955d85d5" />


<img width="650" alt="image" src="https://github.com/user-attachments/assets/fe53074e-80b5-40ef-b45d-854a7be5e342" />


<img width="426" alt="image" src="https://github.com/user-attachments/assets/583639c5-9a36-4a4a-baf3-ee1cd7cf4f6f" />


![image](https://github.com/user-attachments/assets/25035c19-73c9-4d8e-a355-d7788c48f370)

Never put confidential information inside payload
<img width="692" alt="image" src="https://github.com/user-attachments/assets/b25ee99f-e406-4c28-81bf-e0e30ad008c9" />


<img width="280" alt="image" src="https://github.com/user-attachments/assets/1b28e0e6-5b4c-498f-92f2-15e892c2566c" />


<img width="615" alt="image" src="https://github.com/user-attachments/assets/f43a5be7-d46d-4f5f-b05d-ad942e3bdaa9" />

Put any custom thing in custom payload like email, country, city
In private claim u put something inside it which can only be understood by internal people -private claim
Sign = RSA(B64HEADER.B64PAYLAOD,PRIV KEY/SECRET IN CASE OF HMAC)
now encode sign using b64 and put in JWT


<img width="596" alt="image" src="https://github.com/user-attachments/assets/c109f1ed-3363-4597-9d48-12d2c0c9a644" />


<img width="640" alt="image" src="https://github.com/user-attachments/assets/20a10c9d-cedd-4a8d-be39-506d6854ae5a" />


<img width="520" alt="image" src="https://github.com/user-attachments/assets/89edec51-5991-48e5-b35c-54923438287d" />


<img width="568" alt="image" src="https://github.com/user-attachments/assets/bc457be6-0148-41cc-9afc-c95ec5581743" />

IN sso u can pass same JWT to multiple application and they can verify it using same authentication server

For blackisited token tore their jwti,jwti is also used when u need to ensure token is used only once
Never use JWK coz attacked mayt change opaylaod and jwk



















