FROM node:9

# Create app directory
WORKDIR /usr/app

# Setup args for build process
ARG CLIENT_PORT

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY template/package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm install --only=production

# Bundle app source
COPY . .

EXPOSE ${CLIENT_PORT}
