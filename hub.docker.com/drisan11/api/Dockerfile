# VERSION 1.0
# DOCKER-VERSION 1.11.2

# Base container
FROM node:latest

# App Start
ADD . /src
RUN chmod -R 777 /src

# Install app dependencies
WORKDIR /src
RUN npm install bcrypt --save
RUN npm install -g forever
RUN npm install
RUN touch .foreverignore
RUN chown -R $USER:$USER /src && chmod -R 777 /src

# Expose PORTS
EXPOSE 3000
EXPOSE 80

CMD [ "sh", "-c", "/src/start.sh" ]