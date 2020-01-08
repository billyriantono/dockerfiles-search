FROM ubuntu:16.04

MAINTAINER Nguyen Huu Kim <kimnguyen.ict@gmail.com>

RUN apt-get update && apt-get install -y redis-server

EXPOSE 6379

# Run Redis Server
ENTRYPOINT  ["/usr/bin/redis-server"]
