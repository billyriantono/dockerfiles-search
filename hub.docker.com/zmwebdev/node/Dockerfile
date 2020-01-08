FROM node

MAINTAINER zmwebdev

#nodemon node-inspector
RUN npm install -g nodemon
RUN npm i node-inspector --unsafe-perm -g

#vim
RUN apt-get update && apt-get -y install vim
RUN apt-get clean
RUN apt-get purge 

# replace this with your application's default port
# EXPOSE 3000