#### 1) How to squash commits into one single commit?

  - If there are 5 commits and we want the first 4 commits to be squashed, we can reset till the 5th commit with 5th commit's sha. The first 4 commits then goes to the unstaged area and we can
    add a new single commit which will be for changes related to all 4 commits thus bringing them back to the staged area.

  - Same can be done using *REBASE*. We can copy the 5th commit's sha and enter command, *git rebase -i <sha\>* where "i" means interactive.

    <img width="580" alt="Screenshot 2024-06-11 at 1 09 21 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/883410e5-fc05-4045-ac77-a964107247af">

    We can either pick or squash the above commits.

    <img width="582" alt="Screenshot 2024-06-11 at 1 09 50 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/22a49d62-5815-43a3-bec3-93c5fd3b7acf">

    We can select squash for all

    <img width="576" alt="Screenshot 2024-06-11 at 1 10 44 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ed8ab103-714f-4642-9108-d31c6b246deb">

    OR

    if we want to squash certain commits while keeping others, we can use "s" for squash and "p" for pick

    <img width="572" alt="Screenshot 2024-06-12 at 10 13 37 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ff8c6d9d-f769-4c08-ac1c-5073a9a1173d">

    **To exit:** esc + ":" + "x"

    Add a commit message,

    <img width="590" alt="Screenshot 2024-06-12 at 10 15 10 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fc728040-6db4-4e1d-8130-88388608d23c">

#### 2) Merge conflict

 Merge conflict occurs when two or mpeople try to edit the same file or section of code simultaneously, causing changes to clash and become difficult to resolve. This can happen in collaborative coding environments or when working on the same project with multiple developers. To resolve merge conflicts, you typically need to identify the conflicting changes, determine which changes should be kept, and manually merge the changes together. It's important to communicate with other developers to ensure that everyone is on the same page and that the final version of the code reflects the intended changes.  


### Notes

https://github.com/kunal-kushwaha/DSA-Bootcamp-Java/tree/main/lectures/01-git

