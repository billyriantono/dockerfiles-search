FROM node:8

# Make use of -y -q in conjuction to avoid user interaction prompts
ENV DEBIAN_FRONTEND noninteractive

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages with apt-get
RUN apt-get update -q && \
    apt-get upgrade -y -q && \
    apt-get install -y -q curl git

RUN npm install -g npm ionic cordova firebase-tools tslint typescript
