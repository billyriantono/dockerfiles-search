# Base Image
FROM node:latest

#App directory in the container
WORKDIR /app

#Copy files
ADD  build/default /app/build/default
ADD server.js /app
ADD package.json /app

#Dependencies
RUN npm install

#Exposed port
EXPOSE 3000

#Command to execute the app
CMD ["npm", "start"]
