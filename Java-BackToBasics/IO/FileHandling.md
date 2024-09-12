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

## Reader
1. InputStreamReader: It is a bridge from byte streams to character streams.

   Example: BufferedReader br = new BufferedReader(**new InputStreamReader(System.in)**)

   <img width="971" alt="Screenshot 2024-09-12 at 4 58 21 PM" src="https://github.com/user-attachments/assets/b4cf008f-132a-4f88-bec9-5115fd8865c3">
   <img width="846" alt="Screenshot 2024-09-12 at 4 58 26 PM" src="https://github.com/user-attachments/assets/44ad628b-0739-4b0b-b1c5-e31db8d91fda">

2. FileReader:

   <img width="964" alt="Screenshot 2024-09-12 at 9 47 14 PM" src="https://github.com/user-attachments/assets/38a45b38-bd92-4280-ae58-d3170c12bc2c">

3. BufferedReader: It requires a parameter of type "**Reader**".

   <img width="997" alt="Screenshot 2024-09-12 at 9 49 46 PM" src="https://github.com/user-attachments/assets/a0f841f9-395d-4a65-84b0-f7c7b8452afd">
   <img width="803" alt="Screenshot 2024-09-12 at 9 51 06 PM" src="https://github.com/user-attachments/assets/b8e7bea9-5929-4e2c-b095-7a1a397e45fd">

## Writer
1. OutputStreamWriter: Bridge from character stream to byte stream.

   <img width="904" alt="Screenshot 2024-09-12 at 10 00 52 PM" src="https://github.com/user-attachments/assets/28133ca7-6829-400f-a540-6d45a7cec2bd">
   <img width="1041" alt="Screenshot 2024-09-12 at 10 00 57 PM" src="https://github.com/user-attachments/assets/75451eeb-3b65-43d1-a4fb-bc9fb92d1b51">

2. FileWriter:

   <img width="916" alt="Screenshot 2024-09-12 at 10 05 23 PM" src="https://github.com/user-attachments/assets/60ae65b8-37bb-445f-8c71-3d5e155befb5">
   <img width="924" alt="Screenshot 2024-09-12 at 10 05 43 PM" src="https://github.com/user-attachments/assets/2c50dc15-b2d6-4e18-86d1-3e0124d7f393">

   If we don't want to override and append instead, we can use another constructor which takes a boolean value for the appended field.

   <img width="1080" alt="Screenshot 2024-09-12 at 10 06 51 PM" src="https://github.com/user-attachments/assets/c439e715-80d8-4696-94cd-ef4640f459c9">
   <img width="918" alt="Screenshot 2024-09-12 at 10 07 57 PM" src="https://github.com/user-attachments/assets/d51a7a4e-a06d-46c2-b1d8-7c7e48aca761">

3. BufferedWriter:

   <img width="931" alt="Screenshot 2024-09-12 at 10 11 48 PM" src="https://github.com/user-attachments/assets/287da0c1-7c00-4936-bdf3-0e89f4edc577">
   <img width="797" alt="Screenshot 2024-09-12 at 10 11 52 PM" src="https://github.com/user-attachments/assets/fed9cf13-e0b1-4d34-beaf-2adb9a0c5058">


## File

- Create a new file:

  <img width="871" alt="Screenshot 2024-09-12 at 10 17 37 PM" src="https://github.com/user-attachments/assets/bab20e2f-8c18-43a6-ab6e-85a1aa98900c">

- Write to a new file:

  <img width="415" alt="Screenshot 2024-09-12 at 10 18 42 PM" src="https://github.com/user-attachments/assets/f3b61fdb-6852-4ded-822e-ee23e61e0a91">
  <img width="469" alt="Screenshot 2024-09-12 at 10 18 50 PM" src="https://github.com/user-attachments/assets/a9411879-e953-4ccc-817a-a3f8ce909d71">

- Read from the file

  <img width="942" alt="Screenshot 2024-09-12 at 10 20 04 PM" src="https://github.com/user-attachments/assets/7a4666a3-f2fc-4595-bdc8-e2a46c64706e">

- Delete a file

  <img width="422" alt="Screenshot 2024-09-12 at 10 21 12 PM" src="https://github.com/user-attachments/assets/0f17a0ac-faa4-4c11-9e1d-cef347c4ef29">
  <img width="469" alt="Screenshot 2024-09-12 at 10 21 16 PM" src="https://github.com/user-attachments/assets/b459cf3a-adec-4331-ba83-ff8ea3bb1e76">




   



