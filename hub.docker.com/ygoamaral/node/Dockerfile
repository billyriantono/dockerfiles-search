FROM node:10.16.3

ENV LD_LIBRARY_PATH=/opt/oracle/instantclient_19_3

RUN apt update \ 
  && npm i -g nodemon \
  && mkdir /opt/oracle \
  && apt install libaio1 -y

COPY ./instantclient-basic-linux.x64-19.3.0.0.0dbru.zip /opt/oracle

RUN cd /opt/oracle \
  && unzip instantclient-basic-linux.x64-19.3.0.0.0dbru.zip \
  && rm -f instantclient-basic-linux.x64-19.3.0.0.0dbru.zip

WORKDIR /usr/app