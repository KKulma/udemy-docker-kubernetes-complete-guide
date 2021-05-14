Points covered in the chapter:
- assumptions about pre-existing dependencies in the base image 
- choosing the right base image for your needs
- copying files over from the host to the container  
` COPY ./ ./`
- opening up the right port in the container so that it can communicate with the host's browser 
`docker run -p 8080:8080 <>image id>` 
  - first 8080: route incoming requests to this port on local host to...
  - second 8080: ... this port inside the container 
`PORT 80` 
- specifying the working directory so that any following commands will be executed relative to this path in the container 
`WORKDIR /usr/app`
- running another process in the currently running container, e.g. run the app then open another terminal window and run `docker exec -it <image id> sh`
- if we make changes to local files, we need to rebuild the whole image to make sure they are reflected in the container
- unnecessary rebuilds if, e.g. if we change a file that will be copied over, the following installation of npm will rerun, too  

# Minimizing cache busting and rebuilds
