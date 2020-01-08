# Use the official ubuntu:latest runtime as a base image
FROM ubuntu:latest

# Make use of -y -q in conjuction to avoid user interaction prompts
ENV DEBIAN_FRONTEND noninteractive

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages with apt-get
RUN apt-get update -q && \
    apt-get upgrade -y -q && \
    apt-get install -y -q curl git gnupg wget

# Include nodejs v8.x PPA
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -

# Install nodejs and build libs
RUN apt-get install -y -q libpng* nodejs make gcc g++ libc-dev bash

# Install yarn packages globally
RUN npm install -g yarn

# Install php7 + extensions
RUN sh php7-ext.sh

# Install composer
RUN sh composer.sh