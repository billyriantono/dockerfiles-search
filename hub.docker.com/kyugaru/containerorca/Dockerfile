
FROM python:3.7-alpine 

RUN apk add g++
RUN apk add libevent-dev
RUN apk add python3-dev
RUN apk add python-dev
RUN apk add unixodbc
RUN apk add unixodbc-dev
RUN apk add gcc
RUN apk add libxslt-dev
RUN apk add libxml2-dev
RUN apk add --update util-linux
RUN apk add bash
RUN apk add nodejs
RUN apk add npm
RUN apk add curl

COPY ./requeriments.txt .
RUN pip install -r /requeriments.txt

WORKDIR /usr/lib/node_modules/npm
RUN npm i -g autodoc_yaml --ignore-scripts

WORKDIR /
