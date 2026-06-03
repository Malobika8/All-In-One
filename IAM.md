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

