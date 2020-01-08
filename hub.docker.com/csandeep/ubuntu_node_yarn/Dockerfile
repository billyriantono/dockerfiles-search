# Pull base image.
FROM ubuntu:14.04

# Install Grunt and others
RUN apt-get update && \
    apt-get install -y curl && \
    curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash - && \
	apt-get install -y nodejs &&\
	curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - &&\
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list &&\
    apt-get update &&\
    apt-get install -y yarn && \
    apt-get clean && \
    mkdir -p /shared/voices
