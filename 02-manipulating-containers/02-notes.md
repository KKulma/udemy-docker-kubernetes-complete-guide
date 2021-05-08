### STarting with Shell

`docker run -it busybox sh` # run shell in the container but you can't run any other process (than shell) on it

`docker exec -it busybox ls` will run the shell command in the container, you can run otther processes at the same time

### Container isolation
if we run two same containers they are perfectly isolated from each other (with no data sharing between each other)