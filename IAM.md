## Intro

- IAM as an entire service is a global service
- Select "create user"
  - Select create an IAM user
  - Custom password or User must create a password at the next sign in
  - Add permission (create groups)
- To simplify sign in, we can use a sign in alias. We can use account alias for sign in instead of account id
- There are two accounts to log in: root user & IAM user
- Should always log in as IAM user
- There is multiple session support so we can have multiple sessions opened with different roles
  - From the dropdown, we can do "Add session"
  - We can login again using any accountId
 
<img width="814" height="390" alt="Screenshot 2026-06-03 at 8 15 58 AM" src="https://github.com/user-attachments/assets/ae2c4d21-1113-47bd-96ba-b3c9d29bef22" />
<img width="812" height="394" alt="Screenshot 2026-06-03 at 8 18 00 AM" src="https://github.com/user-attachments/assets/b561b453-cede-4cd4-80bd-4e745ee92fcb" />
<img width="823" height="405" alt="Screenshot 2026-06-03 at 8 19 01 AM" src="https://github.com/user-attachments/assets/964488bf-fc39-42c0-90f2-63dac863dd65" />
<img width="850" height="391" alt="Screenshot 2026-06-03 at 8 43 12 AM" src="https://github.com/user-attachments/assets/01953910-66de-46c6-8e5c-2e9904b109d3" />

## IAM Policies

- If attached at group level, the policies apply to all members
- It is also possible for a user to not at all belong to any group
- There is also inline policy that can only be attached to a user

## IAM Policy Structure

- Version
- Id
- Statement
  - Sid: an identifier for the statement
  - Effect: whether the statement allows or denies access
  - Principal
    - AWS: account/user/role to which this policy is allowed to 
  - Action: list of actions this policy allows or denies
  - Resource: list of resources to which the actions are applied
  - Condition (optional): condition to which the statement should apply or not

## Password policy

- default
- custom

## CloudShell
Only available for some regions

## IAM Roles

<img width="804" height="440" alt="Screenshot 2026-06-05 at 8 38 15 AM" src="https://github.com/user-attachments/assets/9dc253d3-7d3c-4ca8-96fc-2c716392a211" />

Role is a way to give AWS entities permissions to do stuff on AWS.

<img width="1059" height="501" alt="Screenshot 2026-06-05 at 8 43 29 AM" src="https://github.com/user-attachments/assets/dffda1a4-5ce9-4628-a41c-ceed13c5652b" />
<img width="1016" height="494" alt="Screenshot 2026-06-05 at 8 43 45 AM" src="https://github.com/user-attachments/assets/2b735924-d27e-4085-99fd-7f1b766c359c" />
<img width="1014" height="507" alt="Screenshot 2026-06-05 at 8 44 09 AM" src="https://github.com/user-attachments/assets/69d03777-d8e4-4717-b30d-90587bd1b312" />
<img width="815" height="442" alt="Screenshot 2026-06-05 at 8 44 51 AM" src="https://github.com/user-attachments/assets/8ba8603a-e3d2-45bd-8d08-2378a72b1ad1" />
<img width="1008" height="437" alt="Screenshot 2026-06-05 at 8 45 03 AM" src="https://github.com/user-attachments/assets/29263f2c-48bc-44d7-92e1-ee5b41cd4ceb" />
<img width="1020" height="502" alt="Screenshot 2026-06-05 at 8 45 15 AM" src="https://github.com/user-attachments/assets/109804fc-1f55-46b3-9f33-ad8e3e1641dd" />
<img width="829" height="458" alt="Screenshot 2026-06-05 at 8 45 41 AM" src="https://github.com/user-attachments/assets/33658fcc-f9a0-4d10-9f1c-30ec2726755d" />

## IAM Security tools

<img width="1037" height="550" alt="Screenshot 2026-06-05 at 8 52 18 AM" src="https://github.com/user-attachments/assets/fbb79d17-fe59-4e99-841c-ef6a469d2115" />
<img width="1076" height="550" alt="Screenshot 2026-06-05 at 8 55 36 AM" src="https://github.com/user-attachments/assets/eca8b47d-5694-4163-984a-e5f0b225d76f" />
<img width="1087" height="233" alt="Screenshot 2026-06-05 at 8 55 45 AM" src="https://github.com/user-attachments/assets/8685ce65-6de6-4a9b-8ef4-49d765c6814f" />
<img width="1076" height="540" alt="Screenshot 2026-06-05 at 8 58 06 AM" src="https://github.com/user-attachments/assets/64490caa-4e6c-42f2-b659-c6eb182ccf96" />
<img width="1069" height="508" alt="Screenshot 2026-06-05 at 8 58 12 AM" src="https://github.com/user-attachments/assets/570400fe-28bc-4129-bd0e-b6d46b40c13b" />

## Guidelines & best practices

<img width="1045" height="569" alt="Screenshot 2026-06-05 at 9 05 30 AM" src="https://github.com/user-attachments/assets/bf76803b-b7ca-4c0c-9141-6cd5c67230eb" />

## Shared responsibility model for IAM

<img width="1007" height="571" alt="Screenshot 2026-06-05 at 9 07 28 AM" src="https://github.com/user-attachments/assets/f9cc7c2a-9b57-48f9-bda5-8fd8b0810dca" />

## Summary

<img width="1035" height="532" alt="Screenshot 2026-06-05 at 9 08 59 AM" src="https://github.com/user-attachments/assets/25031b84-b58e-44db-8dd1-c6a97d719de0" />

