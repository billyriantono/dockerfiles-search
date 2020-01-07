FROM ubuntu:14.04
RUN apt-get update && apt-get install -y nodejs && apt-get -y  install npm

EXPOSE 8080 443

CMD npm install && npm start
