FROM ubuntu
MAINTAINER cinos81 "cinos81@gmail.com"
 
ENV REFRESHED_AT 2017-03-14
RUN apt-get update
RUN apt-get -y install redis-server redis-tools
COPY ./wait-for-it.sh /home
WORKDIR /home
EXPOSE 6379
ENTRYPOINT ["/usr/bin/redis-server"]
