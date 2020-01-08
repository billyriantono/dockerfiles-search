FROM node:10.15.3-stretch-slim

MAINTAINER Jaehoon Choi <plaintext@andromedarabbit.net>

RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y mysql-client && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*

COPY my.cnf /etc/my.cnf
COPY . /usr/src/app
ENV PATH /usr/src/app:${PATH}

VOLUME ["/usr/src/app/dumps"]

CMD ["./dump.js.command"]
