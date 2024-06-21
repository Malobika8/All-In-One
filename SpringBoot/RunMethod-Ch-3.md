# The *Run* method

Run actually helps us to Bootstrap our application.

<img width="1144" alt="Screenshot 2024-06-21 at 9 59 30 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e1c41936-fd56-429f-853d-d7028956b6c1">

It creates the Container/ApplicationContext for us. If we see, the run method returns a generic Application Context i.e. **ConfigurableApplicationContext**.
This is basically an Interface which extends ApplicationContext.

<img width="1046" alt="Screenshot 2024-06-21 at 10 11 34 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4d31e154-dc0f-4df4-a5a4-f6bc12d9fbbe">

There are multiple implementations some of which we have already used.

<img width="1395" alt="Screenshot 2024-06-21 at 10 12 51 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/86e2f994-7fb4-4841-b0c1-15960f6ff477">

Let's try to prove that it actually creates a Bean for us.

Consider a simple class called "College" with *@Component* annotated. This instructs Spring to create a Bean for the class.

<img width="849" alt="Screenshot 2024-06-21 at 10 03 01 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/466df73f-f33c-4e5e-a781-39d9ddc5f9a3">
<img width="781" alt="Screenshot 2024-06-21 at 10 03 41 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8fe2ff8e-778b-465b-bcec-60f099cd72df">
<img width="1113" alt="Screenshot 2024-06-21 at 10 07 38 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cdf00173-c01b-4c44-a7dc-93de3961898d">
<img width="1102" alt="Screenshot 2024-06-21 at 10 07 56 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/935e3016-ffae-4200-8001-03e758744521">
<img width="1008" alt="Screenshot 2024-06-21 at 10 09 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/dd51232e-5838-4244-9966-4c8a452fbcf8">

### *What if we remove @Component from the class?*

<img width="864" alt="Screenshot 2024-06-21 at 10 19 40 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/25d7f631-329b-47e4-adf8-b24af5c3fa95">

We can manually create the bean as well with the *@Bean* annottaion.

<img width="825" alt="Screenshot 2024-06-21 at 10 21 08 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/50d8962f-1b8d-4c1f-9d3d-72c8cae5084d">

This time it will work fine

<img width="1072" alt="Screenshot 2024-06-21 at 10 23 08 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5d8e4517-641c-479a-91fa-77be8576e41e">

But if we keep Bean related configuration in the same class, we can mark the class with *@Configuration*. This tells Spring that Bean related 
configuration is available as well. We can also use *@SpringBootConfiguration* (this basically has *@Configuration* as well).

<img width="1132" alt="Screenshot 2024-06-21 at 10 24 35 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/057669ea-0ecc-4f01-bbf9-8bae86196240">
<img width="1124" alt="Screenshot 2024-06-21 at 10 24 47 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/913b1232-04d1-454c-bd2f-1107904c3703">
<img width="1108" alt="Screenshot 2024-06-21 at 10 24 57 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2295ce2a-0964-4fa6-9f05-4fe87b213a6d">
<img width="1152" alt="Screenshot 2024-06-21 at 10 28 11 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9b713f7f-5c1a-400c-9494-21f7872d704a">

**Note:** The **StarterApp** is used as a Source to our Application.

There's another annotation called *SpringBootApplication* that bundles previous annotations used i.e. *@EnableAutoConfiguration*, *@SpringBootConfiguration*.

<img width="867" alt="Screenshot 2024-06-21 at 10 49 54 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/90b61294-4af3-4cda-99fc-9d2c4e485d4d">
<img width="1124" alt="Screenshot 2024-06-21 at 10 48 41 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ab0bb5d0-53ea-4cca-a0a9-6d828c9f6bff">

Run the Application

<img width="1032" alt="Screenshot 2024-06-21 at 10 49 20 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/883db7f9-b736-432c-818b-2ad6c6ec127f">

We can see, *@SpringBootApplication* contains other necessary annotations.

<img width="927" alt="Screenshot 2024-06-21 at 10 49 31 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/211398f4-df77-4f13-9e74-052a4d440fa1">
<img width="975" alt="Screenshot 2024-06-21 at 10 49 46 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/589739d0-46cb-4919-9032-3dcc27a5b372">

## How to deploy our app in a port another than 8080

*By default, the Tomcat instance runs on port no 8080.*

To do this, we need to configure some properties. Click on Run Configurations and add port in Arguments section.

<img width="1146" alt="Screenshot 2024-06-21 at 3 19 32 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/10ecaf06-3a19-42de-ab84-30d4dfb8f2db">
<img width="874" alt="Screenshot 2024-06-21 at 3 21 53 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e29afd2f-06be-4d55-83a7-f4a30b87ac7e">
<img width="949" alt="Screenshot 2024-06-21 at 3 23 04 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e0baa2f5-5def-439c-a50d-ad4b613918ff">

Port no changed

<img width="1076" alt="Screenshot 2024-06-21 at 3 23 36 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/72998fbb-39fa-4ee1-8bb2-923b8d0dd394">

*Note: Arguments always need to be passed to the Run method whenever we use it*

There are different "run" methods in SpringApplication class, one of which is static. So, instead of creating a SpringApplication object 
and then calling the run method, we can directly call the static "run" method. Static run method internally calls the one which we are using currently.

<img width="468" alt="Screenshot 2024-06-21 at 3 28 14 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a399657e-69c1-4862-a371-82b694cd3caf">
<img width="908" alt="Screenshot 2024-06-21 at 3 30 34 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c6e31e80-2354-4b39-a97f-51c5336ba447">
<img width="1064" alt="Screenshot 2024-06-21 at 3 33 23 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f0753001-33cf-4497-a32f-91bc0efefdf0">

So we write as

<img width="966" alt="Screenshot 2024-06-21 at 3 34 57 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d0b7a0e4-7335-4475-9e12-cd7aaec10c2f">






