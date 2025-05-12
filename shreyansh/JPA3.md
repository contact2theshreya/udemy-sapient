## Important notes
1) Flush means commit so till flush happens everytghing happends in memory(persistent context) not in DB
2) 1 Entity mnager is 1 persistent context
3) entity manager internally creates persistent context
4) Afetr @Transaction commt ha happened so the data is saved in DB
5) there is one usecase that if we first insert then select data in same HTTP request then only insert query is fired but not select coz after insertion we already have object in persistent context so at the time of select we dont see
6) select query that is it doesnt hit DB
7) dispatcher servlet during app startup creates entitymanager so for each HTTP request one entitymanager is created
8) if select query is written in new HTTPO req(api) then u will see select query coz new entitymanager is now created
9) each entity manager has its own persistent context and they are isoltad with anothger entity manager
10) <img width="551" alt="image" src="https://github.com/user-attachments/assets/15462d3a-9f91-41bd-ae48-a70f5cafbbb6" />

11) <img width="955" alt="image" src="https://github.com/user-attachments/assets/f1255166-632e-428c-b395-c4b96218af09" />

<img width="720" alt="image" src="https://github.com/user-attachments/assets/a8575a31-70d5-4df7-be37-852ed1d33d93" />

<img width="860" alt="image" src="https://github.com/user-attachments/assets/ca3db7bd-8b79-47f8-9f1d-e880b8195e0e" />

<img width="862" alt="image" src="https://github.com/user-attachments/assets/5fdecb48-9c6c-40bb-a65e-9c9b99cf3c0d" />

<img width="869" alt="image" src="https://github.com/user-attachments/assets/c9f1bb41-b674-4122-8119-622efd8ca70b" />

<img width="833" alt="image" src="https://github.com/user-attachments/assets/1e85e82f-817b-464f-8e20-c1d574729281" />

<img width="882" alt="image" src="https://github.com/user-attachments/assets/52b98b62-35f6-4d73-87f1-1f3231f2f298" />

<img width="784" alt="image" src="https://github.com/user-attachments/assets/24b83a7b-b38f-4068-8031-5ec8e1479e75" />

<img width="735" alt="image" src="https://github.com/user-attachments/assets/9662866f-18f0-411d-83ad-639159782787" />

<img width="800" alt="image" src="https://github.com/user-attachments/assets/a7c7632d-b5ba-4d93-b09f-d8ed44a9f940" />

<img width="742" alt="image" src="https://github.com/user-attachments/assets/d9b23a87-c0b4-4e40-a080-8ac6dfa95473" />

<img width="838" alt="image" src="https://github.com/user-attachments/assets/2b0644d4-d127-41b9-a530-ae6720c767be" />

<img width="898" alt="image" src="https://github.com/user-attachments/assets/6ba7b669-0cea-4c9d-9985-205c54958b93" />

<img width="787" alt="image" src="https://github.com/user-attachments/assets/693f42a7-82db-4b10-960a-4c807844ddc4" />













