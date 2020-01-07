FROM node
MAINTAINER	Pablo Martinez <ing.martinez.pablo@gmail.com>

RUN apt update

# Install Maven and Java
RUN apt install -y maven default-jdk

# Install Chrome
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN dpkg -i google-chrome-stable_current_amd64.deb; apt-get -fy install

# Create the folder and Install the chromedriver
RUN mkdir /opt/nodejs
WORKDIR /opt/nodejs
RUN npm init --yes
RUN npm install chromedriver
