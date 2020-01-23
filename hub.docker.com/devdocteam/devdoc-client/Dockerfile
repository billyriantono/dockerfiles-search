# Based on latest node (We might wanan specify the version here)
FROM node:latest

# Create a directory
RUN mkdir -p /usr/src/app

# Change working directoy so that our commands run inside this new directory
WORKDIR /usr/src/app

# Copy dependencies
COPY package.json /usr/src/app

# Get dependencies
RUN npm install

# Copy application
COPY . /usr/src/app

# Expose the port
EXPOSE 4200

# Serve the app
CMD ["npm", "start"]