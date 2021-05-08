### App overview
A web app displaying a number of visits so far to this website.
It needs two components: 
- a webserver (node app)
- redis server (in-memory data store to count the visits)

We could create redis server inside the node server but we will isolate them. 
We could put both components inside a single container but this would cause some performance issues when the website has high traffic. At the same time, we can't create multiple containers (with both, node and redis servers)) because then a different count would be available in each of them. 

SOLUTION: Multiple Docker containers for the node app connected to a single redis container 

### docker compose 
- separates CLI that gets installed along with Docker 
- is used to satrt up multipl docker containers at the same time 
- automates some of the long-winded arguments that we were passing to `docker run`

**docker-compose.yml**
redis-server - make it using the *redis* image
node-app - make it using the Dockerfile in the current directory and map it to port 8081

### docker-dompose commands 

docker --- docker-compose 

`docker run myimage` --- `docker-compose up`
`docker build . + docker run myimage` --- `docker-compose up --build`
`docker ps` --- `docker-compose ps` 

`docker-compose up` and `docker-compose up --build` commands always have to be run inside the directory with the docker-compose.yaml file tat we want ot run!!!

**Stopping containers**
`docker-compose up -d` -- start the containers in a detached mode (in the background)
`docker-compose down` - stop the containers

### Container maintanance with compose 
What to do when one of the containers crash? You create a restart policy inside docker-compose:
- "no" - never attempts to restart this contaienr (has to be added specifically in quotes as in yaml files no means False)
- always - if this container stops for any reason, always attempt to restart it
- on-failure  - only restart if the container stops with an error code
- unless-stopped - always restart unless we (developers) forcibly stop it


### container status with compose 