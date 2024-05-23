# Intro

Imagine we have a client machine and a server. In web world, client sends a request to server expecting a response. It can be a string, json, html page(static(already built) or dynamic(build at runtime)) etc. When we ask for a page at runtime and send a request to the server, since the page is not kept handy as it is supposed to build at runtime, the request goes to the helper application(also called as Web Container(tomcat, glassfish, jBoss, websphere etc)). The Web Container will have servlets which are basically java files that can take request from the client on the internet and send response after processing the request.

<img width="550" alt="Screenshot 2024-05-23 at 10 51 13 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3e14a388-2d0d-4b8c-bbc7-9ce9ecf2e3f4">
<img width="517" alt="Screenshot 2024-05-23 at 10 56 34 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/90dd086b-4fc3-4d0c-aca3-5bd925e6dcef">

Inside the container has a special file called deployment descriptor web.xml where it is mentioned for which requests which servlet should be called. All of these should be configured in a file called deployment descriptor.

<img width="560" alt="Screenshot 2024-05-23 at 11 00 22 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/47ca42d5-d04b-48fa-9fe1-0a320e77ca3c">

Servlets are normal java classes which extends HttpServlet to utilize servlet features.

We can use annotations as well instead of configuring in web.xml. Mapping can be done using annotations.
