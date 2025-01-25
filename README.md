1.	 Here we are seeing the contents of the index.html and dockerfile. The index.html file will print the line in between header.
Dockerfile has base image of ubuntu16.04. We have all the commands in this file. We will add index.html to the container which is inside directory /var/www/html/. We will expose to the port 80. We will set the entry point which will start the apache server. The dockerfile will act as the configuration file to build the image.
 
2.	 We will build the image now.
 
 
3.	 The list of all docker images. Ubuntu 16.04 is the base image and on top of it we will build webserver latest.
 
4.	 We have add new docker image which is alpine with latest tag.
 
5.	The 8080 is the port of the host and 80 is the port of the container. The port 8080 is mapped to the port 80 of the container. So we can access the website using the port which is mapped to the port of the host. From webserver image, the container will start. The output shows that the container has started.
 

6.	 The container has started and we can access the webpage we created.
      
7.	  We can also start the container from alpine image.
 
8.	 This command shows all the containers running in the system.
 
9.	We can get an interactive shell in the container. Here we are running the command sh in the container id cbda78302563. Thus, getting the root shell.
 

10.	  We are starting a new container with name “newone” which will be interactive terminal and will run in backend.
 
11.	  Here, we are running the command sh in the container named “newone”.
 
12.	 We can run the command using 1st four digits of container id.
 
13.	 We are stopping all docker images.
 
14.	 Now will remove all docker images.
 
 
15.	 This command gives all information of the docker.
 
16.	  Now if we go to the root directory and navigate through it, we get this output. And in the l directory, it does not contain anything for now.
 
17.	 We are again building the webserver image .
 
 
18.	 The root directory contains all the storage filesystem for Docker. Now if we again navigate through the l directory in overlay2 directory, we can see new layers are created when building the image.
 



19.	It shows how cgroup limits the access of containers to system resources. If someone compromise the container, he can exhaust the resources of the host.
 
20.	Here it shows how cgroup limit the pids to 6 from 12965 to prevent fork bombs.
 
Docker security and vulnerability:
21.	 Trying to exploit vulnerable image 


22.	 Getting into the reverse shell by listening to port 4444.
 


23.	 Privilege escalation by volume mounting. The elevated privilege of user to root level

 

Countermeasures for attack on docker image:
24.	Automated assessment -Trivy:
It does static analysis against vulnerable image.
docker run --rm -v $(pwd):/root/.cache/ aquasec/trivy image getcapsule8/shellshock:test
 

25.	 Starting the container vulnerable
 



26.	  By running docker bench, the score is 18.
 
27.	  If we made some modifications during starting the container.
 

28.	After, we again run the docker bench, the score increases.
 
  
29.	 If we start a new acontainer named vulnerable2 without any uid and gid, this gives us root shell access. 

30.	Whereas vulnerable container with specified uid and gid, does not give us root shell access. Which prevents attacker from getting root access by exploiting vuknerability of images. And docker bench helps by warning this flags.

 



