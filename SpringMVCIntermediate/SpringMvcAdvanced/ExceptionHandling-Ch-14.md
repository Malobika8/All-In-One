# @ControllerAdvice

* ### @ExceptionHandler with @ControllerAdvice
  
  <img width="784" alt="Screenshot 2024-06-20 at 7 06 35 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f36b169a-e56c-4d64-bb93-853899da7922">

  Consider a class. Notice that it doesn't have @Component annotation.

  <img width="645" alt="Screenshot 2024-06-20 at 7 10 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/12d009c0-bae7-45b5-b0ce-0de6eecf2a36">

  If any exception occurs, we can let Spring handle it by creating different methods and annotating it with @ExceptionHandler.

  <img width="685" alt="Screenshot 2024-06-20 at 7 15 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d065d217-9b88-4996-8c37-c6c3a092746a">

  Suppose whenever an exception occurs, we display a jsp page which shows the error

  <img width="660" alt="Screenshot 2024-06-20 at 7 15 36 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f568ca3c-b25c-4647-b992-9353d244c439">
  <img width="680" alt="Screenshot 2024-06-20 at 7 17 49 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a2a38812-6788-4491-a880-21eb9cd8e733">

  #### *But does that mean for every Controllers, we would require such methods to handle exceptions?*

  No. We can globalize it using **ControllerAdvice**.

  <img width="1053" alt="Screenshot 2024-06-20 at 7 26 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a17ce571-0320-4862-9cc9-93a6c9fb0fae">
  <img width="573" alt="Screenshot 2024-06-20 at 7 29 25 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/70c0f60a-5a0c-4ef6-a6ad-3961e431197f">
  <img width="409" alt="Screenshot 2024-06-20 at 7 31 13 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/08694ccb-8fdf-4710-b81f-c21ac2b37c71">

* ### ExceptionHandler, ModelAttribute, InitBinder with @ControllerAdvice

  <img width="1019" alt="Screenshot 2024-06-20 at 7 02 03 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b461fb6e-94d9-4ff5-8a07-67884db898b6">
  <img width="679" alt="Screenshot 2024-06-20 at 7 34 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d6055fb4-c2f6-4374-822b-eb54df7a3389">
  <img width="712" alt="Screenshot 2024-06-20 at 7 31 41 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b3750451-be07-4b7a-abc1-81210c0f31a3">
