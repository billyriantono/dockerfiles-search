# Download base image ubuntu 16.04
FROM node:6.3

# Update Ubuntu Software repository & installed versions
RUN apt-get update && apt-get upgrade -y

# Install awscli dependencies & git
RUN apt-get install -y python-pip libpython-dev python-dev git

# Update pip
RUN pip install --upgrade pip

# Install awscli
RUN pip install awscli
