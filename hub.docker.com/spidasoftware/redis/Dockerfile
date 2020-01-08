FROM ubuntu:14.04

RUN apt-get update && \
	apt-get install -y vim redis-server 2.6 && \
  	rm -rf /var/lib/apt/lists/*

EXPOSE 6379

ENTRYPOINT  ["/usr/bin/redis-server"]
