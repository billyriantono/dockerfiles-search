# Dockerfile for Bitbucket pipeline
FROM  atlassian/default-image:2

RUN apt-get update
RUN apt-get install -y

# Install Node.js
RUN apt-get install --yes curl
RUN curl --silent --location https://deb.nodesource.com/setup_10.x
RUN apt-get install --yes nodejs
RUN apt-get install --yes build-essential

#Install SSHPass
RUN apt-get install sshpass
