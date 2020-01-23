FROM ruby:2.3.1
MAINTAINER Ethan 1451223089@qq.com

RUN apt-get update -y
WORKDIR /app

RUN gem install grape

ADD . /app

EXPOSE 8080

CMD ["rackup","-o","0.0.0.0","-p","8080"]
