# Specify a base image
FROM node:alpine

# Set up a working directory
WORKDIR /usr/app

# Install the dependencies
COPY ./package.json ./
RUN npm install --loglevel=error

# Copy local files to remote image
COPY ./ ./

# Run a startup command
CMD ["npm", "start"]