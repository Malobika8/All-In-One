**Injecting literal values from properties file using Spring annotations**

* Create a properties file

<img width="789" alt="Screenshot 2024-05-21 at 11 09 23 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0dd93134-e7d7-4c74-856f-bee75be38224">
<img width="1029" alt="Screenshot 2024-05-21 at 11 15 29 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/18cdb9f4-d493-49e9-8385-23f6a1655809">
<img width="824" alt="Screenshot 2024-05-21 at 11 12 23 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d70e7ba9-4342-437e-8c12-3f3845da3e54">

But what if we don't want to set properties through xml file? - We can use annotations.

* @Value:

  <img width="1033" alt="Screenshot 2024-05-21 at 11 21 50 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/89379d1b-3b88-4887-a008-12413c958708">
  <img width="1126" alt="Screenshot 2024-05-21 at 11 21 59 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/748dcbb0-4f05-4803-86cb-e00b9d7f8b9f">

But which properties are mandatory? It we don't set any of the peroperty values, the value returned will be null. But a property can be mandated
using @Require annotation.

<img width="1026" alt="Screenshot 2024-05-21 at 11 26 00 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/161b9ff2-7867-4211-9596-28a5b5b08da8">
<img width="475" alt="Screenshot 2024-05-21 at 11 26 45 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1535104a-1ba6-44c3-bee2-a51f06cf1560">

* @Require:
  
  <img width="773" alt="Screenshot 2024-05-21 at 11 28 45 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6a2c44a8-17e7-4ac9-a047-da9300eefa5b">

**Note:** We can set from properties file as well.

<img width="781" alt="Screenshot 2024-05-21 at 11 32 07 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0b7c834e-b1fc-477f-85fc-8ce47ddfad14">

@Value & @Required can be placed diretly above the fields. In that case, setter methods are not made use of.

<img width="709" alt="Screenshot 2024-05-21 at 11 38 25 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/eda6043e-1cd4-4526-9b22-71d1d72626f1">
