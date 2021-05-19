### Development workflow 
Development --> Testing --> Deployment
### creating an app
- install node.js
- run `npx create-react-app frontend`

After you've created the npm project, enter it (`cd frontend`) and you can execute the following commands

`npm run start` - **development** environment only; starts a dev server
`npm run test` Runs tests associated with the project
`npm run build` - build a **production** version of the application 

### Creating a Dev Docker file 
A Dockerfile that will run our application in development `Dockerfile.dev` and then run 
`docker build -f Dockerfile.dev .`
`-f` specifies what file we're using as a Dockerfile

### Starting the container

`docker run -it -p 3000:3000 IMAGE_ID`

### Docker Volume

How to reflect newly added changes to the source code in the running container?

Container will create a reference mapping some files on our local disk, instead of taking a snapshot when building an image 

With Docker volumes, we set up a file placeholder of some sort in the container with references pointing to the local machine.

Why not always use volumes? Because setting them up can be a pain (from the Docker syntax point of view)

`docker run -it -p 3000:3000 -v /app/node_modules -v $(pwd):/app <image id>`

Break down:
- `-v /app/node_modules` - put a bookmark on the node_modules folder (creates a placeholder folder inside the container that is not mapped to anything on the host)
- `-v $(pwd):/app` - map the present working directory (`frontend` folder) into the `/app` folder inside the container

Now, any changes done on the local machine will be automatically reflected in the running container

### Docker compose
can be used to shorten and automate the docker run command that is run for our container  - see the file for an example 

### Executing tests 
we can execute npm tests by running `docker run -it <docker id> npm run test`
### Live updating tests
 
Two approaches: 
- setting up a new service and mounting additional volumes (see `docker-compose.yml` for details) - not ideal solution as it renders tests inside of the app session and we can't enter any standard input into he container

-  `docker attach`  - takes the command typed into the Terminal and attaches it onto one of the running containers, e.g. run the web and test containers and then in a separate terminal window type `docker attach <test container id>  but it's not going to work with docker-compose as the command is attached to the primary process that is un in the container (in our case is npm) but in reality we want ot attach it to the secondary process (e.g. start.js) 
 
### Need for nginx

We'll create a new Dockerfile that will setup a Production Web container (in dev environment we had a Development Web container that was based on the Dockerfile.dev) that will rely on the nginx engine to serve up the app files

### Multi-Step Docker Builds

We are going to have 2 blocks of configuration in the container 
- Build Phase: for the alpine base image, installing dependencies and running `npm run build` and
- Run Phase: for using nginx, copying over the result of `npm run build` and starting nginx. 


---------------
In the next lecture, we will be creating a multi-step build in our production Dockerfile. When we deploy to AWS in section 7, this currently will fail if you attempt to use a named builder as shown.

To remedy this, we should create an unnamed builder like so:

Instead of this:

FROM node:alpine as builder
WORKDIR '/app'
COPY package.json .
RUN npm install
COPY . .
RUN npm run build
 
FROM nginx
COPY --from=builder /app/build /usr/share/nginx/html

Do this:

FROM node:alpine
WORKDIR '/app'
COPY package.json .
RUN npm install
COPY . .
RUN npm run build
 
FROM nginx
COPY --from=0 /app/build /usr/share/nginx/html
--------------

### Implementing Multi-Step Builds 
see the Dockerfile in `frontend/`

### Running Nginx
Nginx' defay=ult port is 80, so you can run the production-ready app locally by running
`docker build .`
`docker run -p 8080:80 <image id>`  

