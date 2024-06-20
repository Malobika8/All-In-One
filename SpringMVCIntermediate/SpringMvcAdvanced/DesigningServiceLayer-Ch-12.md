# Sending an email

<img width="1148" alt="Screenshot 2024-06-20 at 7 24 07 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ebfbeccb-d4b6-434f-81f0-5cf6e6624006">
<img width="734" alt="Screenshot 2024-06-20 at 7 24 23 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3a01d519-c7d0-426f-bb89-345f88b12e29">
<img width="1021" alt="Screenshot 2024-06-20 at 7 24 32 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/445decb7-7c55-49aa-9e0e-0c083e6849ea">

----------------------------------------------------------------------------------------------------------------------------------------
# To construct an email

<img width="1147" alt="Screenshot 2024-06-20 at 7 25 45 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4024817d-989f-4ab2-83ce-c4fb5e65281d">
<img width="625" alt="Screenshot 2024-06-20 at 7 26 28 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ea15adb4-6967-47c4-b2e5-b2684d2a3b2d">

----------------------------------------------------------------------------------------------------------------------------------------
# Let's implement Spring mail API

- Add these 3 dependencies:

  <!-- https://mvnrepository.com/artifact/jakarta.mail/jakarta.mail-api -->
        <dependency>
            <groupId>jakarta.mail</groupId>
            <artifactId>jakarta.mail-api</artifactId>
            <version>2.1.3</version>
        </dependency>
  
  Jakarta mail implementation

  <!-- https://mvnrepository.com/artifact/org.eclipse.angus/jakarta.mail -->
      <dependency>
          <groupId>org.eclipse.angus</groupId>
          <artifactId>jakarta.mail</artifactId>
          <version>2.0.3</version>
      </dependency>
  <!-- https://mvnrepository.com/artifact/org.springframework/spring-context-support -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context-support</artifactId>
            <version>6.1.8</version>
        </dependency>

- We need to create a Bean (This will establish a connection with gmail with all properties set)

  <img width="1045" alt="Screenshot 2024-06-20 at 7 42 15 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/590f73ae-1821-44b7-91ba-623694943c9f">

- We need to add two properties: dls and ssl
  
  <img width="596" alt="Screenshot 2024-06-20 at 7 42 29 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/de0336f0-55ac-4e8e-8c5c-d3f161cdabe0">

- If we want to configure gmail with our application, we need to turn on the less secure app feature inside the gmail app.

  <img width="1043" alt="Screenshot 2024-06-20 at 7 40 31 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/78ef667e-35e5-4460-8cdc-be6652d99fe0">
  <img width="694" alt="Screenshot 2024-06-20 at 7 51 54 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/623516eb-e1f5-4323-9726-abd0c3a0c7be">

- Create a method to send email

  <img width="804" alt="Screenshot 2024-06-20 at 7 55 59 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/82d4208c-5e5d-41d0-941c-d70375c8c6fc">
  <img width="1228" alt="Screenshot 2024-06-20 at 7 57 16 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d7377430-20db-4c55-937d-4fc1be936e04">
  <img width="1088" alt="Screenshot 2024-06-20 at 8 01 15 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c1bcb7ff-e8f7-4495-ab86-2a7819e0c2a9">
  <img width="1188" alt="Screenshot 2024-06-20 at 8 01 28 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2ff90b8b-d1da-46b8-91d0-296eeca0c1ba">
  <img width="1028" alt="Screenshot 2024-06-20 at 8 03 28 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7036ed3d-719b-4217-b171-2e0dfd92e08f">
  <img width="758" alt="Screenshot 2024-06-20 at 8 03 50 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0a53352a-d2fe-4070-9869-7244725aabc4">
  <img width="1155" alt="Screenshot 2024-06-20 at 8 04 17 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/74a8b7ac-2d44-47d3-aac8-56f9940745db">
  <img width="1193" alt="Screenshot 2024-06-20 at 8 04 26 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f1875064-973b-4082-8e8d-39af8fde3410">
  <img width="1130" alt="Screenshot 2024-06-20 at 8 05 01 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/73660931-2a65-4ace-a353-b3be87845263">
  <img width="1056" alt="Screenshot 2024-06-20 at 8 05 57 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6913fc9f-774e-4bfd-8208-091adf0d2a90">
  <img width="802" alt="Screenshot 2024-06-20 at 8 07 23 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/98855450-967b-49c6-9254-af711e7e2bcc">

