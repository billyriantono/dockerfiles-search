FROM ubuntu:latest

# Install utilities
RUN apt-get update --fix-missing && apt-get -y upgrade && apt-get install -y curl

# Install desired NodeJS verion
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash - && \
    apt-get install -y nodejs
