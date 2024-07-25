# **Docker Basic Commands**

<img width="602" alt="Screenshot 2024-06-04 at 1 27 29 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6954e830-1052-40e1-a911-876ac06b7e30">
<img width="1136" alt="Screenshot 2024-06-04 at 1 29 27 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/09003184-f564-4046-8a1b-c8e61ea7e15e">

Tag is basically the version of the Image.

<img width="1122" alt="Screenshot 2024-06-04 at 1 29 59 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5171a70b-ca54-4b42-98b7-40465de3ac28">
<img width="766" alt="Screenshot 2024-06-04 at 1 31 27 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6c1f96f5-546f-4678-b534-29638e7f6008">

- *docker pull \<image-name\>* : to pull an image
- *docker images* : to check all the existing images
- *docker run \<image-name\>* : To create Container of the Image to make it possible to connect to the application. This will run and start the new Container. If the image is not fetched intially,
  it will pull the Image and then start Container.
- *docker ps* : To see list of running Containers
- *docker stop \<container-id\>* : To stop the Container
- *docker start \<container-id\>* : To restart a Container
- *docker ps -a* : Lists running and stopped Containers

When containers with more than one versions are run, the ports specify on which port the container is listening to the incoming requests. If we see, both containers openend the same port.
**How to not have conflict on such case?**

We need to create Binding between a port that our laptop/host machine has & the container. We need to bind them to two different ports in the host machine. The host would know how to forward
the request using Port Binding.

<img width="1143" alt="Screenshot 2024-06-04 at 2 54 45 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3b60f6e5-0ec0-47b3-ac08-363f8f01cc7c">
<img width="1135" alt="Screenshot 2024-06-04 at 2 59 53 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/31bcb404-99fe-4c3c-bd73-a210cf074b54">
<img width="1131" alt="Screenshot 2024-06-04 at 3 01 11 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3e6b7aa8-f27b-4097-a4ea-537e9e03f6fe">

**How to Bind?**

We need to specify binding of the port during run command.
- *docker run -p\<host-port\> \<container-port\>*

  <img width="1084" alt="Screenshot 2024-06-04 at 3 07 51 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f6932ddc-43b4-422e-b31a-99c3acbb84c8">
  <img width="1132" alt="Screenshot 2024-06-04 at 3 08 26 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/695d69cb-a8e8-4d0b-85eb-0644b8b39919">

  If we now try to bind same port to another container, it shows error

  <img width="1150" alt="Screenshot 2024-06-04 at 3 09 51 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0d0336e6-25f6-45bf-b88d-7ade82001376">

  If we bind to another port, it works fine.

  <img width="1198" alt="Screenshot 2024-06-04 at 3 11 26 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/48de9ef1-5a6a-4ae9-b6f2-4b62a9e9ea89">

# **Debugging Containers**

  - *docker logs \<container-id\>* : To see logs associated to a Container.
    Alternative: *docker logs \<container-name\>*

    <img width="1139" alt="Screenshot 2024-06-04 at 3 16 22 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/be336690-f158-4e88-9883-b94e624d6d80">

    Create a new container while naming the container as per our choice.
    *docker run -d -p6001:6379 --name \<container-name\> redis:4.0*

    <img width="1146" alt="Screenshot 2024-06-04 at 3 19 48 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/4eeab815-20e0-4412-bdc7-ef695d0c6293">

  - *docker exec -it \<container-id\> /bin/bash* : (it-interactive) Get the Terminal of the running Container.
    We can navigate differenet directories, check file etc.

    <img width="1140" alt="Screenshot 2024-06-04 at 3 23 19 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/218a3859-80d1-4b6a-84eb-71adf1d4bae5">

    We can do it using name as well instead of container-id.

    <img width="895" alt="Screenshot 2024-06-04 at 3 24 21 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e2ae8c53-1bae-45c7-92ad-5d8f91fb2cf4">

# **docker run VS docker start**
  - *docker run* : This is where we create a new container from an image. It will take an image with specific version or latest.
  - *docker start* : This doesn't work with Images but with Containers. Once the container is created and we wnat to restart post stopping the container, we can use *docker start*.
    When we start it, the Containers retain all the attributes that we defined while creating the Container using docker run.
    So docker-run is to create a new Container and docker-start is to restart a stopped Container.

<img width="1137" alt="Screenshot 2024-06-04 at 3 33 23 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/527f7a52-13e2-4c4c-8dad-224874191232">


