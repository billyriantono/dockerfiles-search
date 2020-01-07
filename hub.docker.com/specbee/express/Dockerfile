# Create image based on the official Node 8 image from dockerhub
FROM node:8.11.3-alpine

# Install latest npm and express
RUN npm i -g npm@latest

# Create a directory where our app will be placed
RUN mkdir -p /usr/src/app

# Change directory so that our commands run inside this new directory
WORKDIR /usr/src/app

# Expose the port the app runs in
EXPOSE 3000

# Serve the app
CMD ["npm", "install"]