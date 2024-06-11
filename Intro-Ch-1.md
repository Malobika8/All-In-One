General commands we should be aware of:
- touch: create a file
- mkdir: created a folder
- cd: change directory
- ls: list files
- ls -a: list hidden files
- cat \<file-name\>: displays whatever is available in the file
- rm -fr \<file-name\>: delete a file

# Git and Github

Git and Github allows us to maintain history(which person made what change and when) of the project. It lets us share our code with people.
Github is a platform, an online website, that allows us to host our git repositories. Repository is basically a folder where all the changes are saved.
Butbucket, Gitlab are among other platforms that allow us to do the same.

- When using git for the first time, set the global configs using the commands:
  * *$ git config --global user.name "your_name"*
  * *$ git config --global user.email your_email*
 
- Download Git: https://git-scm.com/downloads
- To check if git is installed: Open terminal and enter *git*

The histories(creation,deletion,updation of a repo) are stored in a folder that git provides us. This is known as a git repository and it is named ".git". (.) folders are hidden folders.

#### Q. How do we get this folder where all the history is being saved?

- Do *git init*. It initializes an empty git project/repo.
- Since ".git" folder is hidden, "ls" won't show it.
- For it to be shown, enter ".ls". This will show ".git" folder.
- To see the contents, we can enter "ls .git".
- Post this, we will be able to maintain the history of the project. Any changes made in the project will be picked up by git.

#### Q. How do we see what all files that have been changed or modified?
- Command: *git status*

  <img width="511" alt="Screenshot 2024-06-10 at 10 59 17 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5c910e6a-d38d-41b2-9cbf-3b1ba5a9843e">

- Untracked files: Files that are there but not added.
  
  <img width="592" alt="Screenshot 2024-06-10 at 10 53 06 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/32add3dd-cd54-4ae1-915c-459d5b1be2a0">

#### Q. How to save/add in git repo?
- Command: *git add .* ("." means add everything in the current directory)
- Command: *git add \<file-name\>* (to add a specific file in the directory)

  <img width="564" alt="Screenshot 2024-06-10 at 10 54 53 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cf2ce3d6-352b-4b64-9126-5714de4853b0">

Once the file has been added, we need to commit with a message.

- Command: *git commit -m \<file-name\>*

  <img width="588" alt="Screenshot 2024-06-10 at 10 55 46 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/44d815ad-e288-4feb-ad35-c32d736ef315">
  
- Check what has been modified

  <img width="580" alt="Screenshot 2024-06-10 at 11 23 54 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2ba87ed9-eb11-4874-95dc-1705cce6e17c">

- Post commit, the file can be considered to have been staged.

#### Q. How to unstage file or changes that we mistakenly added?
- *git restore --staged \<file-name\>*

  <img width="584" alt="Screenshot 2024-06-10 at 11 28 32 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3176aeac-f1ed-4ed5-b204-fd0fd56549d9">

#### Q. How to see entire history of the project? All commits and files updated/modified

- *git log*

  <img width="509" alt="Screenshot 2024-06-10 at 11 30 14 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c7d531d7-01cb-4f5e-8bb7-438a435b069e">

#### Q. How to delete a file and check log

<img width="581" alt="Screenshot 2024-06-10 at 11 36 05 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8bec1f25-6738-4a6e-a0d0-74bd406827a2">

#### Q. How do we go back to a particular state? Say we deleted a file by mistake or we dont want changes related to certain commits.

- We can unstage commits
- Do "git log" and copy the commit sha till which we want the changes
- Reset it. Command: *git reset \<commit-sha\>

  <img width="587" alt="Screenshot 2024-06-10 at 11 40 47 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/82288c0d-2de0-43a8-bfd2-e169a6d1dd63">

- Post this, all other files become unstaged

  <img width="579" alt="Screenshot 2024-06-10 at 11 42 18 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/420cb623-5871-4963-8b5b-dc756ed54162">

#### Q. What if we don't want to commit updated changes but want to keep it somewhere so that later we can revisit it? We don't want to lose these changes.

- We can send the files to stash area
- The stages files can be stashed
- Command: *git stash*

  <img width="600" alt="Screenshot 2024-06-10 at 11 47 18 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ced73b66-861b-48a2-8f07-533290fffebf">

#### Q. How do we bring back the changes from stash area?

- Command: *git stash pop*

  <img width="595" alt="Screenshot 2024-06-10 at 11 49 55 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6649b3e0-5f2d-4624-91c5-c8bc6301b278">

#### Q. What if we don't want the changes present in stash area?

- Command: *git stash clear*

  <img width="592" alt="Screenshot 2024-06-10 at 11 51 34 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6cefa8ff-dbfd-4731-92be-b29cdc201924">

