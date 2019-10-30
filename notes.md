# General Docker Notes

## Check the docker daemon is running ##
service dockerd status

## Check docker containers ##
*Either option will work
	docker ps
	docker container ls
```
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
```
docker ps -a
### Formatting the docker ps output ###
docker ps --format="ID\t{{.ID}}\nNAME\t{{.Names}}"


## pull image ##
/* kind of like a git clone */

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

docker stop [CONTAINER-ID]

	CONTAINER_ID = can be found with "docker ps"
	
docker stop [CONTAINER-NAME]

        CONTAINER_NAME = can be found with "docker ps"

### Exposing ports with docker ###

docker run -d -p 8080:80 nginx:latest
	-p = port number > map port 8080 to port 80
docker run -d -p 8080:80 -p 3000:80 nginx:latest
	* Multiple ports can be mapped simultaneously

## removing a container ##

docker rm [CONTAINER-ID]  ==> removes one container
docker rm $(docker ps -aq) ==> removes all containers
	* Containers can only be removed if they are stopped
	* -f will forcefully remove the containers

## naming the containers ##

docker run --name website -d -p 8080:80 -p 3000:80 nginx:latest


## Formating output of docker ps ##

export myFormat="ID\t{{.ID}} \nNAME\t{{.Names}} \nIMAGE\t{{.Image}} \nPORTS\t{{.Ports}} \nCOMMAND\t{{.Command}} \nCREATED\t{{.CreatedAt}} \nSTATUS\t{{.Status}}\n"
docker ps --format="${myFormat}"

## VOLUMES ##
Allows for the sharing of data(Files and Folders)
	* Between host and container
	* Between multiple containers
	
The standard syntax is:
	docker run --name some-container -v [/host/mount/point]:[/container/file/system]:[permisions(ro,rw,etc)] -d [container]
	docker run --name nginxWithFS -v /home/dasaed/github/DockerCrashCourse/dockerfs:/usr/share/nginx/html:ro -d nginx:latest

permisions
	* ro = read only
	* [blank i.e. don't put anything] read and write

### Sharing volumes between dockers(containers) ###
docker run --name website-copy -d -p 8081:80 --volumes-from website nginx:latest
	
## run a bash terminal from within the docker ##

docker exec -it website bash


