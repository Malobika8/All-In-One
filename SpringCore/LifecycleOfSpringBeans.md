# **Lifecycle of Spring beans**
- **Using xml**
  <img width="1127" alt="Screenshot 2024-05-12 at 9 41 00 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/96a55736-9571-41fb-9745-6123e0e3bf40">
  <img width="1122" alt="Screenshot 2024-05-12 at 9 43 32 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fdf1fe85-6206-4c29-a03a-bfd88f0d56db">
  <img width="1060" alt="Screenshot 2024-05-12 at 9 44 49 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/be3811e2-c31d-4ad6-9d4d-f39cfcdd1280">
  <img width="914" alt="Screenshot 2024-05-12 at 10 12 52 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ffb8682d-807f-452c-bdf8-c27fe5b03aa1">
  <img width="935" alt="Screenshot 2024-05-12 at 10 14 06 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/61ede481-9789-40c4-83dd-5e68279fe976">
  <img width="396" alt="Screenshot 2024-05-12 at 10 14 19 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3915cca3-e383-45ee-a553-23748cc7d3df">
  <img width="934" alt="Screenshot 2024-05-12 at 10 12 26 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1cc4cbca-22cf-4ca8-a3f7-1a132dbd997a">
  <img width="1220" alt="Screenshot 2024-05-22 at 11 16 47 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c4bf0f67-53a5-429c-83cf-a3681c752615">

- **Using annotation**

  * @PostConstruct: It can be used for setting up resources like db/socket/file etc.

  * @PreDestroy: Clean up unused references. Before out container object gets destroyed, spring calls our custom destroy method.

  <img width="755" alt="Screenshot 2024-05-12 at 10 16 25 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6c50034b-edb7-4c48-9a41-9d0d9f796ba9">

  *Note:*
    * For SE applications, we need to manually close the container.
    * For EE applications, framework closes the container automatically.

    <img width="1145" alt="Screenshot 2024-05-22 at 11 01 33 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e7d716ef-5c13-470b-9330-b3acb7935372">
    <img width="1062" alt="Screenshot 2024-05-22 at 11 02 00 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b6b9debc-a32a-4fcb-b6ee-11c0120a6920">
    <img width="854" alt="Screenshot 2024-05-22 at 11 05 24 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3b0c52af-20fc-48ee-9f7f-28f3d1c74aa5">
    <img width="737" alt="Screenshot 2024-05-22 at 11 06 08 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/293fe9cd-ca4e-45f5-97f0-8224c4c345f7">
    <img width="1072" alt="Screenshot 2024-05-22 at 11 06 21 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/10c3c1fa-c04d-438f-b067-e9da701f9b96">
    <img width="1143" alt="Screenshot 2024-05-22 at 11 07 48 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0b151e3e-8f59-4b52-bab4-034e08eff632">
    <img width="1141" alt="Screenshot 2024-05-22 at 11 08 01 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fd161532-4e84-4585-b1a8-351d3d515a3b">

**Note**

  <img width="1008" alt="Screenshot 2024-05-12 at 10 22 28 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/67518f8b-f32f-4b46-9b4e-0db3e0da36bd">

*To enable all annotations,*

<img width="927" alt="Screenshot 2024-05-12 at 10 25 28 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/40494342-fe36-47f5-b398-4a69044f7aba">
<img width="852" alt="Screenshot 2024-05-12 at 10 24 15 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fcc13d43-113b-41b5-b1b1-34d6b8a2b867">

<img width="583" alt="Screenshot 2024-05-12 at 10 26 24 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d8c5bff5-766a-4d33-92ca-329eefea403c">

*Or if we want to enable only PostContruct and PreDestroy, we can add a bean of the class*

<img width="1232" alt="Screenshot 2024-05-22 at 11 10 44 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0bbcf44f-8c39-44da-9a26-5b938137cec7">
<img width="1073" alt="Screenshot 2024-05-22 at 11 11 42 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/34fbda89-e9a5-489d-8efd-8f7299988b19">
<img width="1075" alt="Screenshot 2024-05-22 at 11 11 52 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/20bf6226-afee-4cf5-9be6-4ec385609725">
<img width="1224" alt="Screenshot 2024-05-22 at 11 12 49 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fc89190a-dd68-47f7-8cc1-d5a87e6e3e70">

