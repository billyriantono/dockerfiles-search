FROM node:slim

LABEL authors="Mathieu De Haeck"

RUN apt-get update \
	&& apt-get install -y awscli \
    && npm install -g yarn typings @angular/cli
	
	
RUN echo "ng-aws-cli container created."