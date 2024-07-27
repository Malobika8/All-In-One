The pipeline that we will be building is as follows

<img width="1413" alt="Screenshot 2024-07-27 at 10 26 43 AM" src="https://github.com/user-attachments/assets/7eff8a60-11f7-4cb5-a141-5841af65f647">

When a user pushes something on GitHub, it automatically triggers the GitHub actions workflow. GitHub actions read the secret store. Post that, there are several steps that are run in 
order to build & publish our Application.

<img width="381" alt="Screenshot 2024-07-27 at 10 01 17 AM" src="https://github.com/user-attachments/assets/7b9c0d3e-ef35-4214-b416-4a5ed29961d2">

## What is a CI/CD Pipeline?

It is a "*Continuous Integration*" & "*Continuous Deployment*", also called a "Continuous Delivery Process" that automates building testing & deployment of Software Applications or Applications
in general. 

The term "*Continuous Integration*" refers to the process of regular merging of small code changes into a shared repository. Testing them and verifying that they can be
integrated with a larger code base. This ensures that any code changes do not break the existing code base & help maintain code quality. This ensures that our code change is safely 
integrated into the whole application's codebase.

"*Continuous Deployment*" or "*Continuous Delivery*" refers to the process of automating the release of Software Applications into Production, So, following successful testing, this process
includes creating builds, running automated tests, deploying the Application to the Staged environment & finally releasing the Application to the Production environment.
It means running, testing, packing, and then deploying to one or several environments.

CI/CI Pipeline combines these two processes providing an end-to-end automated workflow from code changes to production deployment. So, the pipeline includes multiple stages such as source
control, build, test, stage & then production. It automates each stage to reduce the possibility of Human Error.

It enables developers to build, test & deploy features at a faster pace and with confidence.
