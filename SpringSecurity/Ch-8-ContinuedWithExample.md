### Create a table.

<img width="861" height="267" alt="Screenshot 2025-08-25 at 12 18 47 PM" src="https://github.com/user-attachments/assets/7518e903-adcd-4dda-a287-474552955394" />
<img width="605" height="220" alt="Screenshot 2025-08-25 at 12 19 40 PM" src="https://github.com/user-attachments/assets/2ab407d3-1c7d-4e4f-a040-859a77e10a17" />

## Loading login data using JDBCTemplate

<img width="725" height="413" alt="Screenshot 2025-08-25 at 12 24 55 PM" src="https://github.com/user-attachments/assets/099678c7-d5a6-4121-bdae-3c49883bffd1" />
<img width="597" height="511" alt="Screenshot 2025-08-25 at 12 25 27 PM" src="https://github.com/user-attachments/assets/a48e03f9-514a-4431-8b7b-53aa16996c48" />
<img width="806" height="351" alt="Screenshot 2025-08-25 at 12 25 36 PM" src="https://github.com/user-attachments/assets/6e8debbd-fdd3-41da-847d-2b38e814cc52" />
<img width="864" height="337" alt="Screenshot 2025-08-25 at 12 27 29 PM" src="https://github.com/user-attachments/assets/2eb090cf-50de-4743-aa60-312f485574c6" />

#### Note: we can come across an error if multiple UserDetailsServiceManager beans are present. (Comment/remove one of them)

<img width="821" height="330" alt="Screenshot 2025-08-25 at 12 27 55 PM" src="https://github.com/user-attachments/assets/59e23880-5854-4bf1-9cb7-d01e62357319" />
<img width="841" height="343" alt="Screenshot 2025-08-25 at 12 29 06 PM" src="https://github.com/user-attachments/assets/b31c8cea-d588-4c57-92d5-0182c4b33a9e" />
<img width="802" height="192" alt="Screenshot 2025-08-25 at 12 29 50 PM" src="https://github.com/user-attachments/assets/6ba7704a-21df-4ea3-800a-d35d34dde3f2" />

### Try to login and check if the custom method is getting called.

<img width="671" height="356" alt="Screenshot 2025-08-25 at 12 30 04 PM" src="https://github.com/user-attachments/assets/45689057-2c9c-40fe-a327-b53eb2eb28cf" />
<img width="896" height="172" alt="Screenshot 2025-08-25 at 12 30 47 PM" src="https://github.com/user-attachments/assets/8f4387b6-47d3-412d-bdc2-8ca8b0225ecb" />

### Create a DTO class.

<img width="848" height="564" alt="Screenshot 2025-08-25 at 12 36 25 PM" src="https://github.com/user-attachments/assets/ddc2f885-2700-4917-bb21-3ba362ae16f5" />

### Provide Impl

<img width="701" height="574" alt="Screenshot 2025-08-25 at 12 42 31 PM" src="https://github.com/user-attachments/assets/2da8a69e-d13b-4856-8fe9-d0c335799031" />
<img width="959" height="536" alt="Screenshot 2025-08-25 at 12 40 26 PM" src="https://github.com/user-attachments/assets/cb24c145-bb82-433f-951e-69c99c80a5a3" />

### try to sign in

<img width="585" height="366" alt="Screenshot 2025-08-25 at 12 43 22 PM" src="https://github.com/user-attachments/assets/d31723dc-f367-449f-9408-046b52f4bffa" />
<img width="793" height="297" alt="Screenshot 2025-08-25 at 12 43 30 PM" src="https://github.com/user-attachments/assets/cc0e0adf-9fa4-45f8-ad78-7fc48e839574" />

#### Note: if a user doesn't exist, we might come across this error. ("*queryForObject()*" always expects a return value. If it's null, it throws an error. It's better to use "*query()*" method instead. Note that "*query()*" returns a Collection.)

<img width="620" height="325" alt="Screenshot 2025-08-25 at 12 43 59 PM" src="https://github.com/user-attachments/assets/3255cc56-195b-447b-bcc4-8a279cda099a" />
<img width="532" height="370" alt="Screenshot 2025-08-25 at 12 44 03 PM" src="https://github.com/user-attachments/assets/92533dda-2d0f-4eb3-9def-a4a5ada7ff1e" />
<img width="963" height="580" alt="Screenshot 2025-08-25 at 12 46 22 PM" src="https://github.com/user-attachments/assets/b369ec0b-aecb-4a9b-b220-c87a3c2eb7f8" />
<img width="727" height="318" alt="Screenshot 2025-08-25 at 12 47 04 PM" src="https://github.com/user-attachments/assets/fabd26ec-5331-40f0-979a-01db253b2614" />

#### We can run in debug mode and check

<img width="735" height="382" alt="Screenshot 2025-08-25 at 12 48 33 PM" src="https://github.com/user-attachments/assets/4962a677-57d2-4cab-9202-856e09ec8627" />

## Login using email ID

<img width="956" height="573" alt="Screenshot 2025-08-25 at 12 50 54 PM" src="https://github.com/user-attachments/assets/cc0087f0-7e03-4ee2-a58f-bac478ac8f6a" />
<img width="549" height="341" alt="Screenshot 2025-08-25 at 12 51 28 PM" src="https://github.com/user-attachments/assets/d3c3cbb5-0616-46d5-8234-61f85e7b632e" />
<img width="775" height="239" alt="Screenshot 2025-08-25 at 12 51 37 PM" src="https://github.com/user-attachments/assets/f6833093-54e9-47e2-ba8e-364c669ab3be" />
