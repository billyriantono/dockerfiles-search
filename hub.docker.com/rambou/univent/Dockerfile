FROM node:6

# File Author / Maintainer
MAINTAINER Bousios Nikolaos

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Bundle app source
COPY . /usr/src/app

# Install app dependencies
RUN npm install

# Install forever and nodemon to keep server alive forever
RUN npm install -g pm2

# Generate Docs
RUN npm run api
# RUN npm run sys-api

# Expose port
EXPOSE  3000

# Run app using pm2
CMD ["pm2-docker", "--json", "process.yml"]
