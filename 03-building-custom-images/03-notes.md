Dockerfile --> Docker CLI --> Docker Server --> Usable image

1. Specify a base image 
2. Runs some commands to install additional programs
3. Specify commands to run on container startup

### What's the base image?

base image specifies the operating system and the initial set of programs that we need in our image

### The built process in detail

For each step in a Dockerfile - except for setting the base image - a new temporary container based on the image from the previous step and the current command is run as a startup command. Once it's executed, Docker takes a snapshot of new container's file system and pastes it to the original container and deletes the temporary one. 

### Rebuilds with cache

Docker caches intermediate images and can use them in new builds where steps stayed the same and actually building only new steps. Pay attention to the sequence of steps as this may dramatically change how long it takes to re-build the image!

### Tagging an image

`docker build .` --> `docker run 5d9dac9ec44a038d79df4a24ed6e87f0a7fff0a4f9c71ecde5219f341fb276dd`

`docker build -t mytag .` --> `docker run mytag`

tags usually follow this convention:

Docker_ID/project_name:version (e.g. "latest")

### Manual image generation with Docker commit 
We can manually generate images from intermediate steps in the Dockerfile:

`docker run -it alpine sh` -- start shell in the base image
`apk add --update redis` -- run this command in container's shell
`docker ps` -- for fetching running container's ID
`docker commit -c 'CMD ["redis-server"]' containerID`-- pass the startup command to the container that is currently running

The output will be an id of the newly customized image