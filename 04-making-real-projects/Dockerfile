FROM node:alpine

WORKDIR /usr/app

# changed from COPY ./ ./ to avoid unnecessary rebuilds of npm app
COPY ./package_json ./
RUN npm install
COPY ./ ./

CMD ["npm", "start"]