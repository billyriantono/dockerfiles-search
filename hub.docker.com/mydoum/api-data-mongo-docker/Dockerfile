# Dockerfile
# The FROM directive sets the Base Image for subsequent instructions
FROM node

COPY ./project /project
WORKDIR /project

RUN npm install

CMD node index.js data-mongo-docker.fresh 27017 3000

#Expose the port
EXPOSE 3000
