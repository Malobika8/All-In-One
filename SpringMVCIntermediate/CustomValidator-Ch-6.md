# Bean Validation API Advance
<img width="1141" alt="Screenshot 2024-06-03 at 7 38 02 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3f3c3d29-2a1b-492c-9b0f-267282aece89">
<img width="1137" alt="Screenshot 2024-06-03 at 7 39 05 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c8d7518d-637c-4b16-b117-72a735214a86">

# **Custom Validator**

<img width="1042" alt="Screenshot 2024-06-03 at 7 41 59 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/82eb119a-6c41-42a8-93f5-66d3b59be0ca">
<img width="1096" alt="Screenshot 2024-06-03 at 7 43 20 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/613c4b59-26fa-4ae1-b767-02a4cda813c7">
<img width="1253" alt="Screenshot 2024-06-03 at 7 44 27 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3798ea36-3b00-4e7a-bd43-acda33014315">
<img width="1172" alt="Screenshot 2024-06-03 at 7 45 06 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/4924f33c-f501-489d-8cce-f65c65910a88">
<img width="1247" alt="Screenshot 2024-06-03 at 7 46 05 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/4d170f5f-bd34-4f8f-b48e-66dc190fb2bc">
<img width="1226" alt="Screenshot 2024-06-03 at 7 46 41 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3a23ccf3-a7a0-4082-a046-47a28531cf88">
<img width="1045" alt="Screenshot 2024-06-03 at 7 47 24 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cb0646d6-1d95-48fb-b339-24d72f43235b">
<img width="1211" alt="Screenshot 2024-06-03 at 7 48 04 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f49e9566-d242-4879-a317-7512b4757b07">
<img width="1232" alt="Screenshot 2024-06-03 at 7 48 38 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c91bad4f-6c91-44df-82d9-52a8243aa14d">
<img width="1209" alt="Screenshot 2024-06-03 at 7 50 06 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e79b065b-f9cc-4721-8f8f-0995434a4fab">
<img width="1274" alt="Screenshot 2024-06-03 at 7 51 05 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b22b4a98-be4a-4dfd-b980-caabaf096875">
<img width="1237" alt="Screenshot 2024-06-03 at 7 52 37 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8adb12ce-4cff-4ff8-948b-1b520a145bb4">
<img width="1241" alt="Screenshot 2024-06-03 at 7 53 06 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a9ccaa86-c8cc-4a10-8d52-c0787bb24e12">
<img width="1214" alt="Screenshot 2024-06-03 at 7 53 24 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/27f655c0-b2ac-4079-b91f-206e29215e60">
<img width="1024" alt="Screenshot 2024-06-03 at 7 53 34 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9ceec0bb-087e-4647-9ee5-3a2a9a949e69">
<img width="1262" alt="Screenshot 2024-06-03 at 7 54 14 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c08a1bff-0018-4029-af9f-9ba0ba9c0fbe">
<img width="610" alt="Screenshot 2024-06-03 at 7 54 46 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/7eb03cc4-f78b-428a-965d-ca44d739e792">
<img width="471" alt="Screenshot 2024-06-03 at 7 55 18 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c07ec1d7-8ec4-4c26-a618-34b009137d6c">
<img width="665" alt="Screenshot 2024-06-03 at 7 55 47 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0c6868e7-9688-47d4-ad7c-9690da4a6c79">
<img width="1241" alt="Screenshot 2024-06-03 at 7 56 26 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c68b4151-eec4-4dd4-8384-f250babb7292">
<img width="1258" alt="Screenshot 2024-06-03 at 7 56 57 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d564abf1-c8b8-4e70-95de-0aa2aac459c6">

Lets analyse existing annotations.

<img width="787" alt="Screenshot 2024-06-03 at 8 09 26 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e17ac0fd-6b76-4181-944e-c46c3db42f20">

For pre-existing annotations, the way validator classes are located is different than custom annotations.

<img width="1144" alt="Screenshot 2024-06-03 at 8 11 07 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a0b01679-eb9e-49f7-84a0-7a07dc34270e">

How to know which validator class is implemented for which annotation?

<img width="1062" alt="Screenshot 2024-06-03 at 8 14 29 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8e7d76e0-dc60-4cdf-ad91-267550761ca3">

