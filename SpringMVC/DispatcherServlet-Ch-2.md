# **DispatcherServlet**

  Front Controller: The front controller handles all the requests to the web application. This implementation of centralized control that
                    avoids using multiple controllers is desirable for enforcing application-wide policies such as user tracking and         
                    security. It routes the request to one of the specific controllers.

 <img width="1147" alt="Screenshot 2024-05-27 at 11 21 40 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ebb02eb1-2c9d-4790-b7b6-46a00a787b95">

  Spring has a front Controller readily available called DispatcherServlet. It can used similar to how other servlets are used by configuring
  in web.xml file.
  
  <img width="929" alt="Screenshot 2024-05-27 at 11 53 11 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9a3c5215-2ac1-4734-8849-e8b7964513e7">

  **When DispatcherServlet will be initialized?** - It will be initialized once the application deployment is done inside the Tomcat server.
  "load-on-startup" tag makes sure that whenever the Server is started, DispatcherServlet is initialized. 
  
  <img width="946" alt="Screenshot 2024-05-27 at 12 01 27 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5cf8a871-e4f8-4624-92be-8965818a813c">

  When we run the application on the Tomcat Server, while initializing the DispatcherServlet, we get an error.

  <img width="1342" alt="Screenshot 2024-05-27 at 2 00 28 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/662bb48a-955b-4619-890d-ab2ca75bbaea">
  <img width="1307" alt="Screenshot 2024-05-27 at 2 01 18 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/dfc5d672-2818-4973-a2f4-f9243ca24302">

  This is because while initializing the DispatcherServlet, it checks for an xml file based on the DispatcherServlet name.
  
  <img width="1148" alt="Screenshot 2024-05-27 at 12 07 10 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/538a5ed3-24c5-42c2-9811-eac9075c39f5">

  **How to resolve?** -  Create an xml file and add required namespace.

  <img width="458" alt="Screenshot 2024-05-27 at 2 02 20 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/db6bb10a-5425-4dc3-9656-525e1107e6e4">

    <?xml version="1.0" encoding="UTF-8" ?>
    <beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="
    http://www.springframework.org/schema/beans
    https://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/mvc
    https://www.springframework.org/schema/mvc/spring-mvc.xsd
    http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
    </beans>

  Re-run the application. It should work fine this time.

  **Why is the xml file for DispatcherServlet required though?** - DispatcherServlet receives all of the HTTP requests and delegates them to 
  Controller classes. Hence, a Configuration File is required for the DispatcherServlet for forwarding different requests to different 
  Controllers based on the requirement.

  **What happens when DispatcherServlet is initialized?** - It looks for a configuration file and tries to create a container using the same.
  It tries to create a container called WebApplicationContext.
  For core Standalone containers, we have ApplicationContext & for Web Applications, we have WebApplicationContainer.
  *Note:* In Web Application, it's not our responsibility to start and close WebApplicationContext.

  <img width="1146" alt="Screenshot 2024-05-27 at 6 50 40 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ff880ffe-d46a-4795-8b16-8a8fcef33474">
  <img width="827" alt="Screenshot 2024-05-27 at 6 51 44 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9e2c6c8e-6dd4-4ed3-a2b8-aa96dba324dd">

WebApplicationContext is an Interface and extends ApplicationContext. So, it has all the features of ApplicationContext and some additional features.

<img width="992" alt="Screenshot 2024-05-27 at 7 00 20 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5f927d7a-3bc6-4e7e-8cee-dcda912da243">

The DispatcherServlet creates WebApplicationContext through the xml configuration file, <servlet-name>-servlet.xml. It then checks the file and registers the controller classes onto the container based on the config. It checks if the incoming URL request pattern matches with the URL pattern associated with Request Handlers(methods).

<img width="1085" alt="Screenshot 2024-05-27 at 7 04 14 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/db4f548f-5d99-416a-b5fd-94e61ac1e766">
<img width="1150" alt="Screenshot 2024-05-27 at 7 04 34 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a2ffe122-8abe-40b0-8474-c8eb738435a3">
<img width="1070" alt="Screenshot 2024-05-27 at 7 11 15 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f0286172-8fdc-4fde-8224-cac07a24d827">


