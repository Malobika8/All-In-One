# **Another way to Configure DispatcherServlet**

<img width="1141" alt="Screenshot 2024-05-30 at 12 57 14 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a92ee8d9-16cb-4904-b30d-2f239425173d">
<img width="1009" alt="Screenshot 2024-05-30 at 12 57 23 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1c6cc889-be69-4cf9-834f-6e1cd3131c28">
<img width="1142" alt="Screenshot 2024-05-30 at 12 57 33 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/be83103f-3f90-4b65-b8d7-ab67dcaa98e8">
<img width="916" alt="Screenshot 2024-05-30 at 12 57 45 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/50a959ef-46b2-425c-9b53-152de6963418">
<img width="1062" alt="Screenshot 2024-05-30 at 1 06 58 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/91e82fb8-27a1-4514-b326-6fe431f73550">

Our class internally implements WebApplicationInitializer

<img width="1140" alt="Screenshot 2024-05-30 at 1 09 02 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/bd87ee5b-4099-4ea1-ab78-3fef89cf4776">
<img width="1129" alt="Screenshot 2024-05-30 at 1 10 20 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f5dd1a17-2500-4b70-a944-e192fddabce9">
<img width="938" alt="Screenshot 2024-05-30 at 1 11 18 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6f3e3932-71e8-4479-8a67-104db0d906aa">
<img width="1124" alt="Screenshot 2024-05-30 at 1 11 36 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f2f28a7f-12a0-43af-9b28-9d7bb2e0926e">
<img width="799" alt="Screenshot 2024-05-30 at 1 11 52 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/961f208c-657d-4e65-93d6-145ce8d2678f">

To summarize,
  - LCAppInitializer extends AbstractAnnotationConfigDispatcherServletInitialize
  - AbstractAnnotationConfigDispatcherServletInitializer extends AbstractDispatcherServletInitializer
  - AbstractDispatcherServletInitializer extends AbstractContextLoaderInitializer
  - AbstractContextLoaderInitializer implements WebApplicationInitializer
  - <img width="768" alt="Screenshot 2024-05-30 at 1 15 37 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/de16684e-76b7-4797-ae33-ebf111178d4e">

Spring essentially does the same thing in background what we did in Approach 1,

<img width="1003" alt="Screenshot 2024-05-30 at 1 24 25 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ca517b37-5341-4920-9d80-1556ac9cddb8">

*Note:* When we delete web.xml file, it shows an error as missing web.xml

<img width="595" alt="Screenshot 2024-05-30 at 1 31 27 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ae68cc51-bea6-4272-8e38-06c94dee5e37">

To fix, set "failOnMissingWebXml" to false in pom.xml.

<img width="897" alt="Screenshot 2024-05-30 at 4 59 46 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/22722282-d06e-4a3a-a325-c9bfe4af5506">

