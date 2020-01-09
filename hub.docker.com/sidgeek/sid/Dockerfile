# Use an official Python runtime as a parent image
FROM node:carbon

# Copy the current directory contents into the container at /app
ADD . /app

# Set the working directory to /app
WORKDIR /app/server

# Install any needed packages specified in requirements.txt
RUN yarn

# Make port 80 available to the world outside this container
# EXPOSE 80

# Define environment variable
# ENV NAME World

# Run app.py when the container launches
# CMD [ "/bin/sh", "-c", "while true; do sleep 3600; done"]
CMD ["npm", "run", "dev"]