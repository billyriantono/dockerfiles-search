FROM ubuntu:18.04

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get dist-upgrade -y
RUN apt-get install curl build-essential python3-pip zip jq -y
RUN pip3 install --upgrade pip
RUN pip3 install --upgrade awscli==1.14.5 s3cmd==2.0.1

# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash
RUN apt-get install nodejs -y
RUN node -v
RUN npm -v
