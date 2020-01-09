# Use an official Linux 64 Python runtime as a parent image
FROM python:2.7.9
LABEL maintainer="Ignasi Andres <ignasi@ime.usp.br>"
LABEL description="Docker to run NAOQi."

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app/


# Make port 9559 available to the world outside this container
EXPOSE 80
EXPOSE 9559