<img width="1072" alt="Screenshot 2024-05-22 at 11 17 29 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/aaf54993-df05-41dd-81fa-a67d39694b62">
<img width="1072" alt="Screenshot 2024-05-22 at 11 17 48 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3ff0dfac-1b1d-4d40-a57b-d2da4a84f2f6">
<img width="1061" alt="Screenshot 2024-05-22 at 11 18 30 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/40dad6fa-86ce-45c3-ae39-365c0839660f">
<img width="911" alt="Screenshot 2024-05-22 at 11 19 23 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8514931d-f96e-41ff-a3cf-01d25440f1d2">
<img width="534" alt="Screenshot 2024-05-22 at 11 19 35 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/bbb358b2-2ba6-4296-8500-ed59b22bcf0f">
<img width="946" alt="Screenshot 2024-05-22 at 11 19 54 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1c2ddc85-bb4e-4f61-85e7-9921096d38a4">
<img width="404" alt="Screenshot 2024-05-22 at 11 20 03 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f4ba0474-e503-4ce2-aa21-3e24521ddb46">
<img width="814" alt="Screenshot 2024-05-22 at 11 20 22 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/670dd61e-012a-4394-9d84-c8a7c423a059">
<img width="1134" alt="Screenshot 2024-05-22 at 11 20 31 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/43e0cae3-c39b-42c4-af05-30ebadefafad">
<img width="987" alt="Screenshot 2024-05-22 at 11 20 48 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0f948857-30ed-4f49-b5c9-18b15e31c965">
<img width="897" alt="Screenshot 2024-05-22 at 11 21 09 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/835edc38-d685-4709-ae30-ac9771eb40b4">
<img width="510" alt="Screenshot 2024-05-22 at 11 21 56 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d7549ea0-6209-440f-ae29-2bf3a8e9cd38">

<img width="1129" alt="Screenshot 2024-05-22 at 11 23 43 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fe6176da-04ba-4b2c-a919-8e02cdc2216b">
<img width="1135" alt="Screenshot 2024-05-22 at 11 23 55 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5cbb9f6a-3af7-436f-ae19-f6835f1778f9">
<img width="1103" alt="Screenshot 2024-05-22 at 11 24 06 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9550674b-d557-414b-bd67-f30cdd7a1fa1">
<img width="1124" alt="Screenshot 2024-05-22 at 11 24 28 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/53918bbc-0dc5-4150-a27c-c9b0f4321263">
<img width="1109" alt="Screenshot 2024-05-22 at 11 25 43 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/425aab46-2a60-435a-972f-3d231dee7e15">
<img width="772" alt="Screenshot 2024-05-22 at 11 29 13 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/107252ca-ea12-48d3-8c2c-09d67639c2af">
<img width="1187" alt="Screenshot 2024-05-22 at 11 30 34 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/40dd4d22-c637-4d3c-8e94-1d27bdf40580">
<img width="1022" alt="Screenshot 2024-05-22 at 11 30 42 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/75e63cc7-e0b2-4f6d-8840-68fcef10424d">
<img width="1125" alt="Screenshot 2024-05-22 at 11 31 02 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e54c3fbe-131b-4c24-8e1c-16c83c3d2119">
<img width="1178" alt="Screenshot 2024-05-22 at 11 31 08 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/675dac8b-524d-4b06-937f-181825d9879b">
<img width="992" alt="Screenshot 2024-05-22 at 11 31 15 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/85870b24-0497-448c-8575-1d2cad9db27d">
<img width="798" alt="Screenshot 2024-05-22 at 11 33 30 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d7efb8d0-1777-4aa0-a447-e1ed0bd467b4">
<img width="900" alt="Screenshot 2024-05-22 at 11 34 11 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b4b06856-5398-40f2-8c8f-9d2e8353fa39">









