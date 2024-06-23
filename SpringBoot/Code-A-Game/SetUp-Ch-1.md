## Project Setup

1. Create a new Project (maven-archetype-quickstart)
2. Add the following Dependencies

   <img width="1022" alt="Screenshot 2024-06-23 at 7 49 49 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9a031892-f878-4cc8-aacc-8f9c775bfcda">

   ### *Note:*
   Spring Boot DevTools is a set of tools in the Spring Boot framework that provide a bundle of features for rapid application development
   and testing. It offers features such as live reload, restart, and web-gevent integration. Live reload allows for automatic recompilation
   and redeployment of the application after changes are made. Restart provides a simple way to restart the application after changes are
   made. Web-gevent integration enables simultaneous requests to be handled more efficiently. DevTools is particularly useful for rapid
   development, testing, and prototyping, and can be easily disabled for production environments.

3. For Automatic Reloading,
   - Go to "Settings"
  
     <img width="301" alt="Screenshot 2024-06-23 at 7 53 45 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0759f0d6-db81-4eb3-a7ed-14d3fbef6e75">

   - Go to "Compiler" under "Build,Execution,Deployment"
   - Check "Build project automatically". This ensures our changes are automatically built in IDE and reloaded by SpringBoot. (We won't have to restart again & again).
   - Click on "Apply" & then "Ok"
  
     <img width="981" alt="Screenshot 2024-06-23 at 7 54 00 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e85a3829-df08-41b0-b130-5cda8c39fe12">

4. Add a main method which will have "run"

   <img width="919" alt="Screenshot 2024-06-23 at 8 19 37 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d243aec2-82f1-47c9-9176-45467b335ed6">

5. Create Controller (GameController)

   <img width="1022" alt="Screenshot 2024-06-23 at 8 57 01 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cd61ef27-fb93-4e70-ae04-5b26b7e65d4f">

6. Create Service

   <img width="1030" alt="Screenshot 2024-06-23 at 8 58 27 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bb19a116-ac1d-44d5-817b-f03e272d07b3">

8. Create resources/templates folder and add a html file. Don't forget to add Thymeleaf namespace.

   https://www.thymeleaf.org/doc/tutorials/2.1/usingthymeleaf.html
   
       <html xmlns:th="http://www.thymeleaf.org">
     
   <img width="741" alt="Screenshot 2024-06-23 at 8 22 00 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/73f3b70f-5904-40fe-98ec-7aa46a6539c1">
   <img width="362" alt="Screenshot 2024-06-23 at 8 22 16 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3e1cc942-61cb-4d8a-bdb5-deb1ab21f264">
   <img width="806" alt="Screenshot 2024-06-23 at 8 54 30 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/82225abb-cc49-406a-8ee9-b00783abf720">

10. Run the Application

   <img width="1217" alt="Screenshot 2024-06-23 at 9 34 04 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/082ae0e0-aaea-49ed-a259-dc0125f84b47">
