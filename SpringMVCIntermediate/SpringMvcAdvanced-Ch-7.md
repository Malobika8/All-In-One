# **Init Binder**

*Flow of Control:* InitBinder->Handler Method
We can do a lot of pre-work or even control data binding.
For eg, Suppose we don't want to bind Name during Registration. We can disallow binding the field with the help of WebDataBinder.

* Allowed Data Binding for name field:

  <img width="978" alt="Screenshot 2024-06-04 at 7 36 04 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f0692075-260f-40ff-8619-af9d7dd1ab17">
  <img width="783" alt="Screenshot 2024-06-04 at 7 36 27 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/4010a8b4-b520-4013-b499-d75920f80b83">

* Data Binding for name field not allowed:

  - Check the property name

    <img width="901" alt="Screenshot 2024-06-04 at 7 34 40 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c376ff06-36c0-4b9d-933d-ae35de27d356">

  - Disallow DataBinding for name field using **WebDataBinder**

    <img width="962" alt="Screenshot 2024-06-04 at 7 39 05 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/65c7eb37-7310-4711-97fc-f675fb5c139a">

  - Run application and enter details during registration

    <img width="978" alt="Screenshot 2024-06-04 at 7 36 04 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d09b6def-10b4-4f81-8573-bc639dcc076f">
    <img width="703" alt="Screenshot 2024-06-04 at 7 37 26 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d7f7028a-983f-4532-b889-1b9d6c119d66">

There are whole lot of things that can be done with InitBinder.

# **Intro to Property Editor**

Suppose we want to validate a field like name. The app shouldn't allow registration if name is not provided. We can validate the same using 
Annotation(validation-api).

<img width="1074" alt="Screenshot 2024-06-04 at 7 43 07 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1b5152f5-6a4f-48b2-aff5-67a4be6ec6bb">

<img width="979" alt="Screenshot 2024-06-04 at 8 49 01 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9609295e-e0de-4df5-b157-e4b461b506ed">
<img width="945" alt="Screenshot 2024-06-04 at 8 51 06 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f5c09f2c-2fe6-4aeb-a165-21d2c797c4a5">

However, the user can trick the application by providing spaces. @NotEmpty annotation doesn't check for spaces. The application would
allow the user to register.
Entered spaces.

<img width="996" alt="Screenshot 2024-06-04 at 7 49 00 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ddbc564c-814f-456d-8b4e-4bac6de0a369">
<img width="904" alt="Screenshot 2024-06-04 at 8 52 36 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/75d00cfc-a6b3-4a17-a6f2-cf4acb2faa2e">
<img width="890" alt="Screenshot 2024-06-04 at 8 54 29 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1689d38c-47c1-459e-bcd2-3c6a00ac3132">

In such cases, we can make use of Property editor to trim the spaces.