There's a class called Constraint helper which helps locate the validator class.

<img width="816" alt="Screenshot 2024-06-03 at 8 15 27 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/679194b5-a387-466f-b17d-de77ff0297c9">

Default message through preperties file

<img width="1092" alt="Screenshot 2024-06-03 at 8 23 29 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5154dd75-859a-4c01-add3-59bb26111f69">
<img width="1065" alt="Screenshot 2024-06-03 at 8 20 58 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/23abe363-a06d-48be-9d81-6e6ca6a0ce36">

We need to have groups and payload for any annotations we want to have

<img width="847" alt="Screenshot 2024-06-03 at 8 26 34 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/67d740f7-956a-4a14-870a-2e5da7af6592">

##Let's write a Validator for "age" field.

Create an annotation called Age

<img width="995" alt="Screenshot 2024-06-03 at 9 12 05 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/92907c64-6f90-48b0-a738-0bc39e75c3e5">

Always add groups and payload in any annotation classes.

    Class<?>[] groups() default {};
    Class<? extends Payload>[] payload() default {};
    
Create AgeValidator class which will have the logic. The Validator class should implement ConstraintValidator"(Annotation),(fieldType)".

<img width="868" alt="Screenshot 2024-06-03 at 8 40 09 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/26306108-2e07-42ae-b9c3-d807dbf0d357">
<img width="1001" alt="Screenshot 2024-06-03 at 9 26 16 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a3e08436-98cc-4750-aaad-5849bb8ae695">

We can override lower,upper and message.

<img width="908" alt="Screenshot 2024-06-03 at 9 16 57 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3905e586-2bee-4e83-a170-81746388df49">

Add necessary changes in Controller

<img width="1026" alt="Screenshot 2024-06-03 at 9 17 58 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/45b695ba-577b-46db-85fa-8a6eb814e871">

Run the Application,

<img width="1310" alt="Screenshot 2024-06-03 at 9 19 17 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9972bdfc-bd58-4944-a587-b041b49b3ed6">

Left blank

<img width="1182" alt="Screenshot 2024-06-03 at 9 19 24 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/47cd93f8-8cf6-419c-8b3d-a30156b6bff3">

Less than 30

<img width="1141" alt="Screenshot 2024-06-03 at 9 19 37 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c6841c70-0382-4139-8b05-37387d25f868">

Age between 30-75

<img width="1084" alt="Screenshot 2024-06-03 at 9 19 48 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5b8cf457-7469-4ef0-8ea1-4ddb518b9112">
<img width="894" alt="Screenshot 2024-06-03 at 9 19 54 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/100f76ce-26b3-40e0-8017-f749de2d943f">

##Adding a Properties file

Default message shouldn't be hardcoded

<img width="865" alt="Screenshot 2024-06-03 at 9 31 17 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/05f6a7ef-d7e8-4f0e-bda6-ea39b8893e9d">

Its better to avoid harcoding messages.

<img width="998" alt="Screenshot 2024-06-03 at 9 35 47 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8b092b0b-98cc-4cf9-bc69-02754134377e">
<img width="1140" alt="Screenshot 2024-06-03 at 9 35 56 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fcf2d58f-73db-46c5-a116-5918c1ca9693">
<img width="1143" alt="Screenshot 2024-06-03 at 9 36 06 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1eb08751-c8bf-4b13-9fc1-77b417715a30">

Create a properties file

<img width="1268" alt="Screenshot 2024-06-03 at 9 40 05 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/478d6f9e-13b1-4341-99ec-a642da7b144a">

Add the property name

<img width="1031" alt="Screenshot 2024-06-03 at 9 40 57 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8666352a-5166-41da-a2c5-84b039dca7f4">

Create a bean which will locate and load the properties file. (messages is the properties file name)

<img width="1040" alt="Screenshot 2024-06-03 at 10 00 46 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cf29a41e-1fd7-4262-9595-4839b4132938">

Tell Spring to look for above messagesource.

<img width="1017" alt="Screenshot 2024-06-03 at 10 00 17 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/764d0083-4b17-424f-821d-600d9400c6cb">

Run the application. It should work as expected.
