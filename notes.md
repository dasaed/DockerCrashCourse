 General Docker Notes

## Check the docker daemon is running ##
service dockerd status

## Check docker containers ##
*Either option will work
	docker ps
	docker container ls
'''
		docker ps --help
		Usage:	docker ps [OPTIONS]
		List containers
		Options:
		  -a, --all             Show all containers (default shows just running)
		  -f, --filter filter   Filter output based on conditions provided
		      --format string   Pretty-print containers using a Go template
		  -n, --last int        Show n last created containers (includes all states)
		                        (default -1)
		  -l, --latest          Show the latest created container (includes all states)
		      --no-trunc        Don't truncate output
		  -q, --quiet           Only display numeric IDs
		  -s, --size            Display total file sizes
'''
docker ps -a
### Formatting the docker ps output ###
docker ps --format="ID\t{{.ID}}\nNAME\t{{.Names}}"


## pull image ##

docker pull [image]
docker pull nginx

## list images ##

docker images

## Run an image ##

docker run [image]:[version]
docker run nginx:latest 
docker run -d nginx:latest
	-d = detached mode -> basically, in background

## Stopping a running Docker ##

docker stop [CONTAINER_ID]
	CONTAINER_ID = can be found with "docker ps"
docker stop [CONTAINER_NAME]
        CONTAINER_NAME = can be found with "docker ps"

### Exposing ports with docker ###

docker run -d -p 8080:80 nginx:latest
	-p = port number > map port 8080 to port 80
docker run -d -p 8080:80 -p 3000:80 nginx:latest
	* Multiple ports can be mapped simultaneously

## removing a container ##

docker rm CONTAINER_ID  ==> removes one container
docker rm $(docker ps -aq) ==> removes all containers
	* Containers can only be removed if they are stopped
	* -f will forcefully remove the containers

## naming the containers ##
docker run --name website -d -p 8080:80 -p 3000:80 nginx:latest
