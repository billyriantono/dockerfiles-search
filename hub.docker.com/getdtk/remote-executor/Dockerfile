# Docker Parent Image with Node and Typescript
FROM node:10-alpine

# Create Directory for the Container
WORKDIR /app

COPY package.json .

# Copy the files we need to our new Directory
COPY . /app

#Install typescript
RUN npm install -g typescript
# Grab dependencies and transpile src directory to dist
RUN npm install
RUN tsc

# Start the server
ENTRYPOINT ["npm", "start"]