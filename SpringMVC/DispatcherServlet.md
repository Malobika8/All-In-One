# **DispatcherServlet**

  Front Controller: The front controller handles all the requests to the web application. This implementation of centralized control that
                    avoids using multiple controllers is desirable for enforcing application-wide policies such as user tracking and security.
                    It routes the request to one of the specific controllers.

                    <img width="1147" alt="Screenshot 2024-05-27 at 11 21 40 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ebb02eb1-2c9d-4790-b7b6-46a00a787b95">

  Spring has a front Controller readily available called DispatcherServlet. It can used similar to how other servlets are used by configuring
  in web.xml file.
  
  <img width="929" alt="Screenshot 2024-05-27 at 11 53 11 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9a3c5215-2ac1-4734-8849-e8b7964513e7">

  **When DispatcherServlet will be initialized?** - It will be initialized once the application deployment is done inside the Tomcat server.
  "load-on-startup" tag makes sure that whenever the Server is started, DispatcherServlet is initialized. 
  
  <img width="946" alt="Screenshot 2024-05-27 at 12 01 27 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5cf8a871-e4f8-4624-92be-8965818a813c">

  However, while initializing the DispatcherServlet, it checks for an xml file based on the DispatcherServlet name.
  
  <img width="1148" alt="Screenshot 2024-05-27 at 12 07 10 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/538a5ed3-24c5-42c2-9811-eac9075c39f5">

  **Why though?** - 
