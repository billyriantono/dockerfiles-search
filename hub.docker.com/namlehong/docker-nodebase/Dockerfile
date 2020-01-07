FROM smebberson/alpine-nodejs

RUN npm install -g bower gulp nodemon

RUN mkdir /code
WORKDIR /code
ADD . /code/

EXPOSE 3000
EXPOSE 3001