- Create an Interface

  <img width="818" alt="Screenshot 2024-06-20 at 8 16 51 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/596bad3b-d404-4e9b-944f-54632ed147af">

- Create Impl. @Service is same as @Component. It is basically extending @Component and is used to differentiate a service class.

  <img width="1059" alt="Screenshot 2024-06-20 at 8 23 38 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a0a19755-779a-4cb2-bdbe-422967f8e3bb">

- Call the Service from Controller

  <img width="1032" alt="Screenshot 2024-06-20 at 8 17 15 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/103b2be5-3233-4f4b-9af8-80ea5a19d63e">

- Run the Application
  
  <img width="611" alt="Screenshot 2024-06-20 at 8 35 02 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/88e11e0b-7bb0-4462-8541-68bdbfe13731">
  <img width="661" alt="Screenshot 2024-06-20 at 8 35 27 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/836d798e-dab9-47e2-8da3-73203255a9e9">

  <img width="724" alt="Screenshot 2024-06-20 at 8 37 06 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/eef7403d-6fbc-4f9d-ba84-61e1e49396ae">
  <img width="524" alt="Screenshot 2024-06-20 at 8 37 20 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5875d402-bdee-4ca2-b05c-39efb4505c1e">

## Note: *We have used SimpleMailMessage class to send emails*

<img width="1074" alt="Screenshot 2024-06-20 at 11 43 17 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/20cef457-4cf2-4e75-a01e-9c09d69a8328">

----------------------------------------------------------------------------------------------------------------------------------------
# Best Practices

* Rather than hardcoding properties, we can load it from a properties file

  <img width="620" alt="Screenshot 2024-06-20 at 8 42 34 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a4d7e87f-5f8a-4af8-8400-69bc109a873e">
  <img width="472" alt="Screenshot 2024-06-20 at 8 42 45 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/35b7130d-538f-4a20-be0f-6dd1079e751b">
  <img width="839" alt="Screenshot 2024-06-20 at 8 44 25 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/178b7ed5-d0c2-4b0b-9c9e-aef5802d0906">

  To load properties from a properties file, we can use a class called Environment

  <img width="826" alt="Screenshot 2024-06-20 at 8 46 43 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/73682f96-7a4c-43aa-a0f2-b586e8aa6c42">

  We need to mention the location of the properties file. This can be done using @PropertySource annotation. We can use         
  *environment.getProperty* method

  <img width="696" alt="Screenshot 2024-06-20 at 8 51 35 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c57c2d93-2889-4fa7-bcbd-b96edb3ae8a1">
  <img width="766" alt="Screenshot 2024-06-20 at 8 51 55 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/41c4eb49-6c62-46e6-a76c-9029cf40a033">

  <img width="953" alt="Screenshot 2024-06-20 at 9 36 41 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4b6575b0-f61a-449d-97e5-ac1130116253">
  <img width="746" alt="Screenshot 2024-06-20 at 9 37 05 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/158a1b9d-59da-4c9c-95e7-11c221fc0542">

  OR

  <img width="750" alt="Screenshot 2024-06-20 at 9 37 49 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7c40ca7e-ca8c-48d1-9259-4d43fb143ab0">

* Create Utility/Helper methods which could be reusable
* Writting readable code. It's not advisable to dump all our code inside a single method
* Use Logger (No more System.out.println)

  <img width="905" alt="Screenshot 2024-06-20 at 9 34 07 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/439f24fa-69d1-494e-900f-7cfd30f1f144">

  Fetching**

  <img width="775" alt="Screenshot 2024-06-20 at 9 34 43 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6382514e-360a-45e2-9bf8-9c2451f9df19">

* Handle Exception

  <img width="762" alt="Screenshot 2024-06-20 at 9 44 21 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1121654c-83fd-485a-9223-887822f38357">

* We shouldn't send complete dto object but only what is required

# Let's write a Service for Calculator result

