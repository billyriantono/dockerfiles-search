FROM library/python:3.5.3

MAINTAINER Tomasz Szymański <tomasz.szymanski@stxnext.com>

RUN apt-get update -y && apt-get install --no-install-recommends -y -q curl python build-essential git ca-certificates
RUN curl -sL https://deb.nodesource.com/setup_7.x -o nodesource_setup.sh && bash nodesource_setup.sh && apt-get install nodejs && npm install -g yarn
