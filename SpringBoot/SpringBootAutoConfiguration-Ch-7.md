# How SpringBoot AutoConfiguration works?

When we work on SpringBoot, we get a Jar by default (i.e. AutoConfigure Jar) and this Jar has a combination of various AutoConfiguration classes.
Usually we have to configure quite a lot of things when with integrate Spring with SpringSecurity, SpringWebMvc etc. In case of SpringBoot those configurations
are done by default. So they have different packages where configurations related to different modules are already done by Spring.

<img width="444" alt="Screenshot 2024-06-22 at 10 51 34 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6e6708c1-ec23-4db9-aa8b-bef4d2189613">
<img width="444" alt="Screenshot 2024-06-22 at 10 51 46 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/678da9d7-d0f0-4be0-b182-c52126b7c519">

There is a file under META-INF/spring folder where all different autoconfiguration classes are mentioned.

<img width="411" alt="Screenshot 2024-06-22 at 11 14 04 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/67ed8c47-cdad-4b90-b7ce-26294e1fd127">
<img width="1102" alt="Screenshot 2024-06-22 at 11 16 19 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/76a656b1-e8cb-4419-b38c-577d7bd171dc">

These AutoConfiguration classes create Beans on the fly so that we don't have to do it ourself.

<img width="1136" alt="Screenshot 2024-06-22 at 11 46 06 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a88029b0-a482-4684-a02d-bff151d30558">

#### But when do they activate?

It gets activated in our StarterApp where "run" method is called.

<img width="335" alt="Screenshot 2024-06-22 at 11 21 53 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6cc68707-afd4-4aad-9571-ed8e2c359677">

We have *@EnableAutoConfiguration* annotation which triggers all the AutoConfiration Class files.

<img width="290" alt="Screenshot 2024-06-22 at 11 22 38 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bda88061-68c2-424a-83c7-b2297fd739f0">

The *@SpringBootApplication* has *@EnableAutoConfiguration* annotation.

<img width="799" alt="Screenshot 2024-06-22 at 11 25 15 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1128f454-828b-4faa-bf0b-d6c901deb676">

#### But what if we don't need Beans to be created for all different Classes present (There are so many AutoConfiguration classes) ?

Spring creates beans based on Conditions. Consider TomcatServer. Bean for the same gets created only when in our classpath(in maven dependency), 
we have webmvc Jar/servlet Jar. Why would we require these Jars otherwise?

Example 1: In case of TomcatServer, bean gets created only when "Servlet.class" lies in our classpath.

<img width="1172" alt="Screenshot 2024-06-22 at 11 29 22 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9862e931-c06e-4531-9501-a0c26d70be38">

Example 2: DispatcherServlet

<img width="417" alt="Screenshot 2024-06-22 at 11 37 28 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/09efa320-2075-4cf9-b828-3ded154bc1f5">
<img width="1147" alt="Screenshot 2024-06-22 at 11 38 10 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1f52734f-06eb-4a82-bb61-893b1375c52a">

There are different types of Conditionals like ConditionalOnClass, ConditionalOnBean etc.

**ConditionalOnBean:** Creation of Bean is dependent on existence of another Bean(say xyz) in the Applicationcontext.

<img width="416" alt="Screenshot 2024-06-22 at 11 42 12 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1b5132bf-2532-47c1-bfc6-4b571e0a75e5">

# Create custom AutoConfiguration in SpringBoot

Create a custom AutoConfiguration Class

<img width="815" alt="Screenshot 2024-06-22 at 11 53 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4be9d1d2-a186-4d7d-9868-03c73f0ecec4">
<img width="770" alt="Screenshot 2024-06-22 at 11 52 16 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/da926c6c-3119-4b62-9015-007d698fba23">

Let's implement *CommandLineRunner*. Once the main method executes and object of WebApplicationContext is created, run method of CommandLineRunner
is automatically called and executed.

<img width="1006" alt="Screenshot 2024-06-22 at 12 08 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/02cfe55f-5217-409a-9290-83215f6f2e34">
<img width="1344" alt="Screenshot 2024-06-22 at 12 09 03 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/71dbddcf-419e-4326-99fc-9f89f83dae38">

## Custom AutoConfiguration step by step

We can also create Bean by adding a method with *@Bean* annotation in StarterApp.

<img width="915" alt="Screenshot 2024-06-22 at 12 24 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/08ef58c8-31bb-4f9d-8df2-b9c24e74e574">

