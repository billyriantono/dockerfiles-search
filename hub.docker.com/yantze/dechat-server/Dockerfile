# Use an official Python runtime as a parent image
FROM node:8.6.0
MAINTAINER Yantze <yantze@126.com>

# Set the working directory to /app
WORKDIR /app

RUN git clone --progress --verbose http://github.com/yantze/dechat /app \
    && npm install --production

# Make port 80 available to the world outside this container
EXPOSE 2020

# Define environment variable
ENV NAME dechat-server

# Run app.py when the container launches
CMD ["npm", "run", "server"]
