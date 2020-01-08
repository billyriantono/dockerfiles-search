FROM node:8.16.0

#update and install required packages
RUN apt-get update
RUN apt-get install -y curl gettext
RUN apt-get -y autoclean

#set user to root so globally installed packages work (Kyle's concept)
RUN npm config set user 0

RUN npm install -g @bigcommerce/stencil-cli
RUN npm install node-bigcommerce
