FROM ruby:2.6.3-alpine3.9
# rails depends on nokogiri, nokogiri build need g++(depends on gcc) & make
# bundler build need linux-headers
RUN apk add g++ make linux-headers sqlite-dev
RUN gem install bundler
# setup timezone & logrotate
RUN apk add tzdata logrotate supervisor nginx bash
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo 'Asia/Shanghai' > /etc/timezone


