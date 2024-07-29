# Creating and Scheduling Alerts

We cannot check Splunk every day to know if there is any high-priority issue. We can set some Alerts that can notify us about the same.
We need to provide certain criteria based on which alerts can be notified. When the condition is satisfied, the alert is auto-triggered.

When the Job status fails, it should alert.

<img width="690" alt="Screenshot 2024-07-29 at 12 56 23 PM" src="https://github.com/user-attachments/assets/45c0a9e6-b0d7-4486-9c29-d525af2c63b8">
<img width="948" alt="Screenshot 2024-07-29 at 12 57 42 PM" src="https://github.com/user-attachments/assets/f7f1d5b4-e58c-4905-ace4-3f2ea64d0908">

Let's set our conditions.

#### Condition: If the fail count is 3 in 2 mins then it should trigger the alert.

## How to set alerts?

Let's see how to trigger alerts over email.

- Go to "Settings" -> "Server settings" (for email configuration, we need to go to "Server Settings")

  <img width="503" alt="Screenshot 2024-07-29 at 1 00 06 PM" src="https://github.com/user-attachments/assets/408466c6-279e-4aef-b3fa-56a1f65835f2">

- Go to "Email settings"

  <img width="807" alt="Screenshot 2024-07-29 at 1 01 33 PM" src="https://github.com/user-attachments/assets/ca721e4b-22c0-44a5-8db3-b3f7c8183645">

- Enter necessary details.

  <img width="593" alt="Screenshot 2024-07-29 at 1 02 33 PM" src="https://github.com/user-attachments/assets/aa173666-ae54-4fe9-a946-de75075b8268">
  <img width="587" alt="Screenshot 2024-07-29 at 1 03 02 PM" src="https://github.com/user-attachments/assets/54af6c02-4bb1-498c-99f9-880a23abe27e">

- Go to "Splunk Enterprise" -> "Search & Reporting"
- Set the condition for Alert. Search with **FAILED** status & select "Save As".

  <img width="1132" alt="Screenshot 2024-07-29 at 1 05 25 PM" src="https://github.com/user-attachments/assets/5cbe2a2f-467a-4281-bee9-07a3eb7aa46c">

  Click on "Alert".

  <img width="437" alt="Screenshot 2024-07-29 at 1 06 20 PM" src="https://github.com/user-attachments/assets/bef1b3c9-8fd7-488a-ad64-056dd4ab4116">

  Add necessary details.

  <img width="894" alt="Screenshot 2024-07-29 at 1 08 45 PM" src="https://github.com/user-attachments/assets/beca9c5c-debf-42e8-9b9c-3f9cb5a15965">
  <img width="482" alt="Screenshot 2024-07-29 at 1 08 58 PM" src="https://github.com/user-attachments/assets/eb5f5aa9-dea5-41d4-9800-24e518bd6feb">
  <img width="478" alt="Screenshot 2024-07-29 at 1 09 27 PM" src="https://github.com/user-attachments/assets/a5044d2d-8811-4fef-9e16-1352672cc011">
  <img width="465" alt="Screenshot 2024-07-29 at 1 09 44 PM" src="https://github.com/user-attachments/assets/f5118731-045f-47b3-9a7a-16bc59eefe6c">
  <img width="479" alt="Screenshot 2024-07-29 at 1 10 06 PM" src="https://github.com/user-attachments/assets/53824560-1fb5-4d08-bf64-563f54bafa07">
  <img width="483" alt="Screenshot 2024-07-29 at 1 10 28 PM" src="https://github.com/user-attachments/assets/9b12ee3e-98a0-4310-9fcb-ca055512ce31">
  <img width="481" alt="Screenshot 2024-07-29 at 1 11 03 PM" src="https://github.com/user-attachments/assets/78e7370e-0b22-4be7-b29e-0acf9297e6b6">

  Alert created.

  <img width="950" alt="Screenshot 2024-07-29 at 1 14 01 PM" src="https://github.com/user-attachments/assets/75332cd8-cd89-4792-8c93-3263926ce452">
  <img width="542" alt="Screenshot 2024-07-29 at 1 14 28 PM" src="https://github.com/user-attachments/assets/d65df0e1-1709-4979-895c-b141977828b6">
  <img width="1128" alt="Screenshot 2024-07-29 at 1 14 50 PM" src="https://github.com/user-attachments/assets/d694922b-e51b-451f-afb4-6e9f1187d8ec">

## Let's verify

<img width="1136" alt="Screenshot 2024-07-29 at 1 16 00 PM" src="https://github.com/user-attachments/assets/990010db-ab01-4409-8073-f8e004a22f7a">

Go to the Alert & select "Open in Search"

<img width="1112" alt="Screenshot 2024-07-29 at 1 16 18 PM" src="https://github.com/user-attachments/assets/a4977ca6-a354-465d-aedb-736198998c76">

Since it failed more than 3 times within 2 minutes, it should ideally send an Alert as per our condition.

<img width="1125" alt="Screenshot 2024-07-29 at 1 17 10 PM" src="https://github.com/user-attachments/assets/a950645e-0946-4293-b229-76f32cf7a185">

Check email for Alerts.

<img width="964" alt="Screenshot 2024-07-29 at 1 18 13 PM" src="https://github.com/user-attachments/assets/59ad204f-99be-4aa1-bebb-3287deab02a6">



