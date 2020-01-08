FROM ubuntu:16.04
MAINTAINER hiromis

RUN apt update 
RUN apt -y upgrade
RUN apt -y dist-upgrade
RUN apt -y install curl wget build-essential checkinstall libssl-dev nodejs npm 
RUN npm install yarn -g
RUN npm install n -g
RUN npm install npm@5.3 -g
RUN n 8.1.3

RUN apt purge -y nodejs npm


