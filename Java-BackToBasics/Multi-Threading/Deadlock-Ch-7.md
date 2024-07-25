# Deadlock

<img width="1097" alt="Screenshot 2024-07-25 at 8 43 42 PM" src="https://github.com/user-attachments/assets/0bd430d6-dac0-49fc-b1d9-d6a178aadbb3">
<img width="1072" alt="Screenshot 2024-07-25 at 8 44 34 PM" src="https://github.com/user-attachments/assets/55208f23-0458-4bc3-961d-e1946fbf2b9e">

### Q. Create a program in Java depicting the Deadlock situation.

<img width="787" alt="Screenshot 2024-07-25 at 8 47 34 PM" src="https://github.com/user-attachments/assets/1a4253cc-169e-427e-a802-1434189151e4">
<img width="571" alt="Screenshot 2024-07-25 at 8 47 40 PM" src="https://github.com/user-attachments/assets/d317228b-a553-4a23-ab03-b64e1415baef">

This program would never end as both the locks would keep on waiting for the other lock to relinquish. Both of the threads are now in 
"blocked-for-lock-aquisition" state.

If the order of locks is the same, we will get rid of the Deadlock situation.

<img width="818" alt="Screenshot 2024-07-25 at 8 49 30 PM" src="https://github.com/user-attachments/assets/e0ee46d9-e494-4101-a04e-2436f96b1e66">
<img width="568" alt="Screenshot 2024-07-25 at 8 49 39 PM" src="https://github.com/user-attachments/assets/6acd95b2-2929-4910-9492-6a1b77d86a8f">
