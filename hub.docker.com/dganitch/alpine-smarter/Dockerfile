FROM alpine:3.8

MAINTAINER Darin Ganitch dganitch@gmail.com

RUN apk update && \ 

        apk upgrade && \

        apk  add python py-pip  less mailcap curl wget nano bash && \

        pip install --upgrade awscli==1.14.5 s3cmd==2.0.1 python-magic && \ 
 
        pip install --upgrade pip

WORKDIR /app

COPY movie.sh /app

RUN chmod 700 movie.sh

ENV AWS_ACCESS_KEY_ID="***" \AWS_SECRET_ACCESS_KEY="***" \AWS_DEFAULT_REGION="us-west-2"
