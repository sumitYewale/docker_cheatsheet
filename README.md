# docker_cheatsheet
Docker Commands

Images are running in container, so container is running environment of image.

-it => Interactive Terminal
-e => used to define environmental variables in commands

1. docker images => to get all images of current installed on locally
2. docker ps => to list all docker running processes => this will provide following information
container_id name command created_at status port names

3. docker run <image_name> => To run a perticular image on docker, create new container for image
4. docker run -d <image_name> => to run image in ditached mode (It will run your process at backgroun countinously)
5. docker start <container_id> => to start container
6. docker stop <container_id> => to stop container
7. docker ps -a => get running history of docker
8. docker run <image_name>:<version> => it will pull perticular version image in start to process (Combination of command docker pull and docker start)
9. docker run -p<host_port>:<container_port> <image_name> => it will bind specific host port to container port
1o. docker pull => pull image from docker hub to local
11. docker images => give all images installed locally
12. docker run --name <new_name> <image_name> => to changae the container name (Can't use (-) in New name)

DOCKER LOGGING
1. docker log <container_id>
or
1. docker logs <container_name> => to get log of container
2. docker exec -it <container_id> <shell> (Ex. shell => /bin/bash, /bin/sh, /bin/ksh(Korn Shell), /bin/csh/(C shell)) => This will give you a  

DOCKER NETWORKS
1. docker network ls => list all network of docker
2. docker network create <network_name> => it will create new network in docker
3. docker run --net <network_name> => it will add container in specific network 

DOCKER COMPOSE
If want to run multiple docker containers then we can define them in compose file.
File name will be: <file_name>.yaml

Syntax:
version:3
services:
	service1
		image: <docker_image_name>
		ports:
			<port_numbers> host:container
		envirnoment:
			<all_environment_variables>
			
	service2
		image: <docker_image_name>
		ports:
			<port_numbers> host:container
		envirnoment:
			<all_environment_variables>

*To run both containers we used <file_name>.yaml file
	docker-composer -f <file_name>.yaml up -d
	This will start the container with the specific network

*To stop both containers we used <file_name>.yaml file
	docker-compose -f <file_name>.yaml down
	This will stop container and it will remove the default created network also.

WORKFLOW OF DOCKER

Your code 
	||
	\/
Commit in VERSION CONTROL TOOL
	||
	\/
Jenkins(Tool) will create a docker image and push it to private docker hub
	||
	\/
On server we can pull image

Docker file is blueprint of any docker images.

Some syntax of docker file
FROM <service_name(Ex. node, redis)>:<version>
ENV
	ENV1=ENV_VALUE1
	ENV2=ENV_VALUE2
RUN mkdir -p /<path_to_directory>/
COPY ./<path_to_directory>/
ENTRYPOINT ["<any_file_name_to_execute>"]
CMD["",""]
save as => Dockerfile

CREATE DOCKER IMAGE
docker build -t <image_name>:<version> => (If we want to define custom name for docker image then "-t" option should used)
Docker Image should be always Ex. "imageName" format
run docker build in same folder where "Dockerfile" is present
It will run "Dockerfile" and build docker image.

DELETE CONTAINER
docker rm <container_name> or <container_id>

DELETE IMAGES
docker rmi <image_id> => always stop container, then remove container, then remove docker image


DOCKER PUSH
first tag the image
	docker tag <image_name>:<tag_or_version> <image_rename_name>

then push the docker image
	docker push <image_name>

DOCKER PERSISTANCE DATA
	In terms of persistance data of container specified volume path of host or local machine in <file_name>.yaml file
