# Use an official parent image
FROM node

# Set the working directory in which application will run
WORKDIR /meteocityapiserveur

# Copy the current directory contents into the container at /WORKDIR
COPY . /meteocityapiserveur
COPY ./implementation /meteocityapiserveur
COPY ./dependances /meteocityapiserveur
RUN mkdir ./logdir

# Install all needed packages specified in package.json
RUN npm install

# Run node app when the container launches
CMD ["node", "APIServer.js"]