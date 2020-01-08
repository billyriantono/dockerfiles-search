# Define the base image
FROM node:carbon

# Create the app directory
WORKDIR /app

# Install app dependencies
COPY package*.json ./
RUN npm install

# Expose the port for the Vuejs server
EXPOSE 8081

# Expose node inpsect port
EXPOSE 9229

# Set the command to run at container start
CMD ["npm", "start"]