Let's try to move the method to a separate class and run the application

<img width="903" alt="Screenshot 2024-06-22 at 12 27 55 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9ecc2e76-d71d-4b0c-84ee-4281da4f5a96">
<img width="1240" alt="Screenshot 2024-06-22 at 12 28 07 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bf64dd84-2ff5-4f1e-b342-77d4923a0245">

Couldn't create Bean as Spring couldn't identify it as a Component

Let's try to add *@Configuration* annotation and run the application. Note that *@Configuration* contains *@Component* annotation.

<img width="873" alt="Screenshot 2024-06-22 at 12 29 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/16d6a104-e1de-48dc-a0bd-6623d7f733c2">
<img width="607" alt="Screenshot 2024-06-22 at 12 29 09 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b93c8e25-1b18-4364-8fa0-10b398e01a93">
<img width="1195" alt="Screenshot 2024-06-22 at 12 29 28 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/50d2232e-689e-4335-bed5-48d8407cc10f">

#### What if we add @AutoConfiguration annotation? It contains *@Configuration* as well.

<img width="973" alt="Screenshot 2024-06-22 at 12 36 35 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b34aec4f-96f1-4485-9852-021ed7f6ac27">
<img width="845" alt="Screenshot 2024-06-22 at 12 31 08 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ff6e9375-4839-4666-9c30-9dfa8e44b2c5">
<img width="1240" alt="Screenshot 2024-06-22 at 12 30 31 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b3b2a85b-5b8d-4132-8926-a98e122d526d">

**Is *@AutoConfiguration* same as *@Configuration*?** - **NO**

We know that for autoConfiguration to work, we need to add our AutoConfiguration class in a File present in META-INF/spring folder.

<img width="457" alt="Screenshot 2024-06-22 at 12 40 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d03f86a3-695d-45f5-90cf-e612433a62a7">

We can create our own file with same name in src/main/resources under META-INF/spring folder

<img width="387" alt="Screenshot 2024-06-22 at 12 45 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c7b81978-91d5-426b-b1b6-04d90b0f9944">

We need to give an entry to the class with fully qualified path

<img width="1001" alt="Screenshot 2024-06-22 at 12 46 03 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/91b10e02-7010-4b7e-8aa4-563a05432608">

We have *@SpringBootApplication* annotation over our StarterApp. *@SpringBootApplication* internally has *@EnableAutoConfiguration*.

<img width="202" alt="Screenshot 2024-06-22 at 12 48 54 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/58f3e4c8-726e-4c7f-a1ae-e606af13d8bf">
<img width="771" alt="Screenshot 2024-06-22 at 12 49 03 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3f7f089a-9944-4521-84d2-49a34aacb9a1">

Run the application and we'll see Spring is able to detect our Custom AutoConfiguration class

<img width="1344" alt="Screenshot 2024-06-22 at 12 52 45 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ca098e73-da19-4702-8534-c236d8a4fff3">

#### Conditionals

Let's create an "Example" class and configure such that Bean of Custom AutoConfiguration class gets created only if Example.class exists in 
classpath.

<img width="1013" alt="Screenshot 2024-06-22 at 12 58 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f770d89f-851d-461e-8a33-2bc034b95924">
<img width="863" alt="Screenshot 2024-06-22 at 12 58 43 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e801377a-b425-41bc-ad1c-a907e9bfee8d">

We can also write (This will give compilation error though if class doesn't exist)

<img width="796" alt="Screenshot 2024-06-22 at 1 04 55 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e4de806a-0c46-44f7-a5df-b6b4b970341e">

<img width="1342" alt="Screenshot 2024-06-22 at 12 59 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/46c886d3-6525-493f-a69b-6819d938e966">
<img width="951" alt="Screenshot 2024-06-22 at 1 01 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8baa2d22-c997-4793-9ff4-66ceec8c6a86">

If we delete Example class, application will fail to start

<img width="1309" alt="Screenshot 2024-06-22 at 1 02 44 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0161747d-5896-4a98-9ee7-9d369f102c7c">

We can also have Conditional on beans where a bean is dependent on existence of another bean

##### Note: Nean name should be same as the one mentioned

<img width="773" alt="Screenshot 2024-06-22 at 1 07 30 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a8d12f9f-2158-436c-a897-257c8193b996">




