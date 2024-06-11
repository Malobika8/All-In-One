#### 1) Reset

  - If there are 5 commits and we want the first 4 commits to be squashed, we can reset till the 5th commit with 5th commit's sha. The first 4 commits then goes to the unstaged area and we can
    add a new single commit which will be for changes related to all 4 commits thus bringing them back to the staged area.

  - Same can be done using *REBASE*. We can copy the 5th commit's sha and enter command, *git rebase -i <sha\>* where i mean interactive.

    <img width="580" alt="Screenshot 2024-06-11 at 1 09 21 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/883410e5-fc05-4045-ac77-a964107247af">

    We can either pick or squash the above commits.

    <img width="582" alt="Screenshot 2024-06-11 at 1 09 50 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/22a49d62-5815-43a3-bec3-93c5fd3b7acf">

    We can select squash for all

    <img width="576" alt="Screenshot 2024-06-11 at 1 10 44 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ed8ab103-714f-4642-9108-d31c6b246deb">



#### 2) How to squash commits into one single commit?

  - 
