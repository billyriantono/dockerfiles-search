from python:3.6-alpine

LABEL maintainer="SungKwang Song <saltfactory@gmail.com>"

# RUN apk update && apk add gcc g++
RUN apk update && apk add ruby git
RUN echo "gem: --no-rdoc --no-ri" > ~/.gemrc
RUN gem install sass
RUN pip install awscli
RUN pip install awsebcli
RUN mkdir -p /var/app/current
WORKDIR /var/app/current
