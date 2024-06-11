#### 1) To push an existing repository from the command line

- *git remote add origin \<git-url\>*

  <img width="1056" alt="Screenshot 2024-06-11 at 8 53 17 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/7b05dda4-901f-4777-a0dd-b93f36821eab">

  By convention, all the repositories and folders that are in our personal account have a name called **"origin"**

  **Note:** Make sure to initialize the repository before trying this - *git init*

#### 2) To displays a list of all the remote repositories that are currently configured in Git

- Command - *git remote -v*

  When we run this command, we'll see a list of remote names and their corresponding URLs. This can help us manage multiple remote repositories, track changes made by other developers,
  and collaborate with others in a distributed development environment.

  <img width="837" alt="Screenshot 2024-06-11 at 9 00 40 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/89a9d183-01c3-4b25-b9ce-e44c8c311d17">

#### 3) Push changes to url

- *git push \<url\> \<branch-name\>*

  Ex: **git push origin master**

  Repository updated

  <img width="926" alt="Screenshot 2024-06-11 at 9 22 25 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/bd684b7f-313d-4970-94b5-c265fa676599">

#### 4) To create a new branch

- *git branch \<branch-name\>*

#### 5) To checkout a branch

- *git checkout \<branch-name\>*

*Note:* Head is a pointer that says all the new commits that'll be made will be added on the head.

## Fork
#### 6) Upstream

By convention, upstream url is the one from where we have forked a project.

*git remote add upstream \<url\>*

#### 7) How to keep your forked main branch updated?

- We can use github "fetch upstream" button
- Using command line
  - Fetch all the commit from main branch: *git fetch --all --prune*
  - Checkout main: *git checkout main*
  - Reset main branch of our origin to main branch of upstream: *git reset --hard upstream/main*
  - Check commits: *git log*
  - Push changes to origin: *git push origin main*

  OR

  - We can also do *git pull upstream main*
  - Push the changes: *git push origin main*

## TRY IT OUT - Visualize git branching

https://learngitbranching.js.org/

