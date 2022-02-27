# Dockerise-Python-HelloWorld
Testing (Dockerfile, Composer) with a simple python app

# Installation de Docker
  -Windows 10 pro : https://docs.docker.com/docker-for-windows/install/
  
  -Windows 7,8 ,8.1 : https://docs.docker.com/toolbox/overview/
  
  -Mac: https://docs.docker.com/docker-for-mac/
  
# Define a container wirh Dockerfile 

copy paste in a notepad file and save it named Dockerfile (as all files)

# Build The image from Dockerfile

Make sure you are still at the top level of your new directory. Here’s what ls should show:
```
$ ls
Dockerfile		app.py			requirements.txt
```
build the image with friendly name using -t :
```
docker build -t friendlyhello .
```
# Run the app
mapping your machine’s port 4000 to the container’s published port 80 using -p:
```
docker run -p 4000:80 friendlyhello
```
# Testing
```
docker-ip machine -->your IP Machine 
```
making the correct URL http://your_IP_Machine:4000

# Share your image
Log in with your Docker ID
If you don’t have a Docker account, sign up for one at cloud.docker.com. Make note of your username.

Log in to the Docker public registry on your local machine.
```
$ docker login
```
associating a local image with a repository on a registry
```
docker tag friendlyhello john/get-started:part2
```
-The tag is optional, but recommended, since it is the mechanism that registries use to give Docker images a version. Give the repository and tag meaningful names for the context, such as get-started:part2. This puts the image in the get-started repository and tag it as part2.
-get-started is your repo in the registry
-friendlyhello your local image

# Publish the image
```
docker push username/repository:tag
```
for example :
username used in login
repository :get-started
tag :part2
# Pull and run the image from the remote repository
From now on, you can use docker run and run your app on any machine with this command:
```
docker run -p 4000:80 username/repository:tag
```
# Your first docker-compose.yml file

-In a distributed application, different pieces of the app are called “services.” For example, if you imagine a video sharing site, it probably includes a service for storing application data in a database, a service for video transcoding in the background after a user uploads something, a service for the front-end, and so on.

-Services are really just “containers in production.” A service only runs one image, but it codifies the way that image runs—what ports it should use, how many replicas of the container should run so the service has the capacity it needs, and so on. Scaling a service changes the number of container instances running that piece of software, assigning more computing resources to the service in the process.

-Luckily it’s very easy to define, run, and scale services with the Docker platform – just write a docker-compose.yml file.
Save this file as docker-compose.yml wherever you want. Be sure you have pushed the image you created in Part 2 to a registry, and update this .yml by replacing username/repo:tag with your image details.
# Let practice a 3chiri !
Your first docker-compose.yml file

-A docker-compose.yml file is a YAML file that defines how Docker containers should behave in production.

-Save this file as docker-compose.yml wherever you want. Be sure you have pushed the image you created a registry, and update this .yml by replacing username/repo:tag with your image details.

-This docker-compose.yml file tells Docker to do the following:

-Pull the image we uploaded in step 2 from the registry.

-Run 5 instances of that image as a service called web, limiting each one to use, at most, 10% of the CPU (across all cores), and 50MB of RAM.

-Immediately restart containers if one fails.

-Map port 80 on the host to web’s port 80.

-Instruct web’s containers to share port 80 via a load-balanced network called webnet. (Internally, the containers themselves publish to web’s port 80 at an ephemeral port.)

-Define the webnet network with the default settings (which is a load-balanced overlay network).

-Run your service (service = container in prod )
```
docker swarm init

docker stack deploy -c docker-compose.yml getstartedlab
```
-Note :We get into the meaning of that command in part 4. If you don’t run docker swarm init you get an error that “this node is not a swarm manager.”

-hadchi because we are in the cloud otherwise we can run without swarm if we use our local image in the docker-compose.yml file

# The End
```
docker stack ls                                            # List stacks or apps
docker stack deploy -c <composefile> <appname>  # Run the specified Compose file
docker service ls                 # List running services associated with an app
docker service ps <service>                  # List tasks associated with an app
docker inspect <task or container>                   # Inspect task or container
docker container ls -q                                      # List container IDs
docker stack rm <appname>                             # Tear down an application
docker swarm leave --force      # Take down a single node swarm from the manager

How to stop remove containers
docker stop  XXXX
docker rm XXXX
How to remove image
docker rmi ImageID
remove all images 
docker rmi $(docker images -a -q)

```


