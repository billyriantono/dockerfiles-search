
FROM dockerfile/nodejs:latest

MAINTAINER Govind R. "grajagopalan@opentable.com"

RUN apt-get update
RUN apt-get install -y default-jre
RUN apt-get install -y python-software-properties python build-essential curl libfreetype6 libfontconfig git-core
RUN apt-get install -y libcairo2-dev libjpeg8-dev libpango1.0-dev libgif-dev build-essential g++
RUN npm install -g grunt-cli phantomjs bower
