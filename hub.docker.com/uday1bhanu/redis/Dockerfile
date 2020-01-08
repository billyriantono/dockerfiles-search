FROM ubuntu:16.04
MAINTAINER Uday Bhanu Prasad "uday1bhanu@gmail.com"
ENV REFRESHED_AT 2017-03-28
RUN apt-get -yqq update; apt-get -yqq install redis-server redis-tools
EXPOSE 6379
RUN echo "Uday>> Welcome to my container!"
ENTRYPOINT [ "/usr/bin/redis-server" ]
CMD []
