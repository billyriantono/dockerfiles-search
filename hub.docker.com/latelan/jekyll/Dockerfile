FROM ruby:2.5.0-alpine3.7

MAINTAINER coolboy1353@163.com

#RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories
#RUN gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/
RUN apk update --no-cache \
    && apk add --no-cache --virtual .build-deps build-base \
    && apk add --no-cache git openssh \
    && gem install jekyll jekyll-paginate \ 
    && apk del -f .build-deps

WORKDIR /opt/blog/
