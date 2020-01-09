#The first thing we need to do is define from what image we want to build from. Here we will use the latest LTS (long term support) version boron of node available from the Docker Hub:

FROM node:boron

#Next we create a directory to hold the application code inside the image, this will be the working directory for your application*/
# Create app directory

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

#This image comes with Node.js and NPM already installed so the next thing we need to do is to install your app dependencies using the npm binary*/
# Install app dependencies
COPY package.json /usr/src/app/
RUN npm install

#To bundle your app's source code inside the Docker image, use the COPY instruction*/
# Bundle app source
COPY . /usr/src/app
#Your app binds to port 8080 so you'll use the EXPOSE instruction to have it mapped by the docker daemon:
EXPOSE 8080
#Last but not least, define the command to run your app using CMD which defines your runtime. Here we will use the basic npm start which will run node server.js to start your server:
CMD [ "npm", "start" ]