# Arukas-API
FROM node:latest
RUN apt-get clean all
RUN apt-get update
RUN apt-get -y install git
RUN git clone https://bitbucket.org/HuanMeng/arukasapi.git /Arukas-API

ENV IS_CRON= 
ENV TOKEN=
ENV SECRET=

WORKDIR /Arukas-API
RUN npm install
EXPOSE 80
CMD node /Arukas-API/server.js $TOKEN $SECRET $IS_CRON 
