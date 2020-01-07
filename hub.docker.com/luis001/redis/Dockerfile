FROM ubuntu
MAINTAINER louis “luis_airc@sina.com”
ENV CREATE_TIME 2015-03-19
RUN apt-get update
RUN apt-get -y install redis-server redis-tools
EXPOSE 6379
ENTRYPOINT ["/usr/bin/redis-server"]
CMD []