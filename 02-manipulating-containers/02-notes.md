### Overriding Default commands

We can provide additional commands that will be run inside the runnign container, e.g. 
`docker run busybox ls` or `docker run busybox echo hi there` - they will work only if the container included relevant files to run them!

### Listing running containers
`docker ps` - shows all currently running containers
`docker ps -a` - shows all the containers ever created 


### Container lifecycle
What happens when you shut down a container? 

`docker build` creates an **image**
`docker run` creates a **container** and then starts it
`docker create <image name>` preps a container by copying over the system snapshot (files)
`docker start <container id>` executes a startup command

`docker run` = `docker create` + `docker start`

### Restaring stopped containers

`docker ps --all` will give you a list of all the containers - with their ids - including those that were stopped. To restart them, execute `docker start <container id>`

### Removing stopped cotainers

`docker system prune` will delete not only all stopped containers but also all build cache from docker hub (so you'll need to re-download them again in the future if you want to run them)

### Retrieving log outputs

`docker logs <comtainer id>` will print out docker container id with any additional commands that were used to run it, for exmaple:

`docker create busybox echo hi there`
`docker start <container id>`
`docker logs <container id>`
> id
> hi there

### Stopping containers 

`docker stop <container id>` - will stop the container while giving time to the running process to shut itself down. If it doesn't do it within 10 secs then Docker will automatically issue `docker kill` command on it
`docker kill <container id>` - will stop the container instantly

### Multi-command containers
 How to start a new image (container) inside an already running container? 

 `docker exec -it <container-id> <command>`

 `-it` allows us to provide input directly to the container

 ### The purpose ot the -it flag
 It can be used for running a shell in your container, for example  
 `docker exec -it <container id> sh` will run shell inside the container 
 `sh` coud be replced with any command processor, e.g. `bash`, `powershell`, `zsh`, `sh`


### Starting with Shell

`docker run -it busybox sh` # run shell in the container but you can't run any other process (than shell) on it

`docker exec -it busybox ls` will run the shell command in the container, you can run otther processes at the same time

### Container isolation
if we run two same containers they are perfectly isolated from each other (with no data sharing between each other)

