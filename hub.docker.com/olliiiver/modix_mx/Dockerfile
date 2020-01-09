FROM ubuntu:disco

RUN apt-get update

RUN apt-get install -y git nodejs firefox wget npm 
RUN npm i -g npm

RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN dpkg -i google-chrome-stable_current_amd64.deb; apt-get -fy install

RUN npm install @modix/modix-mx -g --unsafe-perm=true
RUN npm install @modix/mx-cucumber-cli -g --unsafe-perm=true