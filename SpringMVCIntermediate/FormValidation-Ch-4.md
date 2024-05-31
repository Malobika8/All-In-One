<img width="830" alt="Screenshot 2024-05-31 at 12 33 08 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8916718d-28c5-4761-8aa3-5d85bae21dfa">

We shouldn't completely rely on client-side valdation as it is possible to  break things by modifying or even disabling javascript.

<img width="1091" alt="Screenshot 2024-05-31 at 12 54 54 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5ea97daf-65a6-4b59-ad96-f76b2a07cc98">

<img width="1013" alt="Screenshot 2024-05-31 at 12 57 28 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e25b0281-131b-407f-b4b5-6cd3bb35d80b">

JSR is Java Specification Request. Suppose we find some gaps in Java & there's a need for improvement, in that case, we can file a JSR. We can
convert our ideas and thoughts to a specification(JSR). Once filed, it is reviewed by a community called JCP(Java Community Process). JSR can be 
filed by JCP members. It then reached PMO which is another organisation managed by Oracle. So JCP is the team/community that continuously 
works for the betterment/improvement of Java Programming languages.
There's total 927 JSR's available and for Bean validation, there are 3(JSR 303, JSR349, JSR380).

<img width="1144" alt="Screenshot 2024-05-31 at 1 06 22 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/11193667-875f-4f7b-8d23-a017d6980125">

*Note:* These are backward compatible.

JSR's are specifications(interfaces). There are companies that provide implementation to those JSR's.

<img width="1018" alt="Screenshot 2024-05-31 at 1 09 02 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/24e80c17-18b4-4677-9c8a-27c497cb871f">
 
We'll be using

<img width="568" alt="Screenshot 2024-05-31 at 1 09 17 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6beeb927-6140-4190-a364-7f3445ad3811">

* Server Side Validation:

  - Add validation-api maven dependency(search for jsr 380)

    <!-- https://mvnrepository.com/artifact/jakarta.validation/jakarta.validation-api -->
        <dependency>
            <groupId>jakarta.validation</groupId>
            <artifactId>jakarta.validation-api</artifactId>
            <version>3.1.0</version>
        </dependency>
    Add validation implementation dependency

    <!-- https://mvnrepository.com/artifact/org.hibernate.validator/hibernate-validator -->
        <dependency>
          <groupId>org.hibernate.validator</groupId>
          <artifactId>hibernate-validator</artifactId>
          <version>8.0.1.Final</version>
        </dependency>

  - Consider the below page. Name and Username shouldn't be left blank.

    <img width="1138" alt="Screenshot 2024-05-31 at 1 31 42 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e56b8e6d-9858-44f7-a5b2-500138f06232">

    In order to validate, we can make use of validation-api. 

    <img width="987" alt="Screenshot 2024-05-31 at 1 35 39 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a71e9bb6-6d12-43b4-b3a3-0b6ae35f34c2">

    To trigger our validation once DataBinding is done, we can use @Valid(it should be there before @ModelAttribute). It triggers the bean for
    validation.

    <img width="966" alt="Screenshot 2024-05-31 at 1 38 33 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a3848731-c390-4842-970a-b99fc0569323">

    The validation result will be stored in BindingResult(It should come after the DTO). If we keep the fields black, it will stay at the home
    page.

    <img width="878" alt="Screenshot 2024-05-31 at 1 40 58 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b91e55e0-b7d0-4212-a7d5-ddfc2b233223">
    <img width="989" alt="Screenshot 2024-05-31 at 1 57 12 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9b081ca2-78e1-4128-a46a-da906c5dc120">
    <img width="1327" alt="Screenshot 2024-05-31 at 1 57 42 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9bb5f1fc-a50f-4a67-9c5a-23650f34fd74">
    <img width="1183" alt="Screenshot 2024-05-31 at 1 57 52 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9b0027c2-e2f2-44dc-bea6-ff53316772ce">
    <img width="1040" alt="Screenshot 2024-05-31 at 1 56 04 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e3699fd8-fa09-4db7-b7db-d1324869fa57">

    We can also display the error.

    <img width="936" alt="Screenshot 2024-05-31 at 2 00 11 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e629c94c-7939-4d3f-bc4f-d5cf941a80f5">
    <img width="1015" alt="Screenshot 2024-05-31 at 2 02 24 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/754c6de4-556a-45ba-940e-a64f1f5e03e4">
    <img width="1016" alt="Screenshot 2024-05-31 at 2 02 43 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8f6094f2-98af-4461-bece-c198ee4ce679">
    <img width="736" alt="Screenshot 2024-05-31 at 2 03 52 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a3ce1f87-42eb-4863-bb83-3b556a83c4d7">
    <img width="1038" alt="Screenshot 2024-05-31 at 2 04 01 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9c04aff8-1d20-497f-a638-b23fe603f9dc">

    We can display it properly by making few changes.

    

    
