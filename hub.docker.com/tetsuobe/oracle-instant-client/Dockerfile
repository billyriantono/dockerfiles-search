FROM alpine

MAINTAINER tetsuobe@gmail.com

ADD ./bin .

RUN apk update && apk add --no-cache unzip \
	&& unzip instantclient-basic-linux.x64-12.2.0.1.0.zip -d /home/oracle