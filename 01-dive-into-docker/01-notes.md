Redis - in-memory data structure store used as a distributed, in-memory key-value database 

### DOCKER

Image - a single file with all the deps and config required to run a program
Container is an instance of an image, runs a program

Docker CLI - tool that issues comans to Docker Server 
Docker Server - tool responsible for creating images, running conttainers, etc. 
Docker client (Docker CLI) interacts with Docker Server 


### Using the Docker client 
the first time you try to run an open container (e.g `docker run hello-world`) from dockerhub docker server will check the container cache and if it can't ffind it there, then it will look for the name/tag on docker hub and if it finds it there, it will download it. 


### What is a container? 
every computer contains a kernel that communicates between software and hard doisk, memory and CPU. If you want to save a NodeJS file, NodeJS will communicate that to the kernel and it then will save it to tthe arddrive. 

**namespacing** - isolating resources per process or group of processes (network, processes, harddrive, users, hostnames, etc.))
**control groups** - limit **amount** of resources used oer process (CPU usage, memory, network bandwith, etc.))

image - file system snapshot and startup command
in a container  