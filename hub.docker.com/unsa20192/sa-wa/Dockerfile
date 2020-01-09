# base image
FROM node:carbon-slim

# set working directory
WORKDIR /app

# install and cache app dependencies
COPY *.json /app/
COPY *.js /app/
COPY src /app/src
RUN npm install

EXPOSE 8080

# start app
CMD ["npm", "run", "serve"]
