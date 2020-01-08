# This image will be based on the official nodejs docker image
FROM node:latest
MAINTAINER <martinbryan.eu@gmail.com>
# Set in what directory commands will run
WORKDIR /home/app

# Put all our code inside that directory that lives in the container
ADD . /home/app

# Make sure NPM is not cached, remove everything first
RUN rm -rf /home/app/node_modules/npm \
 && rm -rf  /home/app/node_modules

# Install dependencies
RUN npm install

#Create an admin account
#RUN curl -H "Content-Type: application/json" -X POST -d '{ "username" : "admin", "password": "admin" }' http://localhost:8080/register

# Tell Docker we are going to use this port
EXPOSE 8080

# The command to run our app when the container is run
CMD ["node", "app.js"]

#RUN curl -H "Content-Type: application/json" -X POST -d '{ "username" : "admin", "password": "admin" }' http://localhost:8080/register
