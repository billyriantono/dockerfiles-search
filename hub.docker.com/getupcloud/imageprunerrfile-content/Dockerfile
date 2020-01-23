FROM node:10-alpine

# Create Directory for the Container
WORKDIR /app

COPY package.json .

# Copy the files we need to our new Directory
COPY . /app

RUN npm install -g typescript

# Grab dependencies and transpile src directory to dist
RUN npm install
RUN tsc

# Start the server
ENTRYPOINT ["npm", "run", "debug"]
