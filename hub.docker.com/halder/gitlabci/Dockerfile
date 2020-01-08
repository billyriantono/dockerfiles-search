FROM node

# Update and install npm
RUN apt-get -y update && apt-get -y install npm

# Install npm dependencies
RUN	npm install -g npm \
	npm install --save @angular/material @angular/cdk @angular/animations \
	npm install -g @angular/cli

