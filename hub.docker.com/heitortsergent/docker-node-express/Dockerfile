FROM ubuntu
MAINTAINER Heitor Tashiro Sergent <heitortsergent@gmail.com>

RUN apt-get update && \
	apt-get install -y \
 		nodejs \
 		npm \
 		nodejs-legacy

RUN npm install -g express-generator

EXPOSE 3000