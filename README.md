# docker-tutorials

### Create a docker imges
### Docker provides a single command that will clean up any resources — images, containers, volumes, and networks — that are dangling (not tagged or associated with a container):

#### docker system prune
#### To additionally remove any stopped containers and all unused images (not just dangling images), add the -a flag to the command:
#### docker system prune -a

## Use the docker images command with the -a flag to locate the ID of the images you want to remove. This will show you every image, including intermediate image layers. When you’ve located the images you want to delete, you can pass their ID or tag to docker rmi:
##### docker images -a
#### docker rmi Image Image
### Remove dangling images
#### Docker images consist of multiple layers. Dangling images are layers that have no relationship to any tagged images. They no longer serve a purpose and consume disk space. They can be located by adding the filter flag -f with a value of dangling=true to the docker images command. When you’re sure you want to delete them, you can use the docker image prune command:
docker images -f dangling=true
docker image prune

### Removing images according to a pattern
You can find all the images that match a pattern using a combination of docker images and grep. Once you’re satisfied, you can delete them by using awk to pass the IDs to docker rmi. Note that these utilities are not supplied by Docker and are not necessarily available on all systems:

docker images -a |  grep "pattern"
docker images -a | grep "pattern" | awk '{print $3}' | xargs docker rmi
docker images -a
docker rmi $(docker images -a -q)

#### Removing Containers
Remove one or more specific containers
Use the docker ps command with the -a flag to locate the name or ID of the containers you want to remove:

docker ps -a
docker rm ID_or_Name ID_or_Name
docker run --rm image_name
### Remove all exited containers
You can locate containers using docker ps -a and filter them by their status: created, restarting, running, paused, or exited. To review the list of exited containers, use the -f flag to filter based on status. When you’ve verified you want to remove those containers, use -q to pass the IDs to the docker rm command:
docker ps -a -f status=exited
docker rm $(docker ps -a -f status=exited -q)
#### Stop and remove all containers
You can review the containers on your system with docker ps. Adding the -a flag will show all containers. When you’re sure you want to delete them, you can add the -q flag to supply the IDs to the docker stop and docker rm commands:
docker ps -a
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)

#### Removing Volumes
Remove one or more specific volumes - Docker 1.9 and later
Use the docker volume ls command to locate the volume name or names you wish to delete. Then you can remove one or more volumes with the docker volume rm command:

docker volume ls
docker volume rm volume_name volume_name

##### 
docker rm -v container_name



