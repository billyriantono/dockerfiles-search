# specify the node base image with your desired version node:<version>
FROM node:8
 
WORKDIR /usr/src/app
 
# Install app dependencies
COPY package.json .
# For npm@5 or later, copy package-lock.json as well
#COPY package.json package-lock.json ./
 
RUN npm install
 
# Bundle app source
COPY . .
 
EXPOSE 8080
CMD [ "npm", "start", "server.js" ]
#CMD npm start server.js

#docker build -t <name-of-your-image> .