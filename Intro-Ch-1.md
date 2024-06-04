# **Intro**

<img width="1068" alt="Screenshot 2024-06-04 at 12 02 55 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/bdf5a216-f034-4dc4-a24a-d66be5aa99e5">
<img width="1112" alt="Screenshot 2024-06-04 at 12 04 03 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b7382769-b4c4-4435-a829-088e06dbb6ed">
<img width="1147" alt="Screenshot 2024-06-04 at 12 04 30 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e4ee55d1-397c-4bbe-b9af-e9327942a5a1">
<img width="1142" alt="Screenshot 2024-06-04 at 12 06 01 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cbeb7cf9-bf88-46ab-b5f4-dbe73e2dfe3f">
<img width="1137" alt="Screenshot 2024-06-04 at 12 07 52 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cff7ce39-94ac-4538-ac01-0f516318f7fa">
<img width="1131" alt="Screenshot 2024-06-04 at 12 09 03 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/83a1972c-dbf5-48e6-8824-a1af245a608a">
<img width="1136" alt="Screenshot 2024-06-04 at 12 09 43 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8aeee3e2-7a9b-47a3-bb95-c6b63902bd71">
<img width="1126" alt="Screenshot 2024-06-04 at 12 10 59 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/4e3adf1c-28a4-4ced-ad5f-5bd9cc219c9a">
<img width="1146" alt="Screenshot 2024-06-04 at 12 21 10 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f071fa2d-2d50-4a6b-890e-5cded579af88">

* docker run <app-name> <version> : Pulls/Fetches the container and starts it. It executes the start script rightaway as soon as it downloads it.
  There are different layers that gets downloaded. It will take lesser time when we download latest version later as only few layers would require to be updated.

  <img width="1146" alt="Screenshot 2024-06-04 at 12 21 10 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/66608b7a-0a04-470b-8c82-6825f664e622">
  <img width="1146" alt="Screenshot 2024-06-04 at 12 25 21 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/debab8bc-b698-44f6-8fd2-42400820b253">

* docker ps : To see all the running containers

  <img width="1148" alt="Screenshot 2024-06-04 at 12 26 21 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ada8a8a6-72b9-48cf-8bc6-768a6bbf8306">

**Docker Image Vs Docker Container** - 
  - Image is the actual package together with the configuration, dependencies etc. The artifact that can be moved around is actually image.
  - Container is when we pull the image on our local machine & actually start it. The application actually starts and that creates the container environment.

  <img width="1145" alt="Screenshot 2024-06-04 at 12 27 21 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/97ba46de-0e50-45f5-a145-feb9db99a879">
  <img width="1148" alt="Screenshot 2024-06-04 at 12 32 50 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/527cfa26-6cd4-4382-9f68-a304d65573f6">

  If we want another version to run in our machine. Since some of the layers already exist, it doesn't need to fetch it again.

  <img width="1140" alt="Screenshot 2024-06-04 at 12 33 58 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8b97e533-83d8-48c6-9bb9-526768487783">

  We can run any number of applications with different versions of the same application.

  <img width="1133" alt="Screenshot 2024-06-04 at 12 35 16 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f2ef937f-1da9-48f7-8cb1-7930b1ee9a38">

**Docker Vs Virtual Machine**

  <img width="1139" alt="Screenshot 2024-06-04 at 12 37 51 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/638bb148-13ba-414a-ad6a-415dbe1d122e">
  <img width="1124" alt="Screenshot 2024-06-04 at 12 37 56 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9a4cb3a0-752e-47b5-9d6c-205b778f9f51">
  <img width="1119" alt="Screenshot 2024-06-04 at 12 38 55 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/21f13be8-3117-41e2-b6b7-3c5ead430d99">
  <img width="1081" alt="Screenshot 2024-06-04 at 12 40 22 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2992531d-ba30-487b-97c5-fc73ce718827">
  <img width="635" alt="Screenshot 2024-06-04 at 12 40 44 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f3d87631-1325-4eea-8091-3c60f0ec3fe1">
  <img width="869" alt="Screenshot 2024-06-04 at 12 40 51 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f6ec31f1-5c1c-4a97-9900-77e3b4225905">
  <img width="922" alt="Screenshot 2024-06-04 at 12 41 04 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a12ac058-5ffb-46c7-a5f6-5c1de2c840f4">

**Docker Installation**

  <img width="1107" alt="Screenshot 2024-06-04 at 12 43 42 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fd55c74c-57ee-4f39-8d9f-5e1720715021">
  <img width="1112" alt="Screenshot 2024-06-04 at 12 44 38 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ec769c67-3754-47a7-9dce-028d7ae26828">
  <img width="1105" alt="Screenshot 2024-06-04 at 12 44 55 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/24b12763-94ac-48df-b4b2-e50d3c16a805">
  <img width="1127" alt="Screenshot 2024-06-04 at 12 45 11 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/dd625532-a3fa-41a1-b074-9c414a71dbf0">

  Pre-requisites for Mac:

  <img width="699" alt="Screenshot 2024-06-04 at 12 45 33 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/da84b896-0dc7-4664-a1ac-13b5efc2e855">

  Pre-requisites for Windows:

  <img width="853" alt="Screenshot 2024-06-04 at 12 45 45 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6605fbdb-d309-47fd-b700-55dfd33b4adc">

  Docker for Mac:

  <img width="906" alt="Screenshot 2024-06-04 at 1 18 51 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/151188fe-e455-4466-a8ee-61e2ee25bdd6">
  <img width="958" alt="Screenshot 2024-06-04 at 1 22 44 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/aafed5ea-0ce1-47d5-a009-0300671f4b64">
  <img width="1040" alt="Screenshot 2024-06-04 at 1 22 58 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/03e5987d-09c2-453b-9276-d5154350649c">
  <img width="792" alt="Screenshot 2024-06-04 at 1 23 20 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/bda67fde-9aa9-46a9-a4cb-05687a897835">






