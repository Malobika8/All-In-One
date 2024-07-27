# Let's get started

If we just go to "Action" and start with a simple workflow configuration, we can get the sample file by clicking on "Configure".

<img width="1438" alt="Screenshot 2024-07-27 at 11 30 09 AM" src="https://github.com/user-attachments/assets/fb718c40-0231-424b-ae01-4c9d277005d5">
<img width="965" alt="Screenshot 2024-07-27 at 11 30 21 AM" src="https://github.com/user-attachments/assets/e50b4c4f-e4e0-4f57-8d2f-3fff87bda506">

## Let's look at the steps now.

1. Create a folder in the root folder named "*.github*". Create another folder inside it named "*workflows*". Here, if we create any "yml" files that have the structure & the configurations
   of GitHub Action, GitHub will be able to automatically read it

   <img width="1302" alt="Screenshot 2024-07-27 at 10 32 19 AM" src="https://github.com/user-attachments/assets/d7733526-2315-4363-bbbf-21f7e9a90230">

2. Create a new file "main.yml". It will represent the definition of the pipeline for the project.

   - We need to have a name for the workflow.

     <img width="778" alt="Screenshot 2024-07-27 at 10 34 12 AM" src="https://github.com/user-attachments/assets/0dec168c-f4ed-4455-9339-1e3400b225d8">

   - We need to specify when to trigger these actions.
   
     Note: We can have autocompletion for JSON. Select "*No JSON Schema*" and then click on one of the applicable ones.
     
     <img width="520" alt="Screenshot 2024-07-27 at 10 34 55 AM" src="https://github.com/user-attachments/assets/729ef26b-7936-480e-bcc6-26d4fed46984">
     <img width="521" alt="Screenshot 2024-07-27 at 10 35 22 AM" src="https://github.com/user-attachments/assets/95211aa4-7c2e-4d6e-813f-82a2caafef9e">

     Select on "*Github Workflow*" as well. Post this, we can have autocompletion for this type of file.

     <img width="507" alt="Screenshot 2024-07-27 at 10 37 29 AM" src="https://github.com/user-attachments/assets/c1ea30e3-c5c3-474c-8312-2910d5465055">

     Define when to trigger the pipeline.

     <img width="1038" alt="Screenshot 2024-07-27 at 10 40 43 AM" src="https://github.com/user-attachments/assets/cea9ffd9-914c-4fd4-ab84-3bc68fc90c72">

   - Define Jobs:

     * Name of the Job - "*build-deploy*"
     * Provide name.

       <img width="935" alt="Screenshot 2024-07-27 at 10 43 22 AM" src="https://github.com/user-attachments/assets/8213f615-6022-497e-a180-15c235c372f0">

     * Define Runner (It's a machine where we want to run these actions): We have a list of Runners that are pre-defined by Github. We can even create our self-hosted Runners.

       <img width="843" alt="Screenshot 2024-07-27 at 10 44 45 AM" src="https://github.com/user-attachments/assets/8f7f7638-c827-4705-9ed8-f6f6da2d3ae6">
       <img width="840" alt="Screenshot 2024-07-27 at 10 46 13 AM" src="https://github.com/user-attachments/assets/83d9468d-f89d-48a4-8b3b-336b5d6578bc">

     * Each Job has different steps. Provide "name" and "uses".
    
       "*checkout*" means Github actions will go & copy the code from Github or our repository & clone it into the Runner.

       "*uses*" will have action mentioned. There is one action named "*actions/setup-java@v3*".
    
       <img width="973" alt="Screenshot 2024-07-27 at 11 00 30 AM" src="https://github.com/user-attachments/assets/70cca4e7-9abd-421b-b792-fa26cec21a3c">
       <img width="888" alt="Screenshot 2024-07-27 at 10 51 31 AM" src="https://github.com/user-attachments/assets/01a1d27d-3d6b-43b0-8112-7a9052744313">

       #### But where do we get these actions from?

       - Go to Github marketplace
    
         <img width="1021" alt="Screenshot 2024-07-27 at 10 52 55 AM" src="https://github.com/user-attachments/assets/8eec02b1-d347-4275-98ee-a3abf5ca2aa9">
         <img width="1439" alt="Screenshot 2024-07-27 at 10 53 25 AM" src="https://github.com/user-attachments/assets/5cefbfd6-96f5-4f44-a313-79c5ac143489">

       - Select Actions
    
         <img width="340" alt="Screenshot 2024-07-27 at 10 53 45 AM" src="https://github.com/user-attachments/assets/13823f8e-8d26-438e-8b21-2554f5f22c82">

       - Search for Checkout and we'll find multiple checkout actions available including the verified one.

         <img width="1426" alt="Screenshot 2024-07-27 at 10 54 41 AM" src="https://github.com/user-attachments/assets/dcf8a154-e3a6-4448-b1f9-6fa72899e53b">
         <img width="1436" alt="Screenshot 2024-07-27 at 10 56 43 AM" src="https://github.com/user-attachments/assets/0cfe12da-6509-44c0-b907-79a55e3af41a">

         In the Documentation, we can see how to use it.

         <img width="795" alt="Screenshot 2024-07-27 at 10 57 21 AM" src="https://github.com/user-attachments/assets/d4ae5cd2-4909-490a-b7fc-b5cd50b91bb9">

     * We need to set up JDK 17 on our Runner as our application runs on JDK 17. We can set up any JDK as per the need. We again would need an "action" for this.

       Specify Java version & distribution.

       <img width="967" alt="Screenshot 2024-07-27 at 11 03 20 AM" src="https://github.com/user-attachments/assets/0433636b-8483-4d67-861a-93652defbdf7">

     * We now need to do the first step which is Testing. For Unit Tests, we won't need an action as we need a manual script.
    
       <img width="969" alt="Screenshot 2024-07-27 at 11 06 15 AM" src="https://github.com/user-attachments/assets/dda379ac-33c8-469f-a54a-72844825d52a">

     * Package & Build:
  
       <img width="971" alt="Screenshot 2024-07-27 at 11 08 20 AM" src="https://github.com/user-attachments/assets/045bec6c-be19-4c83-a21b-11c43e2c36be">

     * We are done with checkout, JDK setup, testing, building & packaging.
  
       Let's first test the execution of this build & deploy Job.
  
       Push the changes and check in the "Actions" tab. We can see all the steps happening.

       <img width="1368" alt="Screenshot 2024-07-27 at 11 43 10 AM" src="https://github.com/user-attachments/assets/d238114b-8c68-4c56-99c3-9a2b86c8b0c7">
       <img width="1110" alt="Screenshot 2024-07-27 at 11 40 27 AM" src="https://github.com/user-attachments/assets/013163b1-305f-450a-8e52-425b5439e4c1">
       <img width="1095" alt="Screenshot 2024-07-27 at 11 41 49 AM" src="https://github.com/user-attachments/assets/3f87589c-df75-4d28-b3b0-1f25ebcc2f53">
       <img width="1093" alt="Screenshot 2024-07-27 at 11 42 24 AM" src="https://github.com/user-attachments/assets/a3cc45d5-4de2-4f4d-bd19-94417fed8485">

     * We now need to push it to Docker.
       - Build Docker image

         
         <img width="967" alt="Screenshot 2024-07-27 at 11 11 19 AM" src="https://github.com/user-attachments/assets/484adfba-ff74-46f8-9dbd-7f1f2307adc4">

       - Login to Docker
    
         <img width="963" alt="Screenshot 2024-07-27 at 11 11 26 AM" src="https://github.com/user-attachments/assets/86ec860e-7e39-4771-a67d-411496b2412f">

       - Push image to Docker
      
         <img width="962" alt="Screenshot 2024-07-27 at 11 11 32 AM" src="https://github.com/user-attachments/assets/6d8bb8dc-4e28-4fe7-a2e5-e79039448433">

     * 

         

       
       















