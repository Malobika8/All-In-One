# Streams

<img width="994" alt="Screenshot 2024-09-12 at 4 16 31 PM" src="https://github.com/user-attachments/assets/aab21f75-e80f-4207-ad84-84e9ede65fd8">

Java has 2 types of Streams(abstract classes)

<img width="1011" alt="Screenshot 2024-09-12 at 4 16 39 PM" src="https://github.com/user-attachments/assets/9de14fc4-2968-4678-8b25-185bb155fd5f">

- ByteStream: Used to handle input & output of bytes of data. Example: reading an image, reading a pdf file etc. It contains binary data.

  * InputStream (Abstract Class)

    <img width="1140" alt="Screenshot 2024-09-12 at 4 24 25 PM" src="https://github.com/user-attachments/assets/29b00e54-263c-4417-b3cf-7fed4da8799d">
    <img width="1113" alt="Screenshot 2024-09-12 at 4 26 47 PM" src="https://github.com/user-attachments/assets/d73c250a-ae6e-44c6-a965-d07cc2da0aae">

  * OutputStream (Abstract Class)
 
    <img width="1134" alt="Screenshot 2024-09-12 at 4 27 36 PM" src="https://github.com/user-attachments/assets/a2061e3b-f44a-4f98-91bf-75416a380ceb">
    <img width="1117" alt="Screenshot 2024-09-12 at 4 28 30 PM" src="https://github.com/user-attachments/assets/2b77e864-71b6-4cc6-a673-093a52d03ec1">

- CharacterStream: This is for characters(unicode).

  * Reader (Abstract Class)

    <img width="1041" alt="Screenshot 2024-09-12 at 4 29 57 PM" src="https://github.com/user-attachments/assets/337be0ea-aed1-4168-8d5f-cd9fbe44f58e">
    <img width="982" alt="Screenshot 2024-09-12 at 4 30 09 PM" src="https://github.com/user-attachments/assets/72e9485f-ff38-47f9-a9f1-8e614c905a86">

  * Writer (Abstract Class)
 
    <img width="1106" alt="Screenshot 2024-09-12 at 4 30 45 PM" src="https://github.com/user-attachments/assets/0748a548-8f40-4be3-a706-027f581960e5">
    <img width="841" alt="Screenshot 2024-09-12 at 4 31 01 PM" src="https://github.com/user-attachments/assets/3a1b3056-5c3c-45bf-8d9d-2781cc71b23b">

-------------------------
### Note:
* If any class ends with Stream(example InputStream or OutputStream), we should know that it is there for handling byte data.
* If any class ends with Reader/Writer, we should know that it is there for handling character data.
* ByteStream can also work with character data (Example: PrintStream(System.out, System.err), InputStream(System.in))
-------------------------

# Predefined Streams in Java

- System.out: standard output stream is "CONSOLE"
- System.in: standard input stream is "KEYBOARD"
- System.err: standard errand stream is "CONSOLE"

These are all ByteStreams.

# Let's look at different classes available

We need to close the resources once used. Note that any class that implements "AutoCloseable" can be considered as a resource.

<img width="1118" alt="Screenshot 2024-09-12 at 4 46 14 PM" src="https://github.com/user-attachments/assets/82462dbe-6b75-4aa9-b070-cef8be67fbe6">

1. InputStreamReader: It is a bridge from byte streams to character streams.

   Example: BufferedReader br = new BufferedReader(**new InputStreamReader(System.in)**)

   <img width="971" alt="Screenshot 2024-09-12 at 4 58 21 PM" src="https://github.com/user-attachments/assets/b4cf008f-132a-4f88-bec9-5115fd8865c3">
   <img width="846" alt="Screenshot 2024-09-12 at 4 58 26 PM" src="https://github.com/user-attachments/assets/44ad628b-0739-4b0b-b1c5-e31db8d91fda">

   

   



