# Use an official NodeJS runtime as a parent image
FROM node:8.11.3

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages and build the project
RUN npm install -g pm2
RUN npm install
RUN npm run prestart:prod

# Make port 80 available to the world outside this container
EXPOSE 3000

# Define environment variable
ENV NODE_ENV development

# Run main.js when the container launches
CMD ["pm2-runtime", "dist/main.js"]
