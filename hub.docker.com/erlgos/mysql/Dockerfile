FROM armhf/alpine:latest
MAINTAINER erlgo <erlgo@ipc6.com>

WORKDIR /app
VOLUME /app
COPY startup.sh /startup.sh
COPY my.cnf /my.cnf


EXPOSE 3306
CMD ["/startup.sh"]
