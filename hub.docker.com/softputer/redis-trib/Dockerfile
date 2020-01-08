FROM ubuntu:trusty
MAINTAINER Jayson Ge <gyj3023@foxmail.com>

RUN apt-get update && \
    apt-get install -y ruby vim wget redis-tools && \
    wget http://download.redis.io/redis-stable/src/redis-trib.rb && \
    gem install redis && \
    chmod +x redis-trib.rb

