# Ways to take input from user

1. *Using read() method in InputStream:* It prints the ASCII value and we have to manually change it to print the correct value.

   <img width="956" alt="Screenshot 2024-09-11 at 6 40 58 PM" src="https://github.com/user-attachments/assets/5dafa646-7ced-46c5-b6e5-f099ec756593">

2. *By creating an object of Scanner class*
3. *By creating an object of BufferedReader class*:

   <img width="790" alt="Screenshot 2024-09-11 at 6 41 54 PM" src="https://github.com/user-attachments/assets/1344285b-f8b8-42bb-8901-32a50c3f76bb">

# Scanner Vs BufferedReader

There are some differences between the 2 as follows - 
- BufferedReader is synchronous while Scanner is not.
- BufferedReader should be used if we are working with multiple threads.
- BufferedReader has significantly larger buffer memory than Scanner.
- The Scanner has a little buffer (1KB char buffer) as opposed to the BufferedReader (8KB byte buffer), but it’s more than enough.
- BufferedReader is a bit faster as compared to scanner because scanner does parsing of input data and BufferedReader simply reads sequence of characters.

<img width="996" alt="Screenshot 2024-09-11 at 6 22 21 PM" src="https://github.com/user-attachments/assets/efee6f24-2b32-428b-bb12-d99eb3906ffa">
<img width="929" alt="Screenshot 2024-09-11 at 6 23 04 PM" src="https://github.com/user-attachments/assets/6ec749bc-0a3d-4f03-8774-50dcfc121597">
<img width="1007" alt="Screenshot 2024-09-11 at 6 23 40 PM" src="https://github.com/user-attachments/assets/5a106fea-b4fa-4586-bfbb-98d8fec6f658">
<img width="969" alt="Screenshot 2024-09-11 at 6 24 27 PM" src="https://github.com/user-attachments/assets/147faec2-db74-4793-9201-b69bfc6de62d">
<img width="836" alt="Screenshot 2024-09-11 at 6 25 29 PM" src="https://github.com/user-attachments/assets/1dfacbee-fc31-4d80-bc93-444378866cf6">

# Note

In Java, when using a Scanner object (sc) to take input from the user, you need to use sc.nextLine() after sc.next() to consume the remaining newline character in the input buffer. This is because sc.next() reads the input until the next whitespace character, but doesn't consume the whitespace character itself. The sc.nextLine() call then reads the rest of the line, effectively clearing the buffer and allowing the next input operation to work correctly. Failing to do so can result in unexpected behavior, such as multiple inputs being treated as one.
