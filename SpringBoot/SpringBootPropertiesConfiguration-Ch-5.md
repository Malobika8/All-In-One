# .YAML vs .Properties

- ## .properties

  Let's start with a question.

  ### How to run an Application on port 9095?

  There are two options that we are aware of 
  - Add property while running the jar in Command line

    <img width="504" alt="Screenshot 2024-06-21 at 8 41 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bbf4fc25-8922-42b6-a624-7261affa2e7a">

  - We can go to Run Configurations in IDE and add property in arguments section

    <img width="815" alt="Screenshot 2024-06-21 at 8 41 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/685631cd-b9c4-47d6-acce-0dfc0423ec7c">

  Apart from these 2, there's another option to do the same.

  We can create a .properties file in *src/main/resources*. The name **should** be "**application.properties**". The properties gets automatically 
  picked up by SpringBoot.

  <img width="377" alt="Screenshot 2024-06-21 at 10 12 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2c4d7ca9-1d10-4ba9-b9d2-bd7ba83e2edb">
  <img width="747" alt="Screenshot 2024-06-21 at 10 12 42 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/929a1ce8-23a9-41e3-b31f-53d39ab9c0f9">
  <img width="1349" alt="Screenshot 2024-06-21 at 10 13 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4c228ce3-f4e1-4568-a18b-7b0f5549065b">

  "server.port" is a System specific key provided by SpringBoot.
  There are multiple properties key provided by SpringBoot that can be used to change the System behavior. We wouldn't even need to make any
  code changes.

  <img width="357" alt="Screenshot 2024-06-21 at 10 15 02 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4d516e98-6a56-4211-af7b-4a89a96eb9bc">
  <img width="751" alt="Screenshot 2024-06-21 at 10 16 54 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b96154ca-78b0-4f0e-a878-f759409d1451">

  We know that we can inject a value using @Value annotation.

  <img width="1164" alt="Screenshot 2024-06-21 at 10 19 12 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3c372cc9-dba6-4daa-868f-2faa769ae5ee">
  <img width="1105" alt="Screenshot 2024-06-21 at 10 21 22 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ebc59c0b-d5e7-4514-8311-c39285050ebf">
  <img width="1113" alt="Screenshot 2024-06-21 at 10 22 07 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9428067f-fb86-4b3a-b694-194d482649a4">

  ### Reading Dynamic Properties

  <img width="672" alt="Screenshot 2024-06-21 at 10 23 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c0f390c6-fad6-4aee-be95-83952354c0d4">
  <img width="855" alt="Screenshot 2024-06-21 at 10 24 03 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bdc33759-da48-4283-b770-43932dd01f92">
  <img width="836" alt="Screenshot 2024-06-21 at 10 23 55 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5cfdcacf-afc7-4c4b-8fbe-72d72f3b2864">
  <img width="1114" alt="Screenshot 2024-06-21 at 10 24 21 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6a0bbc29-1562-4118-b242-c4e070d467b1">

  ### Reading from a Random Properties File

  What if we move the properties to a different properties file than application.properties?

  <img width="319" alt="Screenshot 2024-06-21 at 10 26 43 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d44e45ee-3e08-4f2a-8b0e-b90109cbebad">
  <img width="768" alt="Screenshot 2024-06-21 at 10 26 38 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4d435b42-20eb-4148-b0d0-a1a447564da6">

  If we try to run, we'll get an error

  <img width="1071" alt="Screenshot 2024-06-21 at 10 27 13 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/18d4b820-ea2d-4032-ba15-9c1bd7387776">
  <img width="1064" alt="Screenshot 2024-06-21 at 10 27 46 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/861cb2f1-cb07-434e-b69c-e8c0bbe2ad64">

  It is to be noted that only "application.properties" file is loaded automatically. For any other properties file, we need to mention the
  property source.

  <img width="792" alt="Screenshot 2024-06-21 at 10 28 20 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ced50a47-7881-4df9-ad6e-d6224cd7f6e0">
  <img width="1066" alt="Screenshot 2024-06-21 at 10 29 12 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3106ad55-bacb-4ee3-8a1e-03d921c2327b">

  ### Is it only src/main/resources where SpringBoot looks for application.properties during startup?

  Yes. Otherwise it would throw the same error that we came across earlier.

  <img width="789" alt="Screenshot 2024-06-21 at 10 36 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3f0bf08c-95a3-4e4c-b983-f82b6fcc7f54">

  **But there's a catch.** SpringBoot detects the application.properties file if it's placed in "*config*" folder.

  <img width="327" alt="Screenshot 2024-06-21 at 10 37 57 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/01443ee1-c156-46ae-8702-13d09388840b">
  <img width="794" alt="Screenshot 2024-06-21 at 10 38 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9253efdd-145b-4a09-a197-4e6bcdb41617">
  <img width="1148" alt="Screenshot 2024-06-21 at 10 39 38 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3200bdcd-6caf-4747-9983-c882def4d70f">

  If we go to target folder and unzip the Jar, we'll see the application.properties file is there in BOOT-INF folder

  <img width="651" alt="Screenshot 2024-06-21 at 10 41 31 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/81fed101-773d-4602-9c86-eab3d605fe14">
  <img width="648" alt="Screenshot 2024-06-21 at 10 41 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/17d1ff63-eaa3-4f5f-96a1-3429b68d45ee">
  <img width="646" alt="Screenshot 2024-06-21 at 10 43 02 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/02ada3ec-36af-4cc2-ac49-6bd95461e61b">
  <img width="1145" alt="Screenshot 2024-06-21 at 10 44 15 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cdbce41a-0931-435b-a0e0-cdefdf68b810">

  ### Note:
  Spring also looks from application.properties file outside of our jar / classpath(src/main) if it is inside a **config** folder.

  <img width="326" alt="Screenshot 2024-06-21 at 10 44 52 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b50ace7c-9192-4dd3-9179-90166bfde2aa">
  <img width="305" alt="Screenshot 2024-06-21 at 10 45 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ef6be50a-f72e-465b-9398-3ef3e0364f3b">
  <img width="794" alt="Screenshot 2024-06-21 at 10 45 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2d6dc662-2f7f-4b68-b537-b962282d4616">

  Moreover, application.properties file will be detected if it is simply inside the project. 

  <img width="316" alt="Screenshot 2024-06-21 at 10 48 39 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/be1953c1-e8fd-4ceb-932d-2f0ec60b465c">
  <img width="792" alt="Screenshot 2024-06-21 at 10 48 57 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/720535cc-d9e0-4192-8e68-7be79718d887">

  But in both of these cases, it won't be a part of the Jar file. There won't be any properties file present in BOOT-INT folder.

  <img width="655" alt="Screenshot 2024-06-21 at 10 51 34 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9606ecdb-79a1-417e-bd5b-bff4f5e0aaa2">
  <img width="652" alt="Screenshot 2024-06-21 at 10 51 44 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1ca89bfd-d5dc-4560-bdbe-503352317250">
  <img width="658" alt="Screenshot 2024-06-21 at 10 51 53 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/be6305dd-170e-4bd8-add7-58512351abe1">

  **This basically mean if we launch the app from IDE, it will work fine. However, if we try to directly launch the app from Jar, it won't work.**

  <img width="1141" alt="Screenshot 2024-06-21 at 10 55 23 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ffcf1716-f831-4011-8c2e-cc781c0f538b">

  In that case, we would need to specify location of the properties file.

  <img width="875" alt="Screenshot 2024-06-21 at 10 56 54 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f168b76a-4c9c-4617-88f9-c9857efa5fb3">
  <img width="1142" alt="Screenshot 2024-06-21 at 10 56 43 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/00990a10-b1b3-431c-91a2-5d9c01e8d813">
  <img width="1149" alt="Screenshot 2024-06-21 at 10 58 10 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/af9537b0-d484-4e67-9b33-f778eaa69174">

- ## .yaml

  Like application.properties we can also write a *application.yaml* file to configure our SpringBoot app.

  <img width="897" alt="Screenshot 2024-06-21 at 10 59 52 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7658570d-8ba4-466d-bbc4-0a386d768d29">
  <img width="1225" alt="Screenshot 2024-06-21 at 10 59 58 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/30053eb7-ae39-4ec6-800d-4675adb07580">

  <img width="259" alt="Screenshot 2024-06-21 at 11 00 49 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e356791a-3904-4c26-85a3-ceb70bcdb12d">
  <img width="715" alt="Screenshot 2024-06-21 at 11 00 57 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a3164990-166c-4abb-a199-036c7124ce7b">
  <img width="859" alt="Screenshot 2024-06-21 at 11 01 30 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ec62b331-7db4-42d6-ad52-9cbec9d4116c">

## YML Vs Properties.. Which one to choose?

We can choose any of the two. There's no performance benefit.

<img width="625" alt="Screenshot 2024-06-21 at 11 05 12 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2b03f5b0-4bc1-4d9d-8cc4-cacc2a54f580">
<img width="1043" alt="Screenshot 2024-06-21 at 11 06 21 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/aa144304-e28b-496c-8695-a33233c38a0a">







