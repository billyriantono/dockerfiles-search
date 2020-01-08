FROM node:8.1

# Create app directory
RUN mkdir -p /home/app
WORKDIR /home/app

# Install app dependencies
#COPY src/package.json /home/app/package.json

# Bundle app source
#COPY ./src /home/app

EXPOSE 8080
CMD [ "npm", "start" ]