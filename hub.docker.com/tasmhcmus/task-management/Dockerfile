FROM node:latest

# info label
LABEL author="TASM"

# Create Directory for the Container
WORKDIR /app/taskmanagement

# Copy the files we need to our new Directory
ADD . /app/taskmanagement

# Expose the port outside of the container
EXPOSE 4000

# Grab dependencies and transpile src directory to dist
RUN npm install -g typescript && npm install && tsc

# Start the server
ENTRYPOINT ["node", "dist/server.js"]