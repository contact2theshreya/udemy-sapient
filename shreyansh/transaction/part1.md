<img width="587" alt="image" src="https://github.com/user-attachments/assets/3d161d5b-0b1d-4ac0-8a25-6fd0639fb032" />

even if transaction run in parallel,internally they will use locking to maintain a proper sequence
data jpa dependency will give @transactional ,and inside @Transaction code will be in critical section
<img width="237" alt="image" src="https://github.com/user-attachments/assets/050cf9dc-13bc-4f48-9cec-ed6d233b5602" />

Now there is boilerplate code above like begion/end transaction commit,so use @Transactional which internally uses this boilerplate code

<img width="575" alt="image" src="https://github.com/user-attachments/assets/532b8330-589c-4d20-bc2b-e018c81f3549" />

<img width="583" alt="image" src="https://github.com/user-attachments/assets/753c78c6-9b21-4b3c-bce7-f216384f25a0" />

<img width="564" alt="image" src="https://github.com/user-attachments/assets/0e5e1c87-e85b-4cfa-a088-a09437e04bb0" />

<img width="748" alt="image" src="https://github.com/user-attachments/assets/b0499bff-1f3a-41d9-b070-cee23dc2e882" />

<img width="726" alt="image" src="https://github.com/user-attachments/assets/1fdff7fb-3b0b-4cea-b49b-a82977283a40" />





