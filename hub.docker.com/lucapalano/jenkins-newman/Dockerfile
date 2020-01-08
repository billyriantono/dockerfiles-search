FROM jenkins
MAINTAINER Luca Palano <contact@lpzone.it>

LABEL version="0.1" \
	  releaseDate="01-09-2016"

USER root
RUN apt-get update && curl -sL https://deb.nodesource.com/setup_4.x | bash && apt-get install nodejs -y && npm install newman -g