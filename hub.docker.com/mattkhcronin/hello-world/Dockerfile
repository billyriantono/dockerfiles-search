FROM node:boron

# Create app directory (arbitrary, anything but /)
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json /usr/src/app/
RUN npm install

# Bundle app source
COPY . /usr/src/app

# Expose node port to container
EXPOSE 8080

# Run command "npm start" to which calls "node app.js" to start the app
CMD ["npm", "start"]