<img width="786" alt="Screenshot 2024-06-20 at 11 08 57 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3cf5b06a-355c-4094-9987-7203278b3077">
<img width="908" alt="Screenshot 2024-06-20 at 11 09 08 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/70c72a5b-dd81-4455-beac-dd8537991c81">
<img width="1009" alt="Screenshot 2024-06-20 at 11 09 14 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2f613e26-3de7-4785-80f2-b828e78a5a7b">
<img width="1071" alt="Screenshot 2024-06-20 at 11 09 43 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/beff30b1-c915-4c3b-9beb-21ef393c552f">
<img width="981" alt="Screenshot 2024-06-20 at 11 12 48 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b60f1d45-f587-4d01-b35e-3b5bfe90ce7b">
<img width="681" alt="Screenshot 2024-06-20 at 11 15 02 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/839d1cb4-da58-47ae-ab6f-c676c334890b">

*Note: How to handle form validation manually without ModelAttribute?*

<img width="755" alt="Screenshot 2024-06-20 at 11 40 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3d5c7ce2-5ec0-451b-ad91-ee7e89ed930a">

----------------------------------------------------------------------------------------------------------------------------------------
# Extra:

What if the user blocks Cookies? - We have used SessionAttributes

<img width="1143" alt="Screenshot 2024-06-20 at 11 51 30 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3d006520-77ad-49b7-b366-90371406606f">
<img width="736" alt="Screenshot 2024-06-20 at 11 44 49 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/355dbbfb-0ad9-4f24-920c-cb20234ebef7">
<img width="676" alt="Screenshot 2024-06-20 at 11 45 59 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/dd6059e7-21df-4861-be20-ee0ca9aafcdb">
<img width="1088" alt="Screenshot 2024-06-20 at 11 46 13 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e92dfeaa-f597-4d32-84c5-08126d9d40a6">
<img width="723" alt="Screenshot 2024-06-20 at 11 46 52 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/da412685-9ee1-4f46-b769-2f705fbf754f">
<img width="562" alt="Screenshot 2024-06-20 at 11 47 12 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6120b883-29d9-4dc7-835b-8e8a89896928">
<img width="680" alt="Screenshot 2024-06-20 at 11 47 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1e46da09-eeef-4a84-8c5d-98b746c76477">

There are 2 approaches:
- Approach 1

  <img width="800" alt="Screenshot 2024-06-20 at 11 48 36 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/69821f99-6bb4-4589-85a0-4d203905ed03">

- Approach 2: Encode URL (URL re-writting). We can use JSTL url. This does URL encoding and adds JSESSIONID in the URL

  <img width="1003" alt="Screenshot 2024-06-20 at 11 54 00 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7c9a5072-b709-4f85-9e7c-213c68249b78">
  <img width="440" alt="Screenshot 2024-06-20 at 11 54 51 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/262246b2-9296-400f-bfce-447ca12706ca">
  <img width="808" alt="Screenshot 2024-06-20 at 11 54 55 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d9a8020a-41ba-4aff-882b-fea8fbc95029">
  <img width="425" alt="Screenshot 2024-06-20 at 11 54 59 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/de3189ff-a274-47d7-aa34-dfbbb81ee0e7">

  JSESSIONID added to url
  
  <img width="727" alt="Screenshot 2024-06-20 at 11 55 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ffc99c6b-bb6c-4947-9dc0-79ff27a5fd0e">

  There's no Cookies in the Cookies session as they are blocked

  <img width="1143" alt="Screenshot 2024-06-20 at 11 55 21 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2d75a3f8-c266-4595-b731-2596a6460f5a">

  *Note: Only when the Cookies are blocked the JSESSIONID is appended to url*

  <img width="1144" alt="Screenshot 2024-06-20 at 11 58 50 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c9b0c905-5903-4aa5-891e-5e0da74a2345">
  <img width="1030" alt="Screenshot 2024-06-20 at 11 59 20 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3621e6f1-a9f6-4068-9b45-b557e8a58877">
  <img width="460" alt="Screenshot 2024-06-20 at 11 59 14 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7974d2d1-0976-4233-9885-2d48e4639115">


  
  
