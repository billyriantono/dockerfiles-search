FROM node:12.13.1
MAINTAINER Vincent Castelain <vincent.castelain@dbit.lu>

RUN apt-get update && \
	apt-get install -y python python-pip python-dev jq && \
	pip install awscli==1.16.291

RUN npm i -g @angular/cli@8.3.19

ENV NODE_OPTIONS=--max_old_space_size=2048