- Create an object of StringTrimmerEditor and pass it while registering the same using webDataBinder. It required field type, field name and
  editor object.
  While creating editor object
  * True: Trims the String and converts to null

    <img width="943" alt="Screenshot 2024-06-04 at 7 54 02 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b6e2f637-9637-4722-95e5-17d0de17bb64">
    <img width="920" alt="Screenshot 2024-06-04 at 7 53 03 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/dff56ce1-46e2-403f-a567-1b8523609e91">

  * False: Trims the String(but doesn't convert to null)
 
    <img width="1083" alt="Screenshot 2024-06-04 at 7 55 40 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e651518e-c75b-46b3-bc19-e5a828bc9452">

  StringTrimmerEditor:
  
  <img width="1089" alt="Screenshot 2024-06-04 at 7 51 29 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d3373926-374c-4bb4-a0a3-00e7b6e5d4fb">
  <img width="1020" alt="Screenshot 2024-06-04 at 8 56 40 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ae40ff8a-b7be-4be2-b10f-d014d60817a1">

  Added spaces in name but it didn't allow to proceed this time.
  
  <img width="764" alt="Screenshot 2024-06-04 at 9 04 29 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f56fd45c-2dd2-4087-9ac7-076aebd3de67">
  
  We can see the error that the name provided is null(Since "true" is passed with StringTrimmerEditor, the String is trimmed and converted to
  Null).
  
  <img width="1332" alt="Screenshot 2024-06-04 at 9 04 50 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/db556788-4dd0-4dfd-84f2-ad401f8a4690">

**PropertyEditor**

<img width="991" alt="Screenshot 2024-06-04 at 8 46 02 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d61a7f16-6877-493d-be1e-044f3cb00fc8">

Default Editors

<img width="1134" alt="Screenshot 2024-06-04 at 9 10 11 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b8b6f181-e11a-4cb3-8521-cc2b3c73ad3c">
<img width="1119" alt="Screenshot 2024-06-04 at 9 10 29 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8968ed18-1a45-473e-8b57-987189e9b01d">

Custome Editors

<img width="1140" alt="Screenshot 2024-06-04 at 9 12 00 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1447efd9-28aa-4f04-986c-71aa1342f51c">

Property Editors help us to convert one DataType to another. All different Editors extend PropertyEditorSupport.

<img width="1137" alt="Screenshot 2024-06-04 at 9 13 45 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/90fdca20-4ca7-4e86-8cf3-7191502f962b">
<img width="1142" alt="Screenshot 2024-06-04 at 9 16 08 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e6b40ed6-c615-4a9d-b0a2-e90f086ce0ad">
<img width="1143" alt="Screenshot 2024-06-04 at 9 17 25 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c686db4c-d824-4983-a9bc-696480bd579e">

WebDataBinder Instantiation

<img width="1154" alt="Screenshot 2024-06-04 at 9 17 37 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5fb80e0f-f4ba-4720-a380-457cce2b3373">
<img width="1136" alt="Screenshot 2024-06-04 at 9 27 00 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c990a5b4-709a-422e-8f40-b4dae1f95dc3">
<img width="1133" alt="Screenshot 2024-06-04 at 9 28 44 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/32c74739-9431-4394-b95d-d37d6e76b45d">
<img width="1014" alt="Screenshot 2024-06-04 at 9 29 22 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/86b8f6be-4ff5-44cd-af2f-117a045409fd">
<img width="1150" alt="Screenshot 2024-06-04 at 9 30 22 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fa612e4c-aa0f-4358-b224-422f6c34676e">

Consider a Bill page where we accept Credit Card, Amount, Currency, Date to pay.

<img width="761" alt="Screenshot 2024-06-04 at 10 54 31 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b91c829a-792d-4a04-b0f7-581a60a4a4ab">
<img width="790" alt="Screenshot 2024-06-04 at 10 54 39 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8ddfd733-f970-4f30-b18e-a78d4994c303">
<img width="757" alt="Screenshot 2024-06-04 at 10 55 07 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2f8a9b06-e8d3-4169-a11e-dc3fc12cb0ba">
<img width="766" alt="Screenshot 2024-06-04 at 10 55 18 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/72cc0e16-0348-4d14-b94a-aca7ed8019e4">
<img width="645" alt="Screenshot 2024-06-04 at 10 55 46 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c65f015c-3e05-438a-85e2-4d9b63c18bc4">

- CustomDateEditor: When we try to add a Date in the format dd-mm-yyyy, it doesn't work. We can make use of CustomDateEditor to make it work.

  <img width="1088" alt="Screenshot 2024-06-04 at 10 57 21 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a0f332c2-9ca7-463f-85c1-d64fbc2e3de9">
  <img width="1090" alt="Screenshot 2024-06-04 at 10 59 55 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a1d3f43c-5bfc-45dc-b11b-ea13977e79fa">
  <img width="1117" alt="Screenshot 2024-06-04 at 11 01 06 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/663879a2-8392-4045-a301-f4bba3b2a86b">
  <img width="1009" alt="Screenshot 2024-06-04 at 11 01 12 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8cd1f301-0e0b-404a-8883-7a17347907e9">

- CustomNumberEditor: We want to add amount in the format ##,###.00. This can be customized using CustomNumberEditor.

  <img width="978" alt="Screenshot 2024-06-04 at 11 01 49 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/de581f48-210e-48a6-a042-ad962c6f09d1">
  <img width="1085" alt="Screenshot 2024-06-04 at 11 03 18 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6104182b-1176-481e-acf4-fb9d25801c75">
  <img width="1087" alt="Screenshot 2024-06-04 at 11 06 27 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ccdd4e44-1cfb-4ffe-8a97-c44485527b02">
  <img width="1101" alt="Screenshot 2024-06-04 at 11 06 48 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fd3da70e-f506-4b29-b8ca-06bc979b1592">
  <img width="853" alt="Screenshot 2024-06-04 at 11 06 56 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b653b6ab-4e83-4f31-8518-93f550fc4937">

## CustomPropertyEditor

<img width="1014" alt="Screenshot 2024-06-04 at 11 07 39 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/51271113-e6b5-4c9c-a4af-b31f50b70b19">
<img width="937" alt="Screenshot 2024-06-04 at 11 08 19 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9e518f92-232e-4512-8567-b7cb83fb97ba">

To create our own PropertyEditor, we need to extend PropertyEditorSupport.
  
