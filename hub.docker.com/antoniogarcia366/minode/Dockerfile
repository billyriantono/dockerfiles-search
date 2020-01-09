# Base Image
FROM node:latest

#App directory in the container
WORKDIR /app

#Copy files
ADD . /app

#Dependencies
RUN npm install

#Exposed port
EXPOSE 3000

#Command to execute the app
CMD ["npm", "start"